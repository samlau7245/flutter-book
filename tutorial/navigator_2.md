
Navigator 2.0

## 概述

Navigator2.0 是一套全新的声明式的API。

> `声明式API`VS`声明式API`

新功能页面概述：

* `Page`: 用来表示 `Navigator` 路由栈中各个页面的配置信息。
* `Router`: 用来制定要由 `Navigator` 展示的页面列表，通常，该页面列表会根据系统或应用程序的状态改变而改变。
* `RouteInformationParser`: 持有 `RouteInformationProvider` 提供的  `RouteInformation` ，可以将其解析为我们定义的数据类型。
* `RouterDelegate`: 定义应用程序中的路由行为，例如 Router 如何知道应用程序状态的变化以及如何响应。主要的工作就是监听  `RouteInformationParser` 和应用状态并通过当前页面列表构建。
* `BackButtonDispatcher`，响应后退按钮，并通知 Router。

这张图展示了 `RouterDelegate` `Router` `RouteInformationParser` 以及`应用状态` 的交互原理：

<img src="/assets/images/navigator_2/01.png"/>

大致流程：

* 当系统打开新页面（如 `books/2`）时，`RouteInformationParser` 会将其转换为应用中的具体数据类型 T（如 BooksRoutePath）。
* 该数据类型会被传递给 `RouterDelegate` 的 `setNewRoutePath` 方法，我们可以在这里更新路由状态（如通过设置 selectedBookId）并调用 `notifyListeners` 响应该操作。
* `notifyListeners` 会通知 `Router` 重建 `RouterDelegate`（通过 build() 方法）.
* `RouterDelegate.build()` 返回一个新的 `Navigator` 实例，并最终展示出我们想要打开的页面（如 selectedBookId）。

## 示例

### Book书架

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(BookApp());
}

class BookApp extends StatefulWidget {
  @override
  _BookAppState createState() => _BookAppState();
}

class _BookAppState extends State<BookApp> {
  Book _selectedBook;
  bool show404 = false;
  List<Book> books = [
    Book('Stranger in a Strange Land', 'Robert A. Heinlein'),
    Book('Foundation', 'Isaac Asimov'),
    Book('Fahrenheit 451', 'Ray Bradbury'),
  ];

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Book App',
      theme: ThemeData(primaryColor: Colors.blue),
      home: Navigator(
        /// `Navigator` 接受一个 `pages` 参数，如果 `Page` 列表发生变化，
        /// `Navigator` 也需要更新当前路由栈来保持同步。
        pages: [
          /// `Scaffold()`只展示一个白屏页面
          /// MaterialPage(child: Scaffold(), key: ValueKey('BookListPage')),
          MaterialPage(
            child: BooksListScreen(books: books, onTaped: _onTaped),
            key: ValueKey('BookListPage'),
          ),

          /// 展示404页面
          if (show404)
            MaterialPage(child: UnknownScreen(), key: ValueKey('UnknownPage'))
          else if (_selectedBook != null)
            MaterialPage(
                child: BookDetailsScreen(
                  book: _selectedBook,
                ),
                key: ValueKey(_selectedBook))
        ],
        onPopPage: _onPopPage,
      ),
    );
  }

  bool _onPopPage(Route<dynamic> route, result) {
    return route.didPop(result);
  }

  /// 点击跳转到详情
  _onTaped(Book book) {
    setState(() {
      _selectedBook = book;
    });
  }
}

/// 书籍相关信息的类
class Book {
  final String title;
  final String author;

  Book(this.title, this.author);
}

/// 书籍列表页
class BooksListScreen extends StatelessWidget {
  final List<Book> books;
  final ValueChanged<Book> onTaped;

  const BooksListScreen({Key key, @required this.books, @required this.onTaped})
      : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('BookList'),
      ),
      body: ListView(
        children: [
          for (var book in books)
            ListTile(
              title: Text(book.title),
              subtitle: Text(book.author),
              onTap: () => onTaped(book),
            )
        ],
      ),
    );
  }
}

/// 404页面
class UnknownScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('404'),
      ),
      body: Center(
        child: Text('404!'),
      ),
    );
  }
}

/// Book详情页面
class BookDetailsScreen extends StatelessWidget {
  final Book book;

