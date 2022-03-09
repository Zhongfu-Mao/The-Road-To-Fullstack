# TypeScript基础

## 安装

```shell
npm install -g typescript
yarn add typescript
brew install typescript
```

## tsc

> TypeScript Compile

```shell
tsc --version

tsc <file> [-w] # 编译文件, -w 可以监视文件变化
```

## 类型种类

!!!quote

    TypeScript中有13种基础数据类型

    1. boolean
    2. number
    3. string
    4. Array
    5. Tuple
    6. enum
    7. null
    8. undefined
    9. any
    10. unknown
    11. void
    12. never
    13. object

## 类型声明

### 基础类型

```ts
let isDone: boolean = false,
    count: number = 10,
    firstName: string = "naruto";

const sym = Symbol();
let obj = {
    [sym]: "symbol type",
};

let u: undefined = undefined;
let n: null = null;

// ***********************************字符串字面量类型*************************************
let shape: 'circle' | 'square' = 'circle';
// shape = 'rectangle'; // 错误：字符串“rectangle”不是合法的值
shape = 'square';


// ***********************************数字串字面量类型*************************************
let dayInWeek: 1 | 2 | 3 | 4 | 5 | 6 | 7;
dayInWeek = 1;
dayInWeek = 3;
dayInWeek = 6;
// dayInWeek = 8; // 错误：值必须是从1到7的整数
```

### 对象类型

```ts
let obj: {a: number, b: string, c?: string} = {a: 1, b: '2'};
```

### 数组类型

```ts
let arr: number[] = [1, 2, 3];
let arr2: Array<number> = [1, 2, 3];
```

### 组合类型

```ts
let combinedType1: number | string | boolean = 1;
let combinedType2: number[] | string = [1, 2, 3];
let combinedType3: (string | number | boolean)[] = [1, 2, 3, '4'];
```

### 枚举类型

```ts
enum Direction1 { // 数字列挙型
    NORTH,
    SOUTH,
    EAST,
    WEST,
}
let dir: Direction1 = Direction1.NORTH;

enum Direction2 { //　文字列列挙型
    NORTH = "NORTH",
    SOUTH = "SOUTH",
    EAST = "EAST",
    WEST = "WEST"
}

const enum Direction3 {
    NORTH,
    SOUTH,
    EAST,
    WEST
}
let dir3: Direction3 = Direction3.NORTH; // コンパイルした結果は var dir3 = 0

enum Enum {
    A,
    B,
    C = "C",
    D = "D",
    E = 8,
    F // 9
}
```

### any类型

```ts
let notSure: any = 666; // Any
let valueAny: any; // OK
valueAny.foo.bar; // OK
valueAny.trim(); // OK
valueAny(); // OK
new valueAny(); // OK
```

### unknown类型

```ts
let valueUnknown: unknown; // Unknown
valueUnknown = true; // OK
valueUnknown = 42; // OK
valueUnknown = "Hello World"; // OK
valueUnknown = []; // OK
valueUnknown = {}; // OK
valueUnknown = Math.random; // OK
valueUnknown = null; // OK
valueUnknown = undefined; // OK
valueUnknown = new TypeError(); // OK
valueUnknown = Symbol("type"); // OK

let value: unknown;
let value1: unknown = value,  // OK
    value2: any = value,  // OK
    value3: boolean = value,  // Error
    value4: number = value,  // Error
    value5: string = value,  // Error
    value6: object = value,  // Error
    value7: any[] = value,  // Error
    value8: Function = value;  // Error

value.foo.bar;  // Error
value.trim();  // Error
value();  // Error
new value();  // Error
```

### void类型

```ts
let unusedVar: void = null;
let usedVar: void = undefined;

function warnUser(): void {
    console.log("this is a warning message");
}
```

### never类型

```ts
function error(message: string): never {
    throw new Error(message);
}

function infiniteLoop(): never {
    while (true) {}
}
```

### 函数返回值类型

```ts
function sum(x: number, y: number): number {
    return x + y;
}

functon sum2(x: number, y: number): string {
    return `结果: ${x + y}`;
}

function msg(): void {
    console.log("Hello World");
}

let sum3: (x: number, y: number) => number = (x, y) => x + y;
```

### 函数参数类型

```ts
type userType = {name: string; age: number; sex?: string | number};
let addUser = (user: userType): void => {
    console.log(`Add user: "name: ${user.name}, age: ${user.age}"`);
}

function sum(..args: number[]): number {
    return args.reduce((s, n) => s + n);
}
```

### 函数结构定义

```ts
let hd: (a: number, b: number) => number;
hd = (a, b) => a + b;
```

### 元组类型

```ts
let tupleType: [string, boolean];
tupleType = ["naruto", true];
```

## tsconfig.json

```shell
tsc --init
```

## 断言

### as语法

```ts
function foo(arg: boolean): string | number {
    return arg ? "hello" : 1;
}

let res = foo(true) as string;
```

### as const语法

```ts
let foo: string = "foo";

let bar: "bar" = "bar";

const foobar = "foobar";

let baz = true as const; // 类似 let baz: true = true;

const arr = [foo, bar, baz] as const // 变为readonly
const arr2 = <const>[foo, bar, baz]

const obj = {
    foo,
    bar,
    baz
} as const;
```

### 解构中使用as const语法

```ts
function foo() {
    let a = "a";
    let b = (x: number, y: number, z: number) => x + y + z;

    return [a, b]
    // return [a, b] as [typeof a, typeof b];
}

// const [n, m] = foo();
const [n, m] = [...foo()] as const;
// const [n, m] = foo() as [string, Function];
// const [n, m] = foo() as [string, (x: number, y: number, z: number) => number];
console.log((m as Function)(1, 2, 3));
```

### 非空断言

```ts
let foo: string | null | undefined = "foo";
```

### DOM类型推断与断言处理

```ts
const el: HTMLElement = document.getElementById("foo") as HTMLElement;
const el2: HTMLDivElement = document.getElementById(".bar")!;
```

### class构造函数需要的强制断言

```ts
class Foo {
    constructor(el: HTMLDivElement) {
        this.el = el;
    }

    html() {
        return this.el.innerHTML;
    }
}
```

### DOM事件处理

```ts
const btn = document.getElementById("btn") as HTMLButtonElement;

btn.addEventListener("click", (e: Event) => {
    e.preventDefault();
});
```
