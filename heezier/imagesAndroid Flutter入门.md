# Android Flutter入门

## 一、搭建Flutter环境

Flutter官网： https://flutterchina.club/ 

windows环境搭建过程

1. 由于在国内访问Flutter有时可能会受到限制，为了能正常获取Flutter SDK以及之后第一次执行 flutter doctor 能够正常完成，可以先添加镜像地址，Flutter官方为中国开发者搭建了临时镜像。

   环境变量加入到用户环境变量中：

```
export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
```

或者：

![1595225032715](C:\Users\turing\Desktop\img\typora-user-images\1595225032715.png)



![1595225043271](C:\Users\turing\Desktop\img\typora-user-images\1595225043271.png)





2.[下载Flutter SDK](https://flutter.io/sdk-archive/#windows)

如果下载慢无法下载可以使用git下载：

```
 git clone -b beta https:*//github.com/flutter/flutter.git
```

3.将安装包zip解压到你想安装Flutter SDK的路径 ，即为你的Flutter安装目录

4.在Flutter安装目录的`flutter`文件下找到`flutter_console.bat`，双击运行并启动**flutter命令行** 

![1594956092871](C:\Users\turing\Desktop\img\typora-user-images\1594956092871.png)

5.打开一个新的命令提示符或PowerShell窗口并运行以下命令以查看是否需要安装任何依赖项来完成安装： 

运行 flutter doctor，第一次运行有点慢，需要点等待时间

 flutter doctor： 下载它自己的依赖项并自行编译 

![1594957325718](C:\Users\turing\Desktop\img\typora-user-images\1594957325718.png)

6.Android Studio安装flutter插件，重启

![1594957469700](C:\Users\turing\Desktop\img\typora-user-images\1594957469700.png)



![1594957513096](C:\Users\turing\Desktop\img\typora-user-images\1594957513096.png)

到此说明flutter环境已经搭建完成

## 二、新建Flutter工程

如果首次创建项目如果一直卡在Creating Flutter project上，先打开项目文件，如果里面已经有了创建的文件，那么从任务管理器关掉Android Studio,然后重新打开，点击Open an existing Android Studio project,找到项目文件，打开就行了。
————————————————
版权声明：本文为CSDN博主「非典型废言」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/sinat_35821976/article/details/87454911

![1594957559893](C:\Users\turing\Desktop\img\typora-user-images\1594957513096.png)

工程的目录结构：

![1594967329016](C:\Users\turing\Desktop\img\typora-user-images\1594967329016.png)

官方文档中：

 在这个示例中，你将主要编辑Dart代码所在的 **lib/main.dart** 文件,

我们可以修改main.dart文件来实现简单的信息修改。

我们先运行看一下效果：

![1594967413771](C:\Users\turing\Desktop\img\typora-user-images\1594967413771.png)

## 三、热重载

看一下main.dart文件

```
class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        // This is the theme of your application.
        //
        // Try running your application with "flutter run". You'll see the
        // application has a blue toolbar. Then, without quitting the app, try
        // changing the primarySwatch below to Colors.green and then invoke
        // "hot reload" (press "r" in the console where you ran "flutter run",
        // or simply save your changes to "hot reload" in a Flutter IDE).
        // Notice that the counter didn't reset back to zero; the application
        // is not restarted.
        primarySwatch: Colors.green,
        // This makes the visual density adapt to the platform that you run
        // the app on. For desktop platforms, the controls will be smaller and
        // closer together (more dense) than on mobile platforms.
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}
```

注释中提示我们可以改变

primarySwatch: Colors.green,来修改app的主题颜色，我们来试着修改颜色并体验 热重载



![1594967682076](C:\Users\turing\Desktop\img\typora-user-images\1594967682076.png)

反应很快，日志显示1122ms完成了热重载。

## 四、使用外部包(package)

我们参考官网提供的步骤，使用 english_words 开源软件包 

 flutter一些开源的软件包：https://pub.dev/flutter/packages 

 1.pubspec文件管理Flutter应用程序的assets(资源，如图片、package等) ，所以我们可以到 pubspec.yaml 添加package的依赖

![1594968118124](C:\Users\turing\Desktop\img\typora-user-images\1594968118124.png)

2. 单击右上角的 **Packages get**，这会将依赖包安装到您的项目。您可以在控制台中看到以下内容： 

   ![1594968242387](C:\Users\turing\Desktop\img\typora-user-images\1594968242387.png)

3. **lib/main.dart** 中, 引入 `english_words` 

```
import 'package:flutter/material.dart';
import 'package:english_words/english_words.dart';
```

4.使用词库

![1594968486519](C:\Users\turing\Desktop\img\typora-user-images\1594968486519.png)



此时假如package，热更新会报错，所以需要先停止运行，在运行

之后每一次热更新，MyHomePage的title都会随机出现一个单词。

以上主要是记录软件包package的使用



## 五、页面跳转

 Flutter的路由和导航功能 ，管理多个页面时有两个核心概念和类：[Route](https://docs.flutter.io/flutter/widgets/Route-class.html)和 [Navigator](https://docs.flutter.io/flutter/widgets/Navigator-class.html)。 一个route是一个屏幕或页面的抽象，Navigator是管理route的Widget。Navigator可以通过route入栈和出栈来实现页面之间的跳转。 

### 1.简单的页面跳转

我们先实现简单的页面跳转，可以用 Navigator.push 和 Navigator.pop 实现

1.新建一个page，新建newpage.dart文件，继承StatelessWidget，可以看到需要复写createState

如果不复写，那么只能抽象，或者noSuchMethod，一会能跳转了我们可以验证一下noSuchMethod是什么意思。

![1594969991861](C:\Users\turing\Desktop\img\typora-user-images\1594969991861.png)

在页面显示一串Text，并定义onPressed动作的事件，使用pop返回到上一页

```dart
   @override
  Widget build(BuildContext context) {
    return Scaffold(appBar: AppBar(title: Text('New page'),),
      body: Center(child: RaisedButton(
          child: Text('点击返回上一页'),
          onPressed: () {
            Navigator.pop(context);
          }),),);
  }

```

2.main.dart找到悬浮按钮的点击事件，删除setState，添加跳转动作

```dart
  void _incrementCounter() {
     Navigator.push(context,
        MaterialPageRoute(builder: (context) => Newpage()));
  }

```

3.热重载，查看并点击悬浮按钮，跳转到了第二个页面，点击可以返回到上一页

![1595212566594](C:\Users\turing\Desktop\img\typora-user-images\1595212566594.png)

### 2.通过routes路径方式跳转

 创建 `MaterialApp` 时可以指定 `routes` 参数，该参数是一个映射路由名称和构造器的 Map。 

```
 return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.green,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      routes: {
        "home": (context) => MyHomePage(),
        "newpage": (context) => Newpage()
      },
      home: MyHomePage(title: wordPair.asPascalCase),
    );
```

跳转直接使用Navigator.pushNamed(context, "newpage");

```
Navigator.pushNamed(context, "newpage");
```



### 3.传递数据到下一个页面

传递的方式有两种:

- 在构造方法中传递数据
- 在Route中传递数据给下一个页面

分别来使用一下两种方式

第一种：在跳转的时候将参数传入，在接受页面使用ModalRoute.of(context).settings.arguments获取

```
class User {
  String name;
  int age;

  String toString(){
    return ("name:" + this.name + " age:" + this.age.toString());
  }
  User({this.name, this.age});
}



void startNewPage() {
//     Navigator.push(context,
//        MaterialPageRoute(builder: (context) => Newpage()));

//     Navigator.pushNamed(context, "newpage");
  
     Navigator.pushNamed(context, "newpage", arguments: User(name: "GodV",age: 23));
     
  }
```

接受数据， ModalRoute.of(context).settings.arguments;方式获取传递的数据 

```
@override
  Widget build(BuildContext context) {
    //构造获取传递过来的参数user
    final User user = ModalRoute.of(context).settings.arguments;
    return Scaffold(appBar: AppBar(title: Text("第二页"),),
      body: Center(child: RaisedButton(
          child: Text('传递的参数：' + user.toString()),
          onPressed: () {
            Navigator.pop(context);
          }),),);
  }

```

第二种： onGenerateRoute定义了返回的目标页面需要带有参数，另外目标页面写构造参数 

```
 return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.green,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      routes: {
        "home": (context) => MyHomePage(),
      },
      onGenerateRoute: (settings) {
        if (settings.name == "newpage") {
          final User args = settings.arguments;
          return MaterialPageRoute(builder: (context) {
            return Newpage(
              user: args,
            );
          });
        }
      },
      home: MyHomePage(title: wordPair.asPascalCase),
    );
```

 发送数据的方法没有改变：

```
 Navigator.pushNamed(context, "newpage", arguments: User(name: "Zgg01",age: 23));
```

接受页面：

```
  final User user;
  Newpage({this.user});
  
  @override
  Widget build(BuildContext context) {
    //构造获取传递过来的参数user
    return Scaffold(appBar: AppBar(title: Text("第二页"),),
      body: Center(child: RaisedButton(
          child: Text('传递的参数：' + user.toString()),
          onPressed: () {
            Navigator.pop(context);
          }),),);
  }
```

### 4.接收页面返回值

定义接受值显示在Text上

```
   String reciveString = "接受的值：";
  
  children: <Widget>[
            Text(
              '路由跳转',
            ),
            Text(
              '$reciveString',
//              style: Theme.of(context).textTheme.headline4,
            ),
          ],
```

打开页面时使用then接受返回回来的参数，**需要使用setState来更新组件的值**

```
         Navigator.pushNamed(context, "newpage", arguments: User(name: "Zgg01",age: 23))
              .then((value) => {
                 setState(() {
                   reciveString = value.toString();
                  })
               });

```

在第二个页面发送需要返回的值

```
  @override
  Widget build(BuildContext context) {
    //构造获取传递过来的参数user
    return Scaffold(appBar: AppBar(title: Text("第二页"),),
      body: Center(child: RaisedButton(
          child: Text('传递的参数：' + user.toString()),
          onPressed: () {
            Navigator.pop(context, User(name: "Forever",age: 20));
          }),),);
  }
```

 第二个页面点击返回后效果：

![1595229311210](C:\Users\turing\Desktop\img\typora-user-images\1595229311210.png)





## 六、添加一个 **有状态的部件**（Stateful widget）

**部件** 分为状态可变的和状态不可变的

State*less* widgets 是不可变的, 这意味着它们的属性不能改变 - 所有的值都是最终的.

State*ful* widgets 持有的状态可能在widget生命周期中发生变化. 实现一个 stateful widget 至少需要两个类:

1. 一个 StatefulWidget类。
2. 一个 State类。 StatefulWidget类本身是不变的，但是 State类在widget生命周期中始终存在.

以官网的添加一个ListView为例

第一步：定义一个Page继承StatefulWidget

```
class ListPage extends StatefulWidget {
  final String title;
  ListPage({Key key, this.title}) : super(key: key);
  @override
  State<StatefulWidget> createState() {
     return ListWordsState();
  }
}

```

第二步：定义ListView页面，定义ListWordsState继承State<ListPage>

```
class ListWordsState extends State<ListPage>{
  final _suggestions = <WordPair>[];
  final _biggerFont = const TextStyle(fontSize: 18.0);
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("ListView"),),
      body: new ListView.builder(
          padding: const EdgeInsets.all(16.0),
          // 对于每个建议的单词对都会调用一次itemBuilder，然后将单词对添加到ListTile行中
          // 在偶数行，该函数会为单词对添加一个ListTile row.
          // 在奇数行，该函数会添加一个分割线widget，来分隔相邻的词对。
          // 注意，在小屏幕上，分割线看起来可能比较吃力。
          itemBuilder: (context, i) {
            // 在每一列之前，添加一个1像素高的分隔线widget
            if (i.isOdd) return new Divider();

            // 语法 "i ~/ 2" 表示i除以2，但返回值是整形（向下取整），比如i为：1, 2, 3, 4, 5
            // 时，结果为0, 1, 1, 2, 2， 这可以计算出ListView中减去分隔线后的实际单词对数量
            final index = i ~/ 2;
            // 如果是建议列表中最后一个单词对
            if (index >= _suggestions.length) {
              // ...接着再生成10个单词对，然后添加到建议列表
              _suggestions.addAll(generateWordPairs().take(10));
            }
            return _buildRow(_suggestions[index]);
          }
       ),
    );
  }

  //生成每一个Item的TextView
  Widget _buildRow(WordPair pair) {
    return new ListTile(
      title: new Text(
        pair.asPascalCase,
        style: _biggerFont,
      ),
    );
  }

}
```

注意：复写Widget build(BuildContext context)时，需要return一个以Scaffold为根布局的组件，之后再body里面定义ListView

**padding：**即对应Android的padding，可以使用all修改全部的内边距，或者使用fromLTRB定义每一个方向的内边距

```

  const EdgeInsets.all(double value)
    : left = value,
      top = value,
      right = value,
      bottom = value;
      
      
const EdgeInsets.fromLTRB(this.left, this.top, this.right, this.bottom);
```

 **itemBuilder: (context, i)**：生成item时的遍历

**_buildRow**：定义每一个Item的内容

第三步：添加交互

点击收藏，显示收藏图标

1.添加一个 _saved Set(集合) 到RandomWordsState

```
class ListWordsState extends State<ListPage>{
  final _suggestions = <WordPair>[];
  final _biggerFont = const TextStyle(fontSize: 18.0);
  //添加一个 _saved Set(集合) 到RandomWordsState
  final _saved = new Set<WordPair>();
 }
```

2. 在 `_buildRow` 方法中添加 `alreadySaved`来检查确保单词对还没有添加到收藏夹中。 
3.  定义trailing: new Icon图标，通过alreadySaved状态来设置颜色
4. 定义onTap方法，更新对应item的收藏状态

```
Widget _buildRow(WordPair pair) {
    final alreadySaved = _saved.contains(pair);

    return new ListTile(
      title: new Text(
        pair.asPascalCase,
        style: _biggerFont,
      ),
      trailing: new Icon(
        alreadySaved ? Icons.favorite : Icons.favorite_border,
        color: alreadySaved ? Colors.red : null,
      ),
      onTap: () {
        setState(() {
          if (alreadySaved) {
            _saved.remove(pair);
          } else {
            _saved.add(pair);
          }
        });
      },
    );
  }
```

效果：

![1595237316272](C:\Users\turing\Desktop\img\typora-user-images\1595237316272.png)

关于Flutter和Android对应的Api可以参考： [https://flutterchina.club/flutter-for-android/#flutter%E5%92%8Candroid%E4%B8%AD%E7%9A%84view](https://flutterchina.club/flutter-for-android/#flutter和android中的view) 

 以上Demo GitHub地址： https://github.com/heezier/Flutter 



参考：

[Flutter中文官网]( https://flutterchina.club/get-started/codelab/ )

[Flutter + Tensorflow Lite环境配置](https://blog.csdn.net/sinat_35821976/article/details/87454911)

