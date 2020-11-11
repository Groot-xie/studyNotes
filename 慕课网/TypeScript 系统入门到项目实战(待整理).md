# 一、环境

```npm
// 得到 `tsc` 命令行
npm i typescript -g
```

```npm
tsc index.ts
tsc -w // 监控ts文件变化
```

ts ---> 编译为js ---> 正常运行，简化这个过程的包 `ts-node`

```npm
// 得到 `ts-node` 命令行
npm i ts-node -g
// 直接执行ts文件
ts-node index.ts
```

监听

`nodemon index.ts`



# 二、类型

## 2.1 静态类型

+ 基础类型

  ```tsx
  // 基础类型 null undefined symbol boolean number void any
  const count: number = 123;
  const LeacherName: string = 'Dell'
  ```

  + any

    任意类型
    
  + void

    某种程度上来说，`void` 类型像是与 `any `类型相反，<font color=red> 它表示没有任何类型 </font>。 当一个函数没有返回值时，你通常会见到其返回值类型是 `void`

    声明一个`void`类型的变量没有什么大用，因为你只能为它赋予 `undefined` 和 `null`

  + Undefind null

    `undefined` 和 `null` 两者各自有自己的类型分别叫做 `undefined` 和 `null`。 和  `void` 相似，它们的本身的类型用处不是很大

    + <font color=red> 默认情况下`null`和`undefined`是所有类型的子类型 </font>。 就是说你可以把  `null` 和 `undefined` 赋值给 `number` 类型的变量
    + 然而，当你指定了<font color=red>  `--strictNullChecks` </font> 标记，`null` 和 `undefined` 只能赋值给 `void` 和它们各自

  + never

    `never` 类型<font color=red> 表示的是那些永不存在的值的类型 </font>。 

    `never` 类型是任何类型的子类型，也可以赋值给任何类型；然而，没有类型是 `never` 的子类型或可以赋值给 `never` 类型（除了 `never` 本身之外）, 即使  `any` 也不可以赋值给 `never`。

    ```js
    // 返回never的函数必须存在无法达到的终点
    function error(message: string): never {
      throw new Error(message)
    }
    function loop(): never {
      while(true) {}
    }
    
    // 推断的返回值类型为never
    function fail() {
      return error('Something failed')
    }
    ```

+ 对象类型

  `object` 表示<font color=red> 非原始类型 </font>，也就是除 `number`，`string`，`boolean`，`symbol`，`null` 或 `undefined` 之外的类型

  ```tsx
  // 对象类型-对象 {} class function []
  const teacher: {
      name: string;
      age: number;
  } = {
      name: 'dell',
      age: 18
  }
  // 对象类型-数组
  const numbers: number[] = [1, 2, 3]
  // 对象类型-类
  class Person {}
  const dell: Person = new Person()
  // 对象类型-函数
  // 一般情况下，函数参数需要声明类型，而返回值可以通过类型推断
  const getTotal: (a: number) => number = () => {
      return 123
  }
  ```

+ Date 类型

  ```tsx
  const date = new Date()
  // 相当于
  const date: Date = new Date()
  ```

## 2.2 类型断言

当你在TypeScript里使用JSX时，只有 `as`语法断言是被允许的。

```js
// 尖括号 语法
let someValue: any = 'this is a string'
let strLength: number = (<string>someValue).length
// as 语法
let strLength2: number = (someValue as string).length
```

## 2.3 类型注解

显示的告诉 typescript 变量的类型

```tsx
let count: number
```

## 2.4 类型推断

ts 会自动分析变量类型

```tsx
// 没有显示的声明abc为number型,ts根据你赋值123推断出abc为number型
let abc = 123
```

+ ts 能够自动分析变量类型，我们就不需要显示的声明
+ ts无法分析变量类型，需要使用类型注解

## 2.5 函数类型注解

```tsx
function add (first: number, second: number): number {
    return first + second
}
// 返回类型：void 函数没有返回值
function sayHello(): void {
    console.log('hello')
}
// 返回类型：never 函数永远不能执行完
function errorEmitter(): never {
    while(true) {}
}
// 函数参数解构的声明类型方式
function add1({ first, second }: { first: number, second: number }): number {
    return first +  second
}
```

## 2.6 数组和元组的类型注解

