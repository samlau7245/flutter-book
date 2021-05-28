> 使用Bloc框架实现一个登录界面的功能。

初始化项目：

```bash
git clone -b bloc_login https://gitee.com/flutter-slu/examples.git
cd examples/
git checkout d572ba8769f6b0de40318cf37deee32eeb937df6
```

# 效果

<img src="/assets/images/tutorial/state/08.gif"/>

# 结构

```
├── lib
│   ├── app.dart
│   ├── authentication
│   │   ├── authentication.dart
│   │   └── bloc
│   │       ├── authentication_bloc.dart
│   │       ├── authentication_event.dart
│   │       └── authentication_state.dart
│   ├── home
│   │   ├── home.dart
│   │   └── view
│   │       └── home_page.dart
│   ├── login
│   │   ├── bloc
│   │   │   ├── login_bloc.dart
│   │   │   ├── login_event.dart
│   │   │   └── login_state.dart
│   │   ├── login.dart
│   │   ├── models
│   │   │   ├── models.dart
│   │   │   ├── password.dart
│   │   │   └── username.dart
│   │   └── view
│   │       ├── login_form.dart
│   │       ├── login_page.dart
│   │       └── view.dart
│   ├── main.dart
│   └── splash
│       ├── splash.dart
│       └── view
│           └── splash_page.dart  // APP的启动页，只有个loading效果
├── packages
│   ├── authentication_repository
│   │   ├── lib
│   │   │   ├── authentication_repository.dart
│   │   │   └── src
│   │   │       └── authentication_repository.dart
│   │   └── pubspec.yaml
│   └── user_repository
│       ├── lib
│       │   ├── src
│       │   │   ├── models
│       │   │   │   ├── models.dart
│       │   │   │   └── user.dart
│       │   │   └── user_repository.dart
│       │   └── user_repository.dart
│       └── pubspec.yaml
└── pubspec.yaml
```

# package

## authentication_repository 鉴权包

在项目中创建一个新的 `authentication_repository` package 用来校验用户的登录权限`login`、`logout`。

### pubspec.yaml

```yaml
name: authentication_repository
description: A starting point for Dart libraries or applications.
version: 1.0.0
environment:
  sdk: '>=2.12.0 <3.0.0'
dev_dependencies:
  pedantic: ^1.10.0
  test: ^1.16.0
```

### authentication_repository.dart

```dart
import 'dart:async';

enum AuthenticationStatus { unknown, authenticated, unauthenticated }

class AuthenticationRepository {
  final _controller = StreamController<AuthenticationStatus>();

  Stream<AuthenticationStatus> get status async* {
    await Future<void>.delayed(const Duration(seconds: 1));
    yield AuthenticationStatus.unauthenticated;
    yield* _controller.stream;
  }

  Future<void> logIn({
    required String username,
    required String password,
  }) async {
    await Future.delayed(
      const Duration(milliseconds: 300),
      () => _controller.add(AuthenticationStatus.authenticated),
    );
  }

  void logOut() {
    _controller.add(AuthenticationStatus.unauthenticated);
  }

  void dispose() => _controller.close();
}
```

`AuthenticationRepository` 鉴权包负责告诉App，用户什么时候登录或者登出。

## user_repository

### pubspec.yaml

```yaml
name: user_repository
description: A starting point for Dart libraries or applications.
version: 1.0.0

environment:
  sdk: '>=2.12.0 <3.0.0'
  
dev_dependencies:
  pedantic: ^1.10.0
  test: ^1.16.0

dependencies: 
  equatable: ^2.0.2
  uuid: ^3.0.4
```

### user.dart

```dart
import 'package:equatable/equatable.dart';

class User extends Equatable {
  /// 用户的ID
  final String id;

  const User(this.id);

  @override
  List<Object?> get props => [id];

  static const empty = User('-');
}
```

### user_repository.dart

在 `UserRepository` 中，随机生成用户的随机UUID编码。

