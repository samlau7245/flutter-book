> 使用Bloc框架实现一个无限上拉列表的功能，里面涉及到网络API请求的基础功能。

初始化项目代码：

```bash
git clone -b bloc_infinite_list https://gitee.com/flutter-slu/examples.git
cd examples/
git checkout b2c8d2469cbc591c3cc59025d9c01443af010a90
```

# 效果

<img src="/assets/images/tutorial/state/07.gif"/>

# 结构

```
├── app.dart
├── main.dart
├── posts
│   ├── bloc
│   │   ├── post_bloc.dart
│   │   ├── post_event.dart
│   │   └── post_state.dart
│   ├── models
│   │   ├── models.dart
│   │   └── post.dart
│   ├── posts.dart
│   ├── view
│   │   ├── posts_list.dart
│   │   ├── posts_page.dart
│   │   └── view.dart
│   └── widgets
│       ├── bottom_loader.dart
│       ├── post_list_item.dart
│       └── widgets.dart
└── simple_bloc_observer.dart
```

# pubspec.yaml

```yaml
name: bloc_infinite_list
description: A new Flutter project.
publish_to: 'none' # Remove this line if you wish to publish to pub.dev
version: 1.0.0+1
environment:
  sdk: '>=2.12.0 <3.0.0'

dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.2
  flutter_bloc: ^7.0.0
  equatable: ^2.0.2
  rxdart: ^0.27.0
  http: ^0.13.3

dev_dependencies:
  flutter_test:
    sdk: flutter
flutter:
  uses-material-design: true
```

# post.dart 数据模型

```dart
import 'package:equatable/equatable.dart';

class Post extends Equatable {
  final int id;
  final String title;
  final String body;

  Post({required this.id, required this.title, required this.body});

  @override
  List<Object?> get props => [id, title, body];
}
```

# post_event.dart

* `PostFetched`: 它负责响应展示更多的数据。

```dart
part of 'post_bloc.dart';

abstract class PostEvent extends Equatable {
  const PostEvent();

  @override
  List<Object> get props => [];
}

class PostFetched extends PostEvent {}
```

# post_state.dart

* `PostInitial`: 告诉展示层需要加在数据。
* `PostSuccess`: 告诉展示层数据请求成功。
* `PostFailure`: 告诉展示层数据请求失败。

```dart
part of 'post_bloc.dart';

enum PostStatus { initial, success, failure }

class PostState extends Equatable {
  const PostState({
    this.status = PostStatus.initial,
    this.posts = const <Post>[],
    this.hasReachedMax = false,
  });

  final PostStatus status;
  final List<Post> posts;
  final bool hasReachedMax;

  PostState copyWith({
    PostStatus? status,
    List<Post>? posts,
    bool? hasReachedMax,
  }) {
    return PostState(
      status: status ?? this.status,
      posts: posts ?? this.posts,
      hasReachedMax: hasReachedMax ?? this.hasReachedMax,
    );
  }

  @override
  String toString() {
    return '''PostState { status: $status, hasReachedMax: $hasReachedMax, posts: ${posts.length} }''';
  }

  @override
  List<Object> get props => [status, posts, hasReachedMax];
}
```

* 相比之前的示例，这里的 State 已经不是一个`abstract`类，State 的类型也从子类变成了`enum`。
* 这里实现了一个 `copyWith` 方法，这样我们可以快速的创建一个`PostState`对象。

# post_bloc.dart

<img src="/assets/images/tutorial/state/02.png"/>

* 按照`Bloc`的框架设计，`HTTP`请求应该是在`data`数据层来做的，这里暂时就在Bloc中实现。

```dart
import 'dart:async';
import 'dart:convert';

import 'package:bloc/bloc.dart';
import 'package:bloc_infinite_list/posts/models/post.dart';
import 'package:equatable/equatable.dart';
import 'package:http/http.dart' as http;
import 'package:rxdart/rxdart.dart';

part 'post_event.dart';
part 'post_state.dart';

const _postLimit = 20;

class PostBloc extends Bloc<PostEvent, PostState> {
  final http.Client httpClient;

  PostBloc({required this.httpClient}) : super(PostState());

  @override
  Stream<Transition<PostEvent, PostState>> transformEvents(
    Stream<PostEvent> events,
    TransitionFunction<PostEvent, PostState> transitionFn,
  ) {
    /// `debounceTime` 这里使用了 RxDart 框架。
    return super.transformEvents(
        events.debounceTime(const Duration(milliseconds: 500)), transitionFn);
  }

  @override
  Stream<PostState> mapEventToState(PostEvent event) async* {
    if (event is PostFetched) {
      yield await _mapEventFetchToState();
    }
  }

  Future<PostState> _mapEventFetchToState() async {
    if (state.hasReachedMax) return state;

    try {
      if (state.status == PostStatus.initial) {
        final posts = await _fetechPosts();

        return state.copyWith(
          status: PostStatus.success,
          posts: posts,
          hasReachedMax: false,
        );
      }

      final posts = await _fetechPosts(state.posts.length);

      if (posts.isEmpty) {
        return state.copyWith(hasReachedMax: true);
      }

      return state.copyWith(
        status: PostStatus.success,
        posts: List.of(state.posts)..addAll(posts),
        hasReachedMax: false,
      );
    } catch (e) {
      return state.copyWith(status: PostStatus.failure);
    }
  }

  /// 网络请求
  Future<List<Post>> _fetechPosts([int startIndex = 0]) async {
    final response = await httpClient.get(
      Uri.https(
        'jsonplaceholder.typicode.com/',
        '/posts',
        <String, String>{'_start': '$startIndex', '_limit': '$_postLimit'},
      ),
    );

    if (response.statusCode == 200) {
      final body = json.decode(response.body) as List;

      return body.map((dynamic json) {
        return Post(
          id: json['id'] as int,
          title: json['title'] as String,
          body: json['body'] as String,
        );
      }).toList();
    }

    throw Exception('error fetching posts');
  }
}
```

