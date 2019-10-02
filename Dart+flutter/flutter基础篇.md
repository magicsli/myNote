# flutter 基础篇



## 准备

我们在创建一个flutter项目前需要做以下几部操作:  ( 以官方文档为准 )

- 1, 下载并安装配置`dart`的`SDK`
- 2, 下载并安装配置 `java`的`SDK` 

- 3, 下载并安装安卓模拟器 / 安卓SDK;
- 4, 在 vs Code 或者 Android Studio 上下载 dart / flutter 插件

- 5, 调试dart / flutter .  在命令行输入 flutter doctor 检测当前环境
- 6, 配置模拟器 / 真机, 如果是模拟器, 即将其端口配置到 vs code   --  Android Studio 自带模拟器, 不需要配置
  -  `nox_adb.exe connect 127.0.0.1:62001`		夜神模拟器的配置命令/ 在模拟器的lib目录下 运行
- 7, 开始调试



附:

​	flutter使用的是一套新的包管理工具已经命令行, 不要和node搞混:

​	flutter -h   查看此包工具

​	pub 谷歌的包管理工具  ( 笔者当前也不熟 )

​	**创建项目:** `flutter create flutter_demo`

​	**初始化项目:** `flutter packages get` 获取依赖包 / 会比较卡 = =我们有一堵墙

​	**调试项目:**`flutter run`   注意: 调试前必须连接到安卓/iOS设备,或者模拟器



**备注:**

|                            |                                                              |
| :------------------------- | :----------------------------------------------------------- |
| Flutter 常用命令           | 说明                                                         |
| `flutter`                  | 列出所有的命令                                               |
| `flutter help`             | 查看具体命令的帮助信息                                       |
| `flutter doctor`           | 查看是否还需要安装其它依赖                                   |
| `flutter doctor -v`        | 查看详细信息                                                 |
| `flutter channel`          | 查看 Flutter SDK 所有分支                                    |
| `flutter channel stable`   | 切换分支                                                     |
| `flutter upgrade`          | 升级 Flutter SDK（此命令会同时更新 Flutter SDK 和你的 Flutter 项目依赖包） |
| `flutter packages get`     | 获取项目所有的依赖包（只更新项目依赖包，不包括 Flutter SDK） |
| `flutter packages upgrade` | 获取项目所有依赖包的最新版本（只更新项目依赖包，不包括 Flutter SDK） |
| `flutter analyze`          | 分析项目代码                                                 |
| `flutter build apk`        | 打包为安卓的apk文件                                          |
| `flutter build ios`        | 打包问 ios 的 安装文件                                       |





## 目录结构

我们开发的代码都在`lib`目录下,  

配置信息文档: `pubspec.yaml` 

生成的文件存放于 `build` 目录下

`Android` 和`Ios` 文件分别对应`Android`和`ios`的配置文件, 暂时我们用处理. 



**入口文件 `main.dart`**:

​	首先我们需要导入系统自带的核心包:   `import 'package:flutter/material.dart'`

​	我们需要在此入口文件中使用`runApp()` 函数开启一个flutter应用;

​	其中需要传入一个`widget` 作为中应用界面入口;

​	在我们widget中需注意, 我们的属性都有明确的数据格式定义, 即使我们只想放一行文本, 我们也需要使用`Text( 'something text' )`	这样进行包裹

​	在flutter中, 我们如果需要为widget添加样式, 不能想css那样添加, 我们需要通过定义好的类进行补充; 如:

`Style( color: Color.fromRGBO( 23, 51, 23, 0.6 ) );`





例:

```dart
import 'package:flutter/material.dart';
void main {
    runApp(Myapp);
}

class Myapp extends statelesswidget {
    @override  // 表示从抽象类中定义的必填参数
    Widget build ( BuildContext context ) {	 // 生成widget的方法
        return new  MaterialApp (		// 调用app材质文件 ( 固定参数,作为项目的基础包 )
        	title: 'magicsli'  			// app 名 ( 非常重要 )
            home: Scaffold (			// Scaffold  脚手架包, 其中有已经定义好的功能和widget
                	appBar: AppBar(		// 设置顶部导航栏
                    	title: Text('this is my frist app'),	// 设置顶部标题
                    ),
                	body: Center(		// 在内容部分传入一个居中的widget盒子
                    	child: Text( 'something text' )	 // 设置一个居中的文本	
                    )
            )
        )			
    }
    
    
}
```











## 组件

​	组件分为两种:  有状态组件和无状态组件:

- `statelesswidget`  无状态组件    -- 状态不可变 ( 静态组件, 类似与react的函数式组件 ) --
- `statefulwidght`    有状态组件   -- 持有状态可能会在`widght` 生命周期发生变化 --



我们创建的所有自定义组件都必须继承于这两个类,  继承后都必须传入一个必要方法, `build`

我们将在这方法的返回参数中返回新的`widget`, 类似于`react`中的`render`方法. 二者比较相近

​	例:

```dart
class About extends statelesswidget {
    
    @override
    Widget build () {
        return 
    }
}
```







在flutter中所有组件都是一个类,我们定义的所有属性, 样式,布局容器等都需要在类中进行包裹, 属于类包类的写法. 

这一点和我们前端中的语法有比较大的差异.  在前端中我们将 HTML,  JS , CSS 都进行了分离.  我们只需要在js区域

写逻辑代码. 但是在flutter中由于我们都是用一个类包裹.所以样式可能会和布局内容写在一起. 





## 列表渲染

我们可以使用独立方法进行动态列表渲染; 写法类似与react的jsx语法

​	例:

```dart
List<widget> _getData () {
    List<widget> dataList = new List();
    for ( var i = 1; i < 10; i++ ){
        dataList.add( ListTile(
        	title: Text( '这是第$i行列表' ),
            leading: Image.network('https://www.magicsli.com?***示例图片.png')
        ) );
    };
    return dataList
}

ListView(
	children: this._getData(),
)
```





如果传入的不是一个数组, 我们就需要将其转化为数组: ` return ` dataList.toList()



**使用`Listview.builder()`进行列表渲染**

```dart

List data = [ // 虚拟数据
    {
        title: '示例标题',
        imgUrl: 'https://www.magicsli.com?***示例图片.png'
    }
]

return ListView.builder(
	itemCount: this.data.length,
    itemBuilder: ( context, index) {
        return ListTile(
       		title: Text(this.data[index]['title']),
            leading: Image.network( this.data[index]['imgUrl'] )
        )
    }
)
```





## 网格布局 GridView

```dart
GridView.count(
	crossAxisCount: 3,			// 分为三列
    children: <widget>[]		// 传入一个数组
)
```