```dart
import 'package:uuid/uuid.dart';

import 'models/models.dart';

class UserRepository {
  User? _user;

  Future<User?> getUser() async {
    if (_user != null) return _user;
    return Future.delayed(
      const Duration(milliseconds: 300),
      () => _user = User(const Uuid().v4()),
    );
  }
}
```

# pubspec.yaml

把两个包依赖到主项目中：

```yaml
name: bloc_login
description: A new Flutter project.
publish_to: 'none' # Remove this line if you wish to publish to pub.dev
version: 1.0.0+1
environment:
  sdk: ">=2.12.0 <3.0.0"

dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.2
  flutter_bloc: ^7.0.0
  equatable: ^2.0.2
  formz: ^0.4.0 # Form 字段校验工具
  authentication_repository:
    path: packages/authentication_repository
  user_repository:
    path: packages/user_repository

dev_dependencies:
  flutter_test:
    sdk: flutter
flutter:
  uses-material-design: true
```

# authentication Bloc

## authentication_event.dart

* `AuthenticationStatusChanged`: 这个事件作用就是通知 Bloc 需要改变用户的 `AuthenticationStatus`。
* `AuthenticationLogoutRequested`: 这个事件作用就是通知 Bloc 请求 `logout`，登出。

```dart
part of 'authentication_bloc.dart';

abstract class AuthenticationEvent extends Equatable {
  const AuthenticationEvent();

  @override
  List<Object> get props => [];
}

// AuthenticationStatusChanged: notifies the bloc of a change to the user's AuthenticationStatus
class AuthenticationStatusChanged extends AuthenticationEvent {
  final AuthenticationStatus status;
  const AuthenticationStatusChanged(this.status);

  @override
  List<Object> get props => [status];
}

// AuthenticationLogoutRequested: notifies the bloc of a logout request
class AuthenticationLogoutRequested extends AuthenticationEvent {}
```

## authentication_state.dart

`AuthenticationState` 创建三种构造函数：

* `AuthenticationState.unknown()`: 默认状态，。
* `AuthenticationState.authenticated()`: 。
* `AuthenticationState.unauthenticated()`: 。


```dart
part of 'authentication_bloc.dart';

class AuthenticationState extends Equatable {
  final User user;
  final AuthenticationStatus status;

  const AuthenticationState._({
    this.status = AuthenticationStatus.unknown,
    this.user = User.empty,
  });

  const AuthenticationState.unkonwn() : this._();

  const AuthenticationState.authenticated(User user)
      : this._(status: AuthenticationStatus.authenticated, user: user);

  const AuthenticationState.unauthenticated()
      : this._(status: AuthenticationStatus.unauthenticated);

  @override
  List<Object> get props => [status, user];
}
```

## authentication_bloc.dart

`AuthenticationBloc` 依赖的两个鉴权的包：`AuthenticationRepository`和`UserRepository`，并且设置了初始化State为`AuthenticationState.unknown()`。

创建了一个`StreamSubscription`，来订阅鉴权包中`status`流状态的改变，当流状态发生改变时响应响应`AuthenticationStatusChanged` 事件。