+ 数组的类型注解

  ```js
  const arr: (number | string)[] = [1, '2', 3]
  const stringArr: string[] = ['a', 'b', 'c']
  const undefinedArr: undefined[] = [undefined]
  // 数组的每一项是一个对象，并且包含固定属性
  const objArr: {name: string, age: number}[] = [{
      name: 'xxh',
      age: 28
  }]
  ```

+ 数组泛型，Array\<T>

  ```js
  // 数组泛型，Array<元素类型>
  let list = Array<number> = [1, 2, 3]
  ```

+ ReadonlyArray\<T>类型

  `ReadonlyArray\<T>` 类型，它与 `Array\<T>` 相似，只是把所有可变方法去掉了，因此可以确保数组创建后再也不能被修改

  ```js
  let a: number[] = [1, 2, 3, 4]
  let ro: ReadonlyArray<number> = a
  // ro[0] = 2 // error
  // ro.push(5) // error
  // ro.length = 100 // error
  // a = ro // error
  // 就算把整个ReadonlyArray赋值到一个普通数组也是不可以的。 但是你可以用类型断言重写：
  a = ro as number[]
  ```

+ 类型别名 type

  ```js
  // 如果对象的属性多了以后，可读性很差，使用类型别名 type
  // type alias
  type User = {
      name: string,
      age: number
  }
  const objArr1: User[] = [{
      name: 'xxh',
      age: 28
  }]
  ```

+ 元组 tuple

  ```js
  // 场景：数组长度固定，并且每一项的类型也固定
  const teacherInfo: [string, string, number] = ['xxh', 'male', 18]
  const teacherList: [string, string, number][] = [
      ['xxh', '男', 27],
      ['zwh', '女', 20]
  ]
  ```





# 三、interface 接口

通用性的类型集合用 `interface` 表示

和类型别名 `type` 的区别

+ `interface` 只能代表对象或函数

  ```tsx
  interface Person {
      name: string
  }
  ```

+ `type` 类型别名

  ```
  type Person = string
  type Person = {
  	name: string
  }
  ```

+ 能用 `interface` 就不用 `type`

## 3.1 语法

+ 定义对象

  ```tsx
  interface Person {
      name: string; // 必有属性
      age?: number; // 可选属性
      readonly abc: string; // 只读, 不可修改
      [propName: string]: any; // 索引签名(字符串/数字)：属性名为字符串,值任意,兼容不确定属性
      say(): string; // say方法,返回值为string类型
  }
  ```

+ 定义函数

  ```tsx
  interface SayHi {
    // (参数): 返回值
    (word: string, num: number): string
  }
  // 函数的参数名不需要与接口里定义的名字相匹配
  const say: SayHi = (text) => {
      return text
  }
  ```

## 3.2 接口继承

```tsx
interface Person {
    name: string;
    age?: number;
    say(): string;
}

interface Teacher extends Person {
    teach(): string;
}

class User implements Teacher {
    name = 'xxh'
    say() {
        return 'say'
    }
    teach() {
        return 'teach'
    }
}
```

## 3.3 `class` 类应用接口

```tsx
interface Person {
    name: string;
    age?: number;
    say(): string;
}
// 类应用接口
class User implements Person {
    // 属性必须符合接口要求
    name = 'xxh'
    say() {
        return 'say'
    }
}
```

## 3.4 传对象字面量和变量的区别

```tsx
// 场景1：传对象字面量和变量的区别
interface Person {
    name: string;
}

const getPersonName = (person: Person): void => {
    console.log(person.name)
}
const person = {
    name: 'xxh',
    age: 18
}
// 变量传递：多了一个age属性不报错
getPersonName(person)
// 字面量传递：多了一个age报错, ts进行了强校验
getPersonName({
    name: 'xxh',
    age: 18
})
```





# 四、类

## 4.1 访问类型

+ `public`

  允许在类外/类外被调用

  ```tsx
  class Person {
      // 相当于 public name = 'xxhh'
      name = 'xxhh'
      sayHi() {
          // 类内调用
          this.name
          console.log('hi')
      }
  }
  const person = new Person()
  // 类外调用
  person.name
  person.name = 'zwh'
  ```

+ `private`

  允许在类内被调用

  ```ts
  class Person {
      private name = 'xxh'
      say() {
          // 类内调用
          console.log(this.name)
      }
  }
  
  const person = new Person()
  // 类外调用均报错
  person.name
  person.name = 'hjh'
  
  ```

+ protected

  允许在类内以及继承的子类中使用

  ```ts
  class Person {
      protected name = 'xxh'
      say() {
          console.log(this.name)
      }
  }
  
  class Teacher extends Person {
      sayBye() {
          this.name
      }
  }
  ```