  const BookDetailsScreen({Key key, @required this.book}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(),
      body: Padding(
        padding: const EdgeInsets.all(8.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            if (book != null) ...[
              Text(book.title, style: Theme.of(context).textTheme.headline6),
              Text(book.author, style: Theme.of(context).textTheme.subtitle1),
            ],
          ],
        ),
      ),
    );
  }
}
```

<img src="/assets/images/navigator_2/02.gif"/>

现在，我们基本实现了声明式的路由管理，但是暂时无法处理浏览器的后退、前进按钮，也无法实现同步浏览器地址栏的链接。


### 通过自定义`Page`来实现等同功能

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(BookApp());
}

class BookApp extends StatefulWidget {
  @override
  _BookAppState createState() => _BookAppState();
}

class _BookAppState extends State<BookApp> {
  Book _selectedBook;
  bool show404 = false;
  List<Book> books = [
    Book('Stranger in a Strange Land', 'Robert A. Heinlein'),
    Book('Foundation', 'Isaac Asimov'),
    Book('Fahrenheit 451', 'Ray Bradbury'),
  ];

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Book App',
      theme: ThemeData(primaryColor: Colors.blue),
      home: Navigator(
        pages: [
          MaterialPage(
            child: BooksListScreen(books: books, onTaped: _onTaped),
            key: ValueKey('BookListPage'),
          ),

          /// 展示404页面
          if (show404)
            MaterialPage(child: UnknownScreen(), key: ValueKey('UnknownPage'))
          else if (_selectedBook != null)
            /* 把这段替换
            MaterialPage(
              child: BookDetailsScreen(book: _selectedBook),
              key: ValueKey(_selectedBook),
            )*/
            BookDetailsPage(book: _selectedBook)
        ],
        onPopPage: _onPopPage,
      ),
    );
  }

  bool _onPopPage(Route<dynamic> route, result) {
    /* 把这段替换
    return route.didPop(result);
    */

    if (!route.didPop(result)) {
      return false;
    }

    /// 通过设置 `_selectedBook` 为空来更新 list 的列表。
    setState(() {
      _selectedBook = null;
    });
    return true;
  }

  /// 点击跳转到详情
  _onTaped(Book book) {
    setState(() {
      _selectedBook = book;
    });
  }
}

/// 书籍相关信息的类
class Book {
  final String title;
  final String author;

  Book(this.title, this.author);
}

/// 书籍列表页
class BooksListScreen extends StatelessWidget {
  final List<Book> books;
  final ValueChanged<Book> onTaped;

  const BooksListScreen({Key key, @required this.books, @required this.onTaped})
      : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('BookList'),
      ),
      body: ListView(
        children: [
          for (var book in books)
            ListTile(
              title: Text(book.title),
              subtitle: Text(book.author),
              onTap: () => onTaped(book),
            )
        ],
      ),
    );
  }
}

/// 404页面
class UnknownScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('404'),
      ),
      body: Center(
        child: Text('404!'),
      ),
    );
  }
}

/// Book详情页面
class BookDetailsScreen extends StatelessWidget {
  final Book book;

  const BookDetailsScreen({Key key, @required this.book}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(),
      body: Padding(
        padding: const EdgeInsets.all(8.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            if (book != null) ...[
              Text(book.title, style: Theme.of(context).textTheme.headline6),
              Text(book.author, style: Theme.of(context).textTheme.subtitle1),
            ],
          ],
        ),
      ),
    );
  }
}

/// 我们还可以继承 `Page` 来实现等同功能
class BookDetailsPage extends Page {
  final Book book;

  BookDetailsPage({@required this.book}) : super(key: ValueKey(book));

  @override
  Route createRoute(BuildContext context) {
    return MaterialPageRoute(
      builder: (_) => BookDetailsScreen(book: book),
      settings: this,
    );
  }
}

```

### 实现自定义Page，并添加自定义行为(过渡动画)

修改`BookDetailsPage`类：