```dart
import 'dart:async';

import 'package:authentication_repository/authentication_repository.dart';
import 'package:bloc/bloc.dart';
import 'package:equatable/equatable.dart';
import 'package:user_repository/user_repository.dart';

part 'authentication_event.dart';
part 'authentication_state.dart';

class AuthenticationBloc
    extends Bloc<AuthenticationEvent, AuthenticationState> {
  AuthenticationBloc(
      {required authenticationRepository, required userRepository})
      : this._authenticationRepository = authenticationRepository,
        this._userRepository = userRepository,
        super(AuthenticationState.unkonwn()) {
    // 监听鉴权包用户状态的变化
    _authenticationStatusSubscription = _authenticationRepository.status
        .listen((status) => add(AuthenticationStatusChanged(status)));
  }

  @override
  Future<void> close() {
    _authenticationStatusSubscription.cancel();
    _authenticationRepository.dispose();
    return super.close();
  }

  final AuthenticationRepository _authenticationRepository;
  final UserRepository _userRepository;

  late StreamSubscription<AuthenticationStatus>
      _authenticationStatusSubscription;

  @override
  Stream<AuthenticationState> mapEventToState(
      AuthenticationEvent event) async* {
    if (event is AuthenticationStatusChanged) {
      yield await _mapEventStatusChangedToState(event);
    } else if (event is AuthenticationLogoutRequested) {
      _authenticationRepository.logOut();
    }
  }

  Future<AuthenticationState> _mapEventStatusChangedToState(
      AuthenticationStatusChanged event) async {
    switch (event.status) {
      case AuthenticationStatus.unauthenticated:
        return const AuthenticationState.unauthenticated();
      case AuthenticationStatus.authenticated:
        final user = await _tryGetUser();

        return user != null
            ? AuthenticationState.authenticated(user)
            : const AuthenticationState.unkonwn();
      default:
        return const AuthenticationState.unkonwn();
    }
  }

  Future<User?> _tryGetUser() async {
    try {
      final user = await _userRepository.getUser();
      return user;
    } on Exception {
      return null;
    }
  }
}
```

# main.dart

```dart
import 'package:authentication_repository/authentication_repository.dart';
import 'package:bloc_login/app.dart';
import 'package:flutter/material.dart';
import 'package:user_repository/user_repository.dart';

void main() {
  runApp(App(
    authenticationRepository: AuthenticationRepository(),
    userRepository: UserRepository(),
  ));
}
```

## app.dart

```dart
class App extends StatelessWidget {
  final AuthenticationRepository authenticationRepository;
  final UserRepository userRepository;

  const App({
    Key? key,
    required this.authenticationRepository,
    required this.userRepository,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    /// `RepositoryProvider` 的功能是： 提供一个`AuthenticationRepository`单例，给后续的逻辑使用。
    return RepositoryProvider.value(
      value: authenticationRepository,
      child: BlocProvider(
        create: (_) => AuthenticationBloc(
          authenticationRepository: authenticationRepository,
          userRepository: userRepository,
        ),
        child: AppView(),
      ),
    );
  }
}
```

> `RepositoryProvider` 存储了一个`AuthenticationRepository`的单例，提供给`child`中使用，可以通过下面方式获取这个单例：

```dart
AuthenticationRepository authenticationRepository = RepositoryProvider.of<AuthenticationRepository>(context);
```

在`LoginPage`中，用到了这个单例。

## AppView

```dart
class AppView extends StatefulWidget {
  @override
  _AppViewState createState() => _AppViewState();
}

class _AppViewState extends State<AppView> {
  final _navigatorKey = GlobalKey<NavigatorState>();
  NavigatorState get _navigator => _navigatorKey.currentState!;

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      navigatorKey: _navigatorKey,
      onGenerateRoute: (settings) => SplashPage.route(),
      builder: (context, child) {
        return BlocListener<AuthenticationBloc, AuthenticationState>(
          child: child,
          listener: (context, state) {
            /// 通过 `State`状态去渲染展示层
            switch (state.status) {
              case AuthenticationStatus.authenticated:
                _navigator.pushAndRemoveUntil(
                  HomePage.route(),
                  (route) => false,
                );
                break;
              case AuthenticationStatus.unauthenticated:
                _navigator.pushAndRemoveUntil(
                  LoginPage.route(),
                  (route) => false,
                );
                break;
              default:
                break;
            }
          },
        );
      }, // builder
    );
  }
}
```

`AppView`是一个`StatefulWidget`，因为它需要通过`GlobalKey`来获取`NavigatorState`，然后进行导航逻辑处理。

# login

## bloc

<img src="/assets/images/tutorial/state/02.png"/>

### login_event.dart

* `LoginUsernameChanged`: 用户名更改。
* `LoginPasswordChanged`: 密码更改。
* `LoginSubmitted`: 提交Form。