# simple_bloc_observer.dart 监听Bloc  

如果是单个示例，在少量使用 Bloc的情况下，可以直接在Bloc代码中实现`onTransition`方法监控日志；但如果是一个大型项目，有多个Bloc的情况下，就可使用`BlocObserver`实现全局监听的功能。

```dart
import 'package:flutter_bloc/flutter_bloc.dart';

class SimpleBlocObserver extends BlocObserver {
  @override
  void onTransition(Bloc bloc, Transition transition) {
    super.onTransition(bloc, transition);
    print(transition);
  }

  @override
  void onError(BlocBase bloc, Object error, StackTrace stackTrace) {
    print(error);
    super.onError(bloc, error, stackTrace);
  }
}
```

在`main`中添加自定的监控代码:

```dart
void main() {
  Bloc.observer = SimpleBlocObserver();
  runApp(App());
}
```

# app.dart

创建一个`App` Widget，设置`home`属性为：`PostPage()`:

```dart
import 'package:bloc_infinite_list/posts/view/posts_page.dart';
import 'package:flutter/material.dart';

class App extends MaterialApp {
  App() : super(home: PostPage());
}
```

## posts_page.dart

在`PostPage` Widget中，使用`BlocProvider`把 Bloc 和 Widget 关联在一起；并且添加一个`PostFetched`事件让APP去初始化界面。

```dart
import 'package:bloc_infinite_list/posts/bloc/post_bloc.dart';
import 'package:bloc_infinite_list/posts/view/posts_list.dart';
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';
import 'package:http/http.dart' as http;

class PostPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Posts')),
      body: BlocProvider(
        create: (_) => PostBloc(
          httpClient: http.Client(),
        )..add(PostFetched()),
        child: PostList(),
      ),
    );
  }
}
```

## posts_list.dart

在`PostList` Widget中返回一个`BlocBuilder`， 用来处理不用 Bloc State情况下的 Widget展示。

```dart
import 'package:bloc_infinite_list/posts/bloc/post_bloc.dart';
import 'package:bloc_infinite_list/posts/widgets/post_list_item.dart';
import 'package:bloc_infinite_list/posts/widgets/widgets.dart';
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

class PostList extends StatefulWidget {
  @override
  _PostListState createState() => _PostListState();
}

class _PostListState extends State<PostList> {
  final _scrollController = ScrollController();
  late PostBloc _postBloc;

  @override
  void initState() {
    _scrollController.addListener(_onScroll);
    _postBloc = context.read<PostBloc>();
    super.initState();
  }

  @override
  void dispose() {
    _scrollController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return BlocBuilder<PostBloc, PostState>(
      builder: (context, state) {
        print('PostList.build:$state');

        switch (state.status) {
          case PostStatus.success:
            return statusSuccess(state);
          case PostStatus.failure:
            return Center(child: Text('failed to fetch posts'));
          default:
            return Center(child: const CircularProgressIndicator());
        }
      },
    );
  }

  Widget statusSuccess(PostState state) {
    if (state.posts.isEmpty) {
      return const Center(child: Text('no posts'));
    }

    return ListView.builder(
      itemBuilder: (_, index) {
        return index >= state.posts.length
            ? BottomLoader()
            : PostListItem(
                post: state.posts[index],
              );
      },
      itemCount:
          state.hasReachedMax ? state.posts.length : state.posts.length + 1,
      controller: _scrollController,
    );
  }

  void _onScroll() {
    if (_isBottom) _postBloc.add(PostFetched());
  }

  bool get _isBottom {
    if (!_scrollController.hasClients) return false;
    final maxScroll = _scrollController.position.maxScrollExtent;
    final currentScroll = _scrollController.offset;
    return currentScroll >= (maxScroll * 0.9);
  }
}
```

源代码：

```bash
git clone -b bloc_infinite_list https://gitee.com/flutter-slu/examples.git
cd examples/
git checkout c7a469008325b8899830f70c61d0aaff91f7bf61
```