```dart
class BookDetailsPage extends Page {
  final Book book;

  BookDetailsPage({@required this.book}) : super(key: ValueKey(book));

  @override
  Route createRoute(BuildContext context) {
    /*把这段替换掉
    return MaterialPageRoute(
      settings: this,
      builder: (_) => BookDetailsScreen(book: book),
    );
    */
    return PageRouteBuilder(
      pageBuilder: (BuildContext context, Animation<double> animation,
          Animation<double> secondaryAnimation) {
        final tween = Tween(begin: Offset(0.0, 1.0), end: Offset.zero);
        final curveTween = CurveTween(curve: Curves.easeInOut);
        return SlideTransition(
          position: animation.drive(curveTween).drive(tween),
          child: BookDetailsScreen(
            key: ValueKey(book),
            book: book,
          ),
        );
      },
      settings: this,
    );
  }
}
```

<img src="/assets/images/navigator_2/03.gif"/>

### 实现路由更新、浏览器地址同步

通过`RouteInformationParser`,`RouterDelegate` 更新路由状态，实现与浏览器地址拦中的链接同步。

```dart
import 'package:flutter/material.dart';
import 'package:flutter/rendering.dart';

void main() {
  runApp(BookApp());
}

class BookApp extends StatefulWidget {
  @override
  _BookAppState createState() => _BookAppState();
}

class _BookAppState extends State<BookApp> {
  BookRouterDelegate _routerDelegate = BookRouterDelegate();
  BookRouteInformationParser _routeInformationParser =
      BookRouteInformationParser();

  @override
  Widget build(BuildContext context) {
    return MaterialApp.router(
      routeInformationParser: _routeInformationParser,
      routerDelegate: _routerDelegate,
      title: 'Books App',
    );
  }
}

/// 书籍相关信息的类
class Book {
  final String title;
  final String author;

  Book(this.title, this.author);
}

/// 书籍列表页
class BooksListScreen extends StatelessWidget {
  final List<Book> books;
  final ValueChanged<Book> onTaped;

  const BooksListScreen({Key key, @required this.books, @required this.onTaped})
      : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('BookList'),
      ),
      body: ListView(
        children: [
          for (var book in books)
            ListTile(
              title: Text(book.title),
              subtitle: Text(book.author),
              onTap: () => onTaped(book),
            )
        ],
      ),
    );
  }
}

/// 404页面
class UnknownScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('404'),
      ),
      body: Center(
        child: Text('404!'),
      ),
    );
  }
}

/// Book详情页面
class BookDetailsScreen extends StatelessWidget {
  final Book book;

  const BookDetailsScreen({Key key, @required this.book}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(),
      body: Padding(
        padding: const EdgeInsets.all(8.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            if (book != null) ...[
              Text(book.title, style: Theme.of(context).textTheme.headline6),
              Text(book.author, style: Theme.of(context).textTheme.subtitle1),
            ],
          ],
        ),
      ),
    );
  }
}

/// 我们还可以继承 `Page` 来实现自定义行为，例如，在该页面添加了自定义过渡动画。
/*
class BookDetailsPage extends Page {
  final Book book;

  BookDetailsPage({@required this.book}) : super(key: ValueKey(book));

  @override
  Route createRoute(BuildContext context) {
    return MaterialPageRoute(
      builder: (_) => BookDetailsScreen(book: book),
      settings: this,
    );
  }
}
*/

class BookDetailsPage extends Page {
  final Book book;

  BookDetailsPage({@required this.book}) : super(key: ValueKey(book));

  @override
  Route createRoute(BuildContext context) {
    return MaterialPageRoute(
      settings: this,
      builder: (_) => BookDetailsScreen(book: book),
    );
  }
}
```

使用`BookRoutePath`类来表示应用程序中的路由路径。

```dart
class BookRoutePath {
  final int id;
  final bool isUnknown;

  BookRoutePath(this.id, this.isUnknown);

  BookRoutePath.home()
      : id = null,
        isUnknown = false;

  BookRoutePath.unknown()
      : id = null,
        isUnknown = true;

  BookRoutePath.details(this.id) : isUnknown = false;

  bool get isHomePage => id == null;
  bool get isDetailPage => id != null;
}
```

* `BookRouterDelegate`的泛型为`BookRoutePath`， 其中包含了决定显示哪个页面所需的所有状态。
* 为了能在 URL 中显示正确的路径，我们也需要根据应用程序的当前状态返回一个`BookRoutePath`对象，可以继承`currentConfiguration`方法，在方法中实现。
* 因为 `BookRouterDelegate`不是一个组件，所以在`_onTaped`方法中就得使用`notifyListeners`来代替`setState`来更新状态；当`RouterDelegate`触发状态更新时，`Router`组件同样会触发`RouterDelegate`的`currentConfiguration`方法并调用`build`方法来创建一个新的`Navigator`组件。
* 当新页面打开后，`Router`会调用`setNewRoutePath`方法来更新应用程序的路由状态。