+ `readonly`

  只读属性必须在声明时或构造函数里被初始化
  
  ```ts
  class Person {
      public readonly name: string
      constructor(name: string) {
          this.name = name
      }
  }
  
  const person = new Person('Dell')
  // 报错
  person.name = 'hello'
  ```

## 4.2 constructor 简化写法

```ts
class Person {
    // 传统写法
    // public name: string
    // constructor(name: string) {
    //     this.name = name
    // }
    // 简化写法
    constructor(public name: string) {}
}

const person = new Person('xxh')
```

## 4.3 类中的getter setter

+ `getter`

  ```ts
  class Person {
      constructor(private _name: string) {}
      get name() {
          // 变相的获取_name
          return this._name
      }
  }
  
  const person = new Person('xxh')
  // 报错, _name是private只允许在类中使用
  // person._name
  person.name
  ```

+ `setter`

  ```ts
  class Person {
      constructor(private _name: string) {}
      get name() {
          return this._name
      }
      set name(value: string) {
          this._name = value
      }
  }
  
  const person = new Person('xxh')
  person.name = 'hjh'
  ```

## 4.4 单例类

希望只被实例化一次

```ts
// 单例类
class Demo {
    private static instance: Demo
    private constructor() {}

    static getInstance() {
        if (!this.instance) {
            this.instance = new Demo()
        }
        return this.instance
    }
}

const demo1 = Demo.getInstance()
const demo2 = Demo.getInstance()
```

## 4.5 抽象类

```ts
// 假如很多个类很多共性, 可以提取到抽象类中
class Circle {
    getArea() {}
}

class Square {
    getArea() {}
}

class Triangle {
    getArea() {}
}

// 抽象类
abstract class Geom {
    // 如果给类的方法加上abstract,说明这个方法也是抽象的,没有具体的实现
   abstract getArea(): number
   getType() {
       return 'Geom'
   }
}
// 报错,抽象类只能被继承不能被实例化
// new Geom()

class Circle extends Geom {
    // 需要具体区实现抽象方法
    getArea() {
        retrun 123
    }
}

class Square extends Geom {
    getArea() {
        retrun 123
    }
}

class Triangle extends Geom {
    getArea() {
        retrun 123
    }
}

```

## 4.6 把类当做接口使用

类定义会创建两个东西：类的实例类型和一个构造函数。 因为类可以创建出类型，所以你能够在允许使用接口的地方使用类

```tsx
class Point {
    x: number;
    y: number;
}

interface Point3d extends Point {
    z: number;
}

let point3d: Point3d = {x: 1, y: 2, z: 3};
```





# 五、爬虫案例

## 5.1 `superagent`

在 node 中请求，可以抓取到html

`.d.ts` 文件为<font color=red> 类型定义文件</font> (翻译文件)

```ts
import superagent from 'superagent'

class Crowller {
    private url = 'https://git.imooc.com/?from_url=1011'
    constructor() {
        superagent.get(this.url).then(res => {
            console.log(res.text)
        })
    }
}

const crowller = new Crowller()
```

## 5.2 `cheerio`

可以像 jquery 一样获取dom

```ts
import superagent from 'superagent'
import cheerio from 'cheerio'

class Crowller {
    private url = 'https://git.imooc.com/?from_url=1011'
    constructor() {
        superagent.get(this.url).then(res => {
            const $ = cheerio.load(res.text)
            $.html()
            $('h2').addClass('welcome')
            console.log($.html())
        })
    }
}

const crowller = new Crowller()
```

## 5.3 concurrently

用于运行多个 npm 命令

```json
"script": {
    "dev:build": "tsc -w",
    "dev:start": "nodemon node ./build/croller.js",
    "dev": "concurrently npm:dev:*"
},
"nodemonConfig": {
    "ignore": [
        "data/*"
    ]
}
```





# 六、配置文件

`tsconfig.json`

