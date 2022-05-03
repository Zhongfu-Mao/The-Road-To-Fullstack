# TypeScript中的泛型

```typescript
function add<T>(x: T, y: T): T {
    let result: T = (x as any) + (y as any);
    return result;
}

let sum = add<number>(1, 2); // 得到数字3
let concatenation = add<string>('1', '2'); // 得到字符串12

// let result = add<number>(1, true); // 错误，布尔值true的类型不是number
let result1 = add<boolean>(true, true); // 得到数字2
```

泛型函数（Generic Function），其名字后面的一对尖括号及尖括号内的字母T是其作为泛型函数的标志。  
其中，字母T称为类型参数（Type Parameter），代表一个（定义时未知的）类型，在整个函数的定义过程中都可以当作类型使用

```typescript
// 使用类型约束
function add<T extends number | string>(x: T, y: T): T {
    return (x as any) + (y as any);
}

let sum = add(1, 2); // 得到数字3
let concatenation = add('1', '2'); // 得到字符串12
// let result = add<boolean>(true, true); // 错误，boolean不兼容于number | string
// let result1 = add(false, false); // 错误，推断类型Boolean不兼容于number | string

class Biology {
    name: string;
}

class ObjectFactory<T extends Biology> {
    constructor(constructor: new () => T) {
    }
    // ...省略的代码
}
```

## 接口

### 对象接口

```typescript
// 计算器对象接口
interface ICalculator<T> {
    add(x: T, y: T): T;
}

// 数字计算器类
class NumericCalculator implements ICalculator<number> {
    add(x: number, y: number): number {
        return x + y;
    }
}

// 字符串计算器类
class StringCalculator implements ICalculator<string> {
    add(x: string, y: string): string {
        return x + y;
    }
}

// 泛型计算器类
class Calculator<T> implements ICalculator<number> {
    add(x: number, y: number): number {
        return (x as any) + (y as any);
    }
}

// 另一个泛型计算器类
class Calculator1<T> implements ICalculator<T> {
    add(x: T, y: T): T {
        return (x as any) + (y as any);
    }
}
```

### 函数接口

```typescript
// 泛型函数add()的类型接口
interface TypeOfAdd<T> {
    (x: T, y: T): T;
}

let add: TypeOfAdd<number> = (x: number, y: number) => x + y; // 数字加法运算函数
let add1: TypeOfAdd<string> = (x: string, y: string) => x + y; // 字符串拼接函数

let add2: <T>(x: T, y: T) => T;
add2 = <T>(x: T, y: T) => (x as any) + (y as any); // 数字加法运算或字符串拼接函数
add2<number>(1, 2); // 得到数字3
add2<string>('1', '2'); // 得到字符串12
```

### 类接口

```typescript
// 泛型计算器类
class Calculator<T>  {
    add(x: T, y: T): T {
        return (x as any) + (y as any);
    }
}

// 泛型计算器类的类型接口
interface TypeOfCalculator {
    new <T>(): Calculator<T>
}

// 定义值为泛型计算器类的变量，并使用它来创建计算器对象
let genericCalculator: TypeOfCalculator = Calculator;
let calculator: Calculator<number> = new genericCalculator<number>();
calculator.add(1, 2); // 得到数字3
```