```dart
class BookRouterDelegate extends RouterDelegate<BookRoutePath>
    with ChangeNotifier, PopNavigatorRouterDelegateMixin<BookRoutePath> {
  Book _selectedBook;
  bool show404 = false;

  List<Book> books = [
    Book('Stranger in a Strange Land', 'Robert A. Heinlein'),
    Book('Foundation', 'Isaac Asimov'),
    Book('Fahrenheit 451', 'Ray Bradbury'),
  ];

  bool _onPopPage(Route<dynamic> route, result) {
    if (!route.didPop(result)) {
      return false;
    }

    _selectedBook = null;
    show404 = false;

    notifyListeners();
    return true;
  }

  /// 点击跳转到详情
  /// 因为 `BookRouterDelegate`不是组件，而是由`ChangeNotifier`实现，
  /// 所以`setState()`方法要使用`notifyListeners()`来代替，实现状态的改变。
  _onTaped(Book book) {
    /*setState(() {});*/
    _selectedBook = book;
    notifyListeners();
  }

  /// build 返回一个`Navigator`组件
  @override
  Widget build(BuildContext context) {
    return Navigator(
      pages: [
        MaterialPage(
          child: BooksListScreen(books: books, onTaped: _onTaped),
          key: ValueKey('BookListPage'),
        ),
        if (show404)
          MaterialPage(child: UnknownScreen(), key: ValueKey('UnknownPage'))
        else if (_selectedBook != null)
          BookDetailsPage(book: _selectedBook)
      ],
      onPopPage: _onPopPage,
    );
  }

  @override
  GlobalKey<NavigatorState> get navigatorKey => GlobalKey<NavigatorState>();

  /// 开新页面后，`Router` 会调用`setNewRoutePath`方法来更新应用程序的路由状态。
  @override
  Future<void> setNewRoutePath(BookRoutePath path) async {
    print('setNewRoutePath:${path.id}');

    if (path.isUnknown) {
      _selectedBook = null;
      show404 = true;
      return;
    }

    if (path.isDetailPage) {
      if (path.id < 0 || path.id > books.length - 1) {
        show404 = true;
        return;
      }
      _selectedBook = books[path.id];
    } else {
      _selectedBook = null;
    }

    show404 = false;
  }

  /// 当 `RouterDelegate` 触发状态更新时，`Router` 同样会触发 `RouterDelegate`
  /// 的 `currentConfiguration` 方法并调用 `build` 方法创建出一个新的 `Navigator` 组件。
  @override
  BookRoutePath get currentConfiguration {
    print('currentConfiguration');
    if (show404) {
      return BookRoutePath.unknown();
    }
    return _selectedBook == null
        ? BookRoutePath.home()
        : BookRoutePath.details(books.indexOf(_selectedBook));
  }
}
```

* `BookRouteInformationParser`内部可以接收到路由的信息`RouteInformation`，我们可以把它转换成自定义的路由数据类型`BookRoutePath`。

```dart
class BookRouteInformationParser extends RouteInformationParser<BookRoutePath> {
  /// 把路由信息`RouteInformation`转换成指定的数据类型`BookRoutePath`
  /// 并用`Uri`进行解析
  @override
  Future<BookRoutePath> parseRouteInformation(
      RouteInformation routeInformation) async {
    final uri = Uri.parse(routeInformation.location);

    // Handle '/'
    if (uri.pathSegments.length == 0) {
      return BookRoutePath.home();
    }

    // Handle '/book/:id'
    if (uri.pathSegments.length == 2) {
      if (uri.pathSegments[0] != 'book') return BookRoutePath.unknown();

      var id = int.tryParse(uri.pathSegments[1]);
      if (id == null) return BookRoutePath.unknown();

      return BookRoutePath.details(id);
    }

    // Handle unkonwn routes
    return BookRoutePath.unknown();
  }

  @override
  RouteInformation restoreRouteInformation(BookRoutePath path) {
    if (path.isUnknown) {
      return RouteInformation(location: '/404');
    }
    if (path.isHomePage) {
      return RouteInformation(location: '/');
    }
    if (path.isDetailPage) {
      return RouteInformation(location: '/book/${path.id}');
    }
    return null;
  }
}
```

