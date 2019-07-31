### dart

**简章**: dart源自于谷歌, 旗下的flutter是当前最火热的原生app开发技术栈.所需要开发fluuter必须能掌握dart;   而dart是一个独立的编程语言. 需重学

###  变量

+ 变量 `var int String `  其中 var可自动定位其类型, 与js一样. 会自动判断当前变量的数据类型

+ 常亮 `final   const` 

  + 附: final 的值初始化在代码第一次运行前, 即就你可以用函数啊, 这些不确定的数据, 但`const`的值在定义时就需要确定. 它不能用于接受函数返回值之类不确定因素的数据

    

    

### 数据类型

共有 ` String, List, Maps, int, double....` 



#### **字符串**: ( String )

```dart
 var str = "hello word";

 String str1 = 'hello word';

 String str2 = "hello word";

 String str3  = ''' hello word,

  我是第二行文本	 '''		//可显示多行文本
    
 String str4 = """ Hello word 
  					我也是多行文本
 				"""			// 可显示多行文本
    
   ------ 字符串拼接 ------
    print("$str1 $str2"); // 利用$在字符串中插入变量
    print("${this.name}好"); // 利用 ${ } ( 类似es6的模板字符串 )
    print( str1 + str2 ); // 利用 + 号进行字符串拼接
```



#### **数字**:    ( int, double )

```dart
var num = 1223;
int num1 = 1223;	// 整数型
double num2 = 1223; // 浮点 / 小数型 ( 定义的变量会带小数点...默认携带一位小数 )

---- 运算符 ----
    + - * / %    ~/ ( 取整 )
    // 附: 如 ( 12 ~/ 5 ) = 2; 除后取整()
    
```



#### boolean ( ture false )

```dart
使用与js无异, 但有一点, 在执行if等判断语句时, 不会进行数据类型转化, 所以 123 != "123"
```



#### List ( 数组 )

```dart
var arr = [1, 2, 3, 5];
var arr1 = new List();
var arr2 = new List<String>(); // 要求里面的值必须是字符串类型  
```



#### Maps ( 对象 )

```dart
var a = new Map();
var a1 = {
    "a" : "12345",
    "b": "456"
};  // 键名必须带双引号
```



#### 功能 ( 函数 ) function

```dart 
// 返回类型 方法名 () {

// }

int mg_getInt (  ) {
    return int.parse( "123" )
}

// 参数 int mg_getInt( String temp ) {

// }

// 可选参数 int mg_getInt( String temp, [ int temp2 ] ) {

// }

// 默认参数 int mg_getInt ( String temp = "123456", [ int temp2 ] ) {
	
// }

// 命名参数 int mg_getInt ( String temp = "123456", { String temp2 } ) {

// }

// 调用命名参数类型的函数 mg_getInte( "12", temp2:"我是谁,你是谁" )


```



#### 类 ( class  )

```dart
// 在dart没有构造函数的说法, 我们通过class来创建对象, 并实现面向对象化开发

// 创建一个继承自 People 的 Person 类
class Person extends People {
    String name;
    int age;
    
    // 默认构造函数的简写
    Person( String name, String age ) : super( name, age ) {
        this.name = name;
		this.age = age;
    }
    
    // 静态方法
    static call () {
        print( "打电话给xxx" )
    }
    
    // 命名构造函数
    Person.now() {
        print('我是命名构造函数');
    }
    
    // 定义命名构造方法
    Person.like(String love, String hate) {
        this.love = love;
		this.hate = hate;
    }
    
    // 私有属性, 私有属性必须要在独立文件; 带以下划线开头的方法或属性就是私有的, 外部不能调用(类似局部作用域)
    String _name = "123456";
    
    
    void sayHi ( ) {
        print('hello, word');
        print( "${ this.name } love ${ this.love }; and... i hate ${ this.hate } " )
    }
}
	// get set 




// 运算操作符 ? is as ..

// ? 如:  Person a;  a?.sayHi() --- 如果a不为空就 调用a的sayHi方法
// is 判断类型  if( a is Person ) 判断数据类型
// as 若: var a; a = "";   a = new Person( "张三", '45' ); 这时候就需要将a确定数据类型并且进行操作;  ( a as Person ).call();
// .. 级联操作符
/*
		Person a = new Person( "张三", "45" );
		a.sayHi();
		a.name = "老王";
		a.sayHi();
		
	简写为:   
		Person a = new Person( "张三", "45" );
		   a..sayHi()
			..name="老王"
			..sayHi();

*/


// 抽象类
	// ( 抽象类中的方法一定要有定义 )
abstract class Animal {	// 这就是一个抽象类, 抽象类没法直接实例化
    eat();
    run();
    printInfo() {
        print('我是一个抽象类里面的普通方法');
    }
}

class Dog extends Animal {
    @override
    eat () {	// 如果不定义这个方法, 则会报错
        print("小狗在吃骨头");  
    }
}


/*
	Dart抽象类, Dart抽象类主要用于定义标准, 子类可以继承抽象类, 也可以实现抽象类接口.

        1, 抽象类通过abstract 关键字来定义

        2, Dart中的抽象方法不能用abstract声明, Dart中没有方法体的方法我们称为抽象方法.

        3, 如果子类继承抽象类必须得实现里面的抽象方法

        4, 如果把抽象类当做接口的话必须的实现抽象类中的所有属性和方法

        5, 抽象类不能被实例化, 只有继承它的子类可以
	
	
	extends抽象类 和 implements的区别:
	
		1, 如果要复用抽象类中的方法, 并且要用抽象方法约束子类的话我们就用extends继承抽象类
		
		2, 如果只是把抽象类当做标准的话我们就用implements实现抽象类
	


*/



/*
	mixins
		1, 作为mixins的类只能继承自Object, 不能继承其他类
		2, 作为mixins的类不能用有构造函数, 
		3, 一个类可以mixins多个mixins类
		4, mixins绝不是继承, 也不是接口, 而是一种全新的特性
		
	mixins使用 with 关键字进行操作:
	
		class A {
			String ingo = "123456";
			
		}
		
		class B {
			String add = "addEvent";
		}
		
		class c with A,b {
			
		}
		
		
		此时 c 就获得了 A,Bd的属性
	
		
*/

```





#### 泛型

```dart
class Public_people <T> {
    // 泛型代表不定义传入参数, 当用户生成新的工具对象时, 可位此类定义一个类型
}
```



#### 库

​	在Dart中, 有三类库:

+ 1, 自定义库:` import "./lib/Person.dart"`
+ 2, Dart自带库: `import "dart:math"`
+ 3, Pub包管理系统中的库: 
  + `https://pub.dev/packages`
  + `https://pub.flutter-io.cn/packages`
  + `https://pub.dartlang.org/flutter/`
  + 操作:
    + 1, 需要在自己的项目根目录新建一个`pubspec.yaml`
    + 2, 在`pubspec.yaml`文件 然后配置名称, 描述, 依赖等信息
    + 3, 然后运行 `pub get` 获取包下载到本地
    + 4, 项目中引入库 `import 'package:http/http.dart' as http` 看文档使用





**重命名:**

​	`import 'package/lib/lib.dart' as lib`

===>  将这个包重命名为lib   <===



**部分导入:**
	如果只需要导入库的一部分, 有两种模式:

+ 模式一: 只导入需要的部分, 使用show关键字, 如下例子所示:

​		`import 'package:lib1/lib1.dart' show foo;`


+ 模式二: 隐藏不需要的部分, 使用hide关键字, 如下例子所示:

  `import 'package:lib2/lib2.dart' hide foo;`