```json
{
  "compilerOptions": {
    /* Basic Options */
    // 增量编译 只编译不同的部分
    // "incremental": true,
    "target": "es5",
    "module": "commonjs",
    // "lib": [],
    // "allowJs": true,
    // "checkJs": true,
    // "jsx": "preserve",
    // "declaration": true,
    // "declarationMap": true,
    // "sourceMap": true,
    // "outFile": "./",
    // "outDir": "./",
    // "rootDir": "./",
    // "composite": true,
    // "tsBuildInfoFile": "./",
    // "removeComments": true,
    // "noEmit": true,
    // "importHelpers": true,
    // "downlevelIteration": true,
    // "isolatedModules": true,

    "strict": true,
    // 必须手动指定类型
    // "noImplicitAny": true,
    // 是否强制检查null类型
    // "strictNullChecks": true,
    // "strictFunctionTypes": true,
    // "strictBindCallApply": true,
    // "strictPropertyInitialization": true,
    // "noImplicitThis": true,
    // "alwaysStrict": true,
    // "noUnusedLocals": true,
    // "noUnusedParameters": true,
    // "noImplicitReturns": true,
    // "noFallthroughCasesInSwitch": true,

    // "moduleResolution": "node",
    // "baseUrl": "./",
    // "paths": {},
    // "rootDirs": [],
    // "typeRoots": [],
    // "types": [],
    // "allowSyntheticDefaultImports": true,
    "esModuleInterop": true,
    // "preserveSymlinks": true,
    // "allowUmdGlobalAccess": true,

    // "sourceRoot": "",
    // "mapRoot": "",
    // "inlineSourceMap": true,
    // "inlineSources": true,

    // "experimentalDecorators": true,
    // "emitDecoratorMetadata": true,

    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true 
  },
  // 要编译的目录
  // "include": ["./demo.ts"],
  // "exclude": []
}

```





# 七、联合类型和类型保护

```ts
interface Bird {
  fly: Boolean;
  sing: () => {}
}

interface Dog {
  fly: Boolean;
  bark: () => {}
}

// 联合类型 animal: Bird | Dog
function trainAnimal(animal: Bird | Dog) {
  // 报错：因为传入的类型中不一定有sing方法
  animal.sing()
}

// 类型断言做类型保护
function trainAnimal1(animal: Bird | Dog) {
  if(animal.fly) {
    // 如果传入的animal是Bird类型就可以调用sing方法
    (animal as Bird).sing()
  } else {
    (animal as Dog).bark()
  }
}

// in语法做类型保护
function trainAnimal2(animal: Bird | Dog) {
  if ('sing' in animal) {
    animal.sing()
  } else {
    animal.bark()
  }
}

function add(first: string | number, second: string | number) {]
  // 报错
  return first + second
}
// typeof语法做类型保护
function add1(first: string | number, second: string | number) {
  if (typeof first === 'string' || typeof second === 'string') {
    return `${first}${second}`
  }
  return first + second
}

class NumberObj {
  count: number
}
function addSecond(first: object | NumberObj, second: object | NumberObj) {
  // 报错 object 不一定有count属性
  return first.count + second.count
}
// instanceof做类型保护
function addSecond1(first: object | NumberObj, second: object | NumberObj) {
  if (first instanceof NumberObj && second instanceof NumberObj) {
    return first.count + second.count
  } else {
    return 0
  }
}

```





# 八、枚举类型 enum

+ 场景

  ```ts
  // 硬编码可读性很差
  function getResult(status: number) {
    if (status === 0) {
      return 'offline'
    } else if (status === 1) {
      return 'online'
    } else if (status === 2) {
      return 'deleted'
    }
    return 'error'
  }
  ```

+ js 中解决可读性差

  ```ts
  // 声明为常量
  const Status = {
    OFFLINE: 0,
    ONLINE: 1,
    DELETED: 2
  }
  
  function getResult(status: number) {
    if (status === Status.OFFLINE) {
      return 'offline'
    } else if (status === Status.ONLINE) {
      return 'online'
    } else if (status === Status.DELETED) {
      return 'deleted'
    }
    return 'error'
  }
  ```

+ 枚举类型解决

  ```ts
  enum Status {
    // 设置默认值
    // OFFLINE = 1,
    OFFLINE,
    ONLINE,
    DELETED
  }
  // 增量 每一项会根据上一项的值 + 1
  console.log(Status.OFFLINE) // 0
  console.log(Status.OFFLINE) // 1
  // 反查
  console.log(Status[0]) // OFFLINE
  
  function getResult(status: number) {
    if (status === Status.OFFLINE) {
      return 'offline'
    } else if (status === Status.ONLINE) {
      return 'online'
    } else if (status === Status.DELETED) {
      return 'deleted'
    }
    return 'error'
  }
  getResult(Status.OFFLINE) // offline
  getResult(0) // offline
  getResult(1) // online
  ```
  