<img src="/assets/images/navigator_2/04.gif"/>

### 给自定义路由设置路由动画

```dart
class NoAnimationTransitionDelegate extends TransitionDelegate<void> {
  @override
  Iterable<RouteTransitionRecord> resolve(
      {List<RouteTransitionRecord> newPageRouteHistory,
      Map<RouteTransitionRecord, RouteTransitionRecord>
          locationToExitingPageRoute,
      Map<RouteTransitionRecord, List<RouteTransitionRecord>>
          pageRouteToPagelessRoutes}) {
    final results = <RouteTransitionRecord>[];

    for (var pageRoute in newPageRouteHistory) {
      if (pageRoute.isWaitingForEnteringDecision) {
        pageRoute.markForAdd();
      }
      results.add(pageRoute);
    }

    for (var exitingPageRoute in locationToExitingPageRoute.values) {
      if (exitingPageRoute.isWaitingForExitingDecision) {
        exitingPageRoute.markForRemove();
        final pagelessRoutes = pageRouteToPagelessRoutes[exitingPageRoute];
        if (pagelessRoutes != null) {
          for (final pagelessRoute in pagelessRoutes) {
            pagelessRoute.markForRemove();
          }
        }
        results.add(exitingPageRoute);
      }
    }

    return results;
  }
}
```

* `markForPush`: 打开页面时使用过渡动画。
* `markForAdd`: 打开页面时不使用过渡动画。
* `markForPop`: 弹出页面时使用动画，并通知应用，即将该事件传递给 AppRouterDelegate 的 onPopPage 函数。
* `markForComplete`: 弹出页面时不使用过渡动画，同样会通知应用。
* `markForRemove`: 弹出页面时不使用过渡动画，不会通知应用。

```dart
class BookRouterDelegate extends RouterDelegate<BookRoutePath>
    with ChangeNotifier, PopNavigatorRouterDelegateMixin<BookRoutePath> {
  @override
  Widget build(BuildContext context) {
    return Navigator(
      transitionDelegate: NoAnimationTransitionDelegate(),
      //...
    );
  }
  //...
}
```

## 嵌套路由

## 其他

```dart
Router({
	Key key, 
    RouteInformationProvider routeInformationProvider, 
    RouteInformationParser<T> routeInformationParser, 
    @required RouterDelegate<T> routerDelegate, 
    BackButtonDispatcher backButtonDispatcher
})
```

RouterDelegate

```
// RouterDelegate 继承了 Listenable ，它可以实现实时监听对象的状态。
abstract class RouterDelegate<T> extends Listenable{}
```

```dart
build(BuildContext context) → Widget
popRoute() → Future<bool>
setInitialRoutePath(T configuration) → Future<void>
setNewRoutePath(T configuration) → Future<void>
```

```dart
// @see https://api.flutter.dev/flutter/widgets/RouterDelegate/setNewRoutePath.html
@override
Future<void> setNewRoutePath(configuration) {
  throw UnimplementedError();
}
```


```dart
class Navigator2RouteDelegate extends RouterDelegate<String> {
  @override
  Widget build(BuildContext context) {
    return Navigator(
      pages: [],
      onPopPage: _onPopPage,
    );
  }
  ...
}

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  @override
  Widget build(BuildContext context) {
    return MaterialApp.router(
      routerDelegate: delegate,
      title: 'Flutter Demo',
    );
  }
}
```

当`RouterDelegate`对象传入`MaterialApp.router()`构造函数后，`RouterDelegate.build`中的`Navigator`就成为了`Router`的子组件了。



* [Flutter Navigator2.0 完全指南与原理解析](https://mp.weixin.qq.com/s/hDLxWJuUylw8UaOidUa3Hg)
* [RouterDelegate class](https://api.flutter.dev/flutter/widgets/RouterDelegate-class.html)
* [Navigator 2.0 and Router 官方公开分享](https://docs.google.com/document/d/1Q0jx0l4-xymph9O6zLaOY4d_f7YFpNWX_eGbzYxr9wY/edit#)

* MaterialPageRoute()
* MaterialApp()
* Material()
* Scaffold()
* MaterialPage()






