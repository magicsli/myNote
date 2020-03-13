## TypeScript

序: 学习前需要拥有js基础, 最好也有dart基础

数据类型: 

​	基本于js一致, 但是在定义时稍有不同

布尔值:

`let bool: boolean  = true;`



数字:

`let sum: number = 6;`

也支持es6中提出的*Unicode*编码:	

`let picre:number = 0xf00;	`



字符串:

```typescript
let name: string = "我是一条字符串";

let str: string = `${domain}是一个字符串`;

let num: number = 45;

// 多行字符串
let code = `${domain} 是一个可换行的

字符串, ` + num + `对吧`
```



数组: 

```typescript
let list: number[] = [ 1, 2, 3 ];

// 或者使用泛型写法: 这点与flutter有几分相似
let list: Array<number> = [ 1, 2, 3 ]

// 二者都是定义一个内部元素为数字的数组变量
```



元组: 

元组在某些方面与数组并无不同, 元组相对于数组的强类型定义稍宽松, 只需要符合其定义的所允许格式即可

```typescript
let x: [string, number];	// 定义了一个内部元素格式为string 与 number的元组
// 按照所定义格式赋值, ( 因为 0下标与 1下标已经被定义了, 需要符合其格式定义 )
x = ['hello', 10]		// ok

// 未按照其定义时的格式	( 0, 1下标未按照标准格式赋值 )
x = [10, 'hello'] 		// error

```

当访问一个已知索引的元组元素时:

```typescript
console.log( x[0].substr(1) );	// ok
console.log( x[1].substr(1) );	// error 第二位被定义为数字, 没有substr方法
```

当访问的是一个未定义下标类型的元素时, 会使用联合类型进行替代:

```typescript
x[3] = 'word';	// 下标3没有进行定义, 即会在符合0, 1的任一个格式下进行赋值

console.log( x[5].toString() ); // ok 预先定义的字符格式和数字格式都有toString

x[6] = true; // error boolean并没有在元组类型中进行定义;
```



枚举: 

enum 类型是对js标准数据类型的一个补充, 像c#等其他数据类型一样, 枚举可以为一组数据中赋予名字

类型于: 使用中文排序时, 因为我们的unincode编码不能进行排序, 即我们可以使用枚举类型为其定义顺序

```typescript
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
```

默认以0开始编号, 当然也可以