+ 常量枚举

  为了避免在额外生成的代码上的开销和额外的非直接的对枚举成员的访问( console.log(枚举) )。 常量枚举通过在枚举上使用 `const`修饰符来定义

  ```tsx
  const enum Enum {
      A = 1,
      B = A * 2
  }
  ```

  



# 九、泛型

`generic` 泛指的类型 不是具体的类型

+ 语法

  `<T>` 字母可以随意 一般用T：type

+ 作用

  先声明为泛型，在具体使用的时候指定

## 9.1 函数泛型

+ 场景

  ```ts
  // 需求：如果传入first是rting 那么second也必须是string
  function join(first: string | number, second: string | number) {
    return `${first}${second}`
  }
  // 类型虽然吻合，但是无法控制一样
  join(1, '1')
  join('2', 1)
  join(2, 1)
  ```

+ 泛型解决

  ```ts
  // 用泛型解决 <T> 中随意写
  function join1<T>(first: T, second: T) {
    return `${first}${second}`
  }
  join1(1, 2) // 正常
  join1('1', 2) // 报错 两个参数类型不一致
  // 还可以指定具体的类型
  join1<string>('1', '2') // 类型符合预设
  join1<string>(1, 2) // 报错 参数不是string
  
  // 数组写法
  // function map<ABC>(params: Array<ABC>) { 等价于下面
  function map<ABC>(params: ABC[]) {
    return params
  }
  // <string> 实际上是指定上面<ABC>的类型
  map<string>(['1', '2'])
  map<string>('1', '2') // 报错
  ```

+ 定义多个泛型

  ```ts
  function join<T, P>(first: T, second: P) {
    return `${first}${second}`
  }
  join<number, string>(1, '2')
  // 类型推断
  join(1, '2')
  
  ```

+ 指定返回值类型为泛型

  ```ts
  function anotherJoin<T>(first: T): T {
    return first
  }
  ```

## 9.2 类泛型

+ 类中的泛型

  ```ts
  class DataManager<T> {
    constructor(private data: T[]) {}
    getItem(index: number): T {
      return this.data[index]
    }
  }
  
  const data = new DataManager<number>([1])
  // 类型注解
  const data1 = new DataManager([1])
  ```

+ 泛型继承

  ```ts
  interface Item {
    name: string;
  }
  
  class DataManager<T extends Item> {
    constructor(private data: T[]) {}
    getItem(index: number): string {
      return this.data[index].name
    }
  }
  
  const data = new DataManager([{
    name: 'xxh'
  }])
  ```

+ 限定泛型类型

  ```ts
  class DataManager<T extends string | number> {
    constructor(private data: T[]) {}
    getItem(index: number): T {
      return this.data[index]
    }
  }
  
  interface Test {
    name: string
  }
  
  // 报错 Test没有number或者string上面的方法不满足
  const data = new DataManager<Test>([])
  const data1 = new DataManager<string>([])
  const data2 = new DataManager<number>([])
  ```

## 9.3 泛型作为类型注解

```ts
function hello<T>(param: T) {
  return param
}

const func: <T>(param: T) => T = hello
```

## 9.4 keyof

+ 场景

  ```ts
  interface Person {
    name: string;
    age: number;
    gender: string;
  }
  class Teacher {
    constructor(private info: Person) {}
    getInfo(key: string) {
      // 这里返回的类型不确定 不传这个三个固定key 返回的类型为undefined
      // Teacher.getInfo(key: string): string | number | undefined
      // 类型保护
      if (key === 'name' || key === 'age' || key === 'gender') {
        return this.info[key]
      }
    }
  }
  
  const teacher = new Teacher({
    name: 'xxh',
    age: 18,
    gender: 'nan'
  })
  // Teacher.getInfo(key: string): string | number | undefined
  teacher.getInfo('name')
  ```

+ `keyof`

  ```ts
  interface Person {
    name: string;
    age: number;
    gender: string;
  }
  class Teacher {
    constructor(private info: Person) {}
    // keyof对Person中的属性值挨个遍历
    // 第一次循环 T extends 'name' 等价于 type T = 'name' 泛型T可以是一个固定的字符串！！
    // Person[T] ---> Person['name'] = string
    // 这样只限定了T只能为 'name' 'age' 'gender'
    getInfo<T extends keyof Person>(key: T): Person[T] {
        return this.info[key]
    }
  }
  
  const teacher = new Teacher({
    name: 'xxh',
    age: 18,
    gender: 'nan'
  })
  const test = teacher.getInfo('name') // test ---> string
  const test1 = teacher.getInfo('age') // test ---> number
  const test2 = teacher.getInfo('gender') // test ---> string
  const test3 = teacher.getInfo('hello') // 报错 没有hello这个key
  ```

  结论：<font color=red> **类型可以是一个字符串** </font>

  ```ts
  type NAME = 'name'
  const abc: NAME  = 'name' // 正确
  const abc: NAME  = 'hello' // 正确
  ```

  