```dart
part of 'login_bloc.dart';

abstract class LoginEvent extends Equatable {
  const LoginEvent();

  @override
  List<Object> get props => [];
}

// LoginUsernameChanged: notifies the bloc that the username has been modified.
class LoginUsernameChanged extends LoginEvent {
  final String username;

  const LoginUsernameChanged(this.username);

  @override
  List<Object> get props => [username];
}

// LoginPasswordChanged: notifies the bloc that the password has been modified.
class LoginPasswordChanged extends LoginEvent {
  final String password;

  const LoginPasswordChanged(this.password);

  @override
  List<Object> get props => [password];
}

// LoginSubmitted: notifies the bloc that the form has been submitted.
class LoginSubmitted extends LoginEvent {
  const LoginSubmitted();
}
```

### login_state.dart

`LoginState` 负责管理 用户名、密码的输入 `State`，

```dart
part of 'login_bloc.dart';

class LoginState extends Equatable {
  final FormzStatus status;
  final Username username;
  final Password password;

  const LoginState({
    this.status = FormzStatus.pure,
    this.username = const Username.pure(),
    this.password = const Password.pure(),
  });

  LoginState copyWith(
    FormzStatus? status,
    Username? username,
    Password? password,
  ) =>
      LoginState(
        status: status ?? this.status,
        username: username ?? this.username,
        password: password ?? this.password,
      );

  @override
  List<Object> get props => [status, username, password];
}
```

### login_bloc.dart

```dart
import 'dart:async';

import 'package:authentication_repository/authentication_repository.dart';
import 'package:bloc/bloc.dart';
import 'package:bloc_login/login/login.dart';
import 'package:equatable/equatable.dart';
import 'package:formz/formz.dart';

part 'login_event.dart';
part 'login_state.dart';

class LoginBloc extends Bloc<LoginEvent, LoginState> {
  final AuthenticationRepository _authenticationRepository;

  LoginBloc({required AuthenticationRepository authenticationRepository})
      : _authenticationRepository = authenticationRepository,
        super(LoginState());

  @override
  Stream<LoginState> mapEventToState(LoginEvent event) async* {
    if (event is LoginUsernameChanged) {
      yield mapEventUsernameChangedToState(event, state);
    } else if (event is LoginPasswordChanged) {
      yield mapEventPasswordChangedToState(event, state);
    } else if (event is LoginSubmitted) {
      yield* mapEventSubmittedToState(event, state);
    }
  }

  /// 用户名更改对应的State逻辑
  LoginState mapEventUsernameChangedToState(
      LoginUsernameChanged event, LoginState state) {
    final username = Username.dirty(event.username);

    return state.copyWith(
      status: Formz.validate([username, state.password]),
      username: username,
    );
  }

  LoginState mapEventPasswordChangedToState(
      LoginPasswordChanged event, LoginState state) {
    final password = Password.dirty(event.password);

    return state.copyWith(
      status: Formz.validate([password, state.username]),
      password: password,
    );
  }

  Stream<LoginState> mapEventSubmittedToState(
      LoginSubmitted event, LoginState state) async* {
    if (state.status.isValid) {
      yield state.copyWith(status: FormzStatus.submissionInProgress);

      try {
        await _authenticationRepository.logIn(
          username: state.username.value,
          password: state.password.value,
        );

        yield state.copyWith(status: FormzStatus.submissionSuccess);
      } catch (e) {
        yield state.copyWith(status: FormzStatus.submissionFailure);
      }
    }
  }
}
```

* 初始化`State`是`pure`，表示 username password 都为空字符。
* `LoginBloc` 依赖了鉴权包`AuthenticationRepository`, 当Form表单点击了提交按钮后，Bloc 就会触发`Login`方法。
* 当 Form 中的 username password 值发生改变时， Bloc 会触发`Formz.validate`,对字段进行校验。

## view

### login_page.dart

```dart
import 'package:authentication_repository/authentication_repository.dart';
import 'package:bloc_login/login/login.dart';
import 'package:bloc_login/login/view/login_form.dart';
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

class LoginPage extends StatelessWidget {
  static Route route() => MaterialPageRoute(builder: (_) => LoginPage());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Login')),
      body: Padding(
        padding: EdgeInsets.all(12),
        child: BlocProvider(
          create: (_) => LoginBloc(
            authenticationRepository:
                RepositoryProvider.of<AuthenticationRepository>(context),
          ),
          child: LoginForm(),
        ),
      ),
    );
  }
}
```