# 十、命名空间

## 10.1 命名空间

+ 场景

  ```ts
  // 这样写等于暴露出三个全局变量 造成变量污染
  class Header {}
  class Content {}
  class Footer {}
  // 实际上我只需要执行Page这个类
  class Page {
      construtor() {
          new Header()
          new Content()
          new Footer
      }
  }
  ```

+ 用命名空间解决

  ```ts
  // 将所有的声明放在一个Home的命名空间中 将需要用到的申明export出去
  namespace Home {
    class Header {}
    class Content {}
    class Footer {}
    export class Page {
      construtor() {
        new Header()
        new Content()
        new Footer
      }
    }
  }
  // 使用
  new Home.Page()
  // 报错 Header并没有export出来
  new Home.Header()
  ```

+ 将多个文件打包成一个文件

  代码分离

  ```ts
  // Components.ts
  namespace Components {
    export class Header {}
    export class Content {}
    export class Footer {}
  }
  ```

  ```ts
  // Home.ts
  namespace Home {
    export class Page {
      construtor() {
        // 此时无法访问到Comment这个命名空间
        new Components.Header()
        new Components.Content()
        new Components.Footer
      }
    }
  }
  ```

  ```json
  // tsconfig.json
  {
    "compilerOptions": {
      "module": "amd", 
       // 将多个文件打包到一个文件
      "outFile": "./build/index.js",
    },
  }
  
  ```

  为了直观的可阅读性：依赖声明

  ```ts
  // Home.ts
  ///<reference path="./Components.ts" />
  namespace Home {
    export class Page {
      construtor() {
        new Components.Header()
        new Components.Content()
        new Components.Footer
      }
    }
  }
  ```

## 10.2 子命名空间

```ts
namespace Components {
  // 子命名空间
  export namespace SubComponents {
    export class Test {}
  }
  // 可以export接口
  export interface User {
    name: string;
  }
  export class Header {}
  export class Content {}
  export class Footer {}
}

// 外面使用
new Components.SubComponents.Test()
```





# 十一、import/export 模块化

namespace 不直观

```ts
// Components.ts
export class Header {}
export class Content {}
export class Footer {}
```

```ts
// Home.ts
import { Header, Content, Footer } from './Components.ts'
class Page {
  constructor() {
    new Headers()
    new Content()
    new Footer()
  }
}
```

## 11.1 Parcel 打包 TS 代码

+ `npm i parcel@next -D`

+ 不需要过多的配置

+ ```json
  // package.json
  "scripts": {
      "dev": "parcel ./src/index.html"
  }
  ```





# 十二 类型定义(描述)文件

`***.d.ts`

```ts
// jquery.d.ts

// 定义全局变量 declare var
// declare var $: (param: () => void) => void

// 1和2 重载
// 1. 定义全局函数 declare function
declare function $(readyFunc: () => void): void
// 2. 同时申明
declare function $(selector: string): {
  html: () => {}
}
// 使用interface重塑1和2的申明
interface JqueryInstance {
    html: (html: string) => JqueryInstance
}
interface JQuery {
    (readyFunc: () => void): void;
    (selector: string): JqueryInstance;
}
declare var $: JQuery;

// $.fn.init() 
// 对对象进行类型定义，以及对类进行类型定义，以及命名空间的嵌套
declare namespace $ {
    namespace fn {
        class init {}
    }
}
```

+ ES6 模块化中类型定义

  ```ts
  // index.ts
  import jquery from 'jquery'
  ```

  ```ts
  // jquery.d.ts
  // 名称必须一致
  declare module 'jquery' {
      interface JqueryInstance {
          html: (html: string) => JqueryInstance
      }
      // 前面的 declare 都可以去掉
      function $(readyFunc: () => void): void
      function $(selector: string): JqueryInstance
      namespace $ {
          namespace fn {
              class init {}
          }
      }
      export $
  }
  ```

  