### login_form.dart

```dart
import 'package:bloc_login/login/login.dart';
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';
import 'package:formz/formz.dart';

class LoginForm extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return BlocListener<LoginBloc, LoginState>(
      listener: (context, state) {
        if (state.status.isSubmissionFailure) {
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(
              SnackBar(content: Text('Authentication Failure')),
            );
        }
      },
      child: Align(
        alignment: Alignment(0, -1 / 3),
        child: Column(
          mainAxisSize: MainAxisSize.min,
          children: [
            _UsernameInput(),
            const Padding(padding: EdgeInsets.all(12)),
            _PasswordInput(),
            const Padding(padding: EdgeInsets.all(12)),
            _LoginButton(),
          ],
        ),
      ),
    );
  }
}

class _UsernameInput extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return BlocBuilder<LoginBloc, LoginState>(
      buildWhen: (pre, current) => pre.username != current.username,
      builder: (context, state) {
        return TextField(
          key: const Key('loginForm_usernameInput_textField'),
          onChanged: (username) {
            context.read<LoginBloc>().add(LoginUsernameChanged(username));
          },
          decoration: InputDecoration(
            labelText: 'username',
            errorText: state.username.invalid ? 'invalid username' : null,
          ),
        );
      },
    );
  }
}

class _PasswordInput extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return BlocBuilder<LoginBloc, LoginState>(
      buildWhen: (pre, current) => pre.password != current.password,
      builder: (context, state) {
        return TextField(
          key: const Key('loginForm_passwordInput_textField'),
          onChanged: (password) {
            context.read<LoginBloc>().add(LoginPasswordChanged(password));
          },
          decoration: InputDecoration(
            labelText: 'password',
            errorText: state.password.invalid ? 'invalid password' : null,
          ),
        );
      },
    );
  }
}

class _LoginButton extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return BlocBuilder<LoginBloc, LoginState>(
        buildWhen: (pre, cur) => pre.status != cur.status,
        builder: (context, state) {
          return state.status.isSubmissionInProgress
              ? const CircularProgressIndicator()
              : ElevatedButton(
                  key: const Key('loginForm_continue_raisedButton'),
                  child: Text('Login'),
                  onPressed: state.status.isValidated
                      ? () => context.read<LoginBloc>().add(LoginSubmitted())
                      : null,
                );
        });
  }
}
```

* `BlocListener`用于监控登录状态，如果登录失败`isSubmissionFailure`，则展示`SnackBar`给用户提示。
* 给每个`TextField`添加一个`BlocBuilder`，监控`State`来对 Widget Tree 进行重建。

# home

```dart
import 'package:bloc_login/authentication/authentication.dart';
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

class HomePage extends StatelessWidget {
  static Route route() => MaterialPageRoute(builder: (_) => HomePage());
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Home')),
      body: Center(
        child: Column(
          mainAxisSize: MainAxisSize.min,
          children: [
            Builder(
              builder: (BuildContext context) {
                final userId = context
                    .select((AuthenticationBloc bloc) => bloc.state.user.id);

                return Text('userId: $userId');
              },
            ),
            // 上下两种方式都可获取到 userId 的值。
            BlocBuilder<AuthenticationBloc, AuthenticationState>(
                builder: (context, state) {
              return Text('userId: ${state.user.id}');
            }),
            ElevatedButton(
                onPressed: () {
                  context
                      .read<AuthenticationBloc>()
                      .add(AuthenticationLogoutRequested());
                },
                child: Text('Logout')),
          ],
        ),
      ),
    );
  }
}
```

完整的代码：

```bash
git clone -b bloc_login https://gitee.com/flutter-slu/examples.git
cd examples/
git checkout d83f7146217fe283d6b9475e43614271f0776a3b
```