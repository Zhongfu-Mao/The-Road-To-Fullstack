## 参数

### 默认参数


```typescript
function getBiggerHeight(height: number, unit: string = 'px') {
    return height * 2 + unit;
}

getBiggerHeight(20); // 获得40px
getBiggerHeight(30, 'em'); // 获得60em
```

### 可选参数


```typescript
// 用户注册函数
function register(name: string, password: string, age?: number) {
    console.log(`记录注册信息-用户名：${name}，密码：${password}` + (age ? `，年龄：${age}` : ''));
}

register('Lcng', '1'); // 输出“记录注册信息-用户名：Lcng，密码：1”
register('Lcng', '1', 3); // 输出“记录注册信息-用户名：Lcng，密码：1，年龄：3”
```

### 剩余参数


```typescript
// 添加联系方式
function addContact(phone: string, ...addresses:string[]) {
    console.log(`记录联系方式-电话号码：${phone}` + (addresses && addresses.length ? `，地址：${addresses.join(',')}` : ''));
}

addContact('13111111111'); // 输出“记录联系方式-电话号码：13111111111”

// 输出“记录联系方式-电话号码：13111111111，地址：Baker Street 221B”
addContact('13111111111', 'Baker Street 221B');

// 输出“记录联系方式-电话号码：13111111111，地址：Baker Street 221B, Calle Bleeckrr 177A”
addContact('13111111111', 'Baker Street 221B', 'Calle Bleeckrr 177A');

// 错误：类型“string[]”的值不能赋给类型“string”的参数
// addContact('13111111111', ['Baker Street 221B', 'Calle Bleeckrr 177A'])

// 输出“记录联系方式-电话号码：13111111111，地址：Baker Street 221B, Calle Bleeckrr 177A”
addContact('13111111111', ...['Baker Street 221B', 'Calle Bleeckrr 177A'])
```

## 函数类型


```typescript
// 加法函数
function add(x: number, y: number): number {
    return x + y;
}

let typeOfAdd = typeof (add); // 得到字符串function
let myAdd: (x: number, y: number) => number = add;
// let myAdd_2: function = add; // 错误，不存在类型function
```

### 类型别名


```typescript
type containingType = (x: string, y: string) => boolean;
type comparingType = (x: string, y: string) => boolean;
// 尽管以上两个类型别名是等价的，但我们不能使用等于号（“==”或“===”）对它们进行比较，因为等于号仅用于值的比较，而类型（别名）不是值

// 判断指定字符串是否包含另一个子字符串的函数变量
let contains: containingType = function (x: string, y: string): boolean {
    return x.indexOf(y) > -1;
}

// 按字典顺序判断指定的一个字符串是否大于指定的另一个字符串
let greaterThan: comparingType = function (x: string, y: string): boolean {
    return x > y;
}

// 获取函数变量greaterThan的类型别名
type greaterThanType = typeof greaterThan; // 获取编译时类型
let typeOfGreaterThan: string = typeof greaterThan; // 获取运行时类型
```

### 类型兼容


```typescript
/**
 * 模拟jQuery中的ajax()函数
 * @param url 要访问的URL
 * @param callback 服务端返回响应后要执行的回调函数
 */
 function ajax(url: string, callback: (response: string, statusCode: number, statusText: string) => void) {
    // 省略了异步请求

    // 服务端返回响应后，执行调用方提供的回调函数
    callback('服务端响应字符串', 0, '调用成功');
}

// 异步访问http://localhost:3000/ajax
ajax('http://localhost:3000/ajax', function (res: string, code: number, text: string): void {
    if (code !== 0) {
        console.log('调用失败');
        return;
    }

    console.log(res);
});


// 计算函数变量
let calculate: (x: number, y: number, operator: string) => number;
calculate = function (a: number, b: number): number {
    return a + b;
}
// 错误，类型不兼容
// calculate = function(a: string, b: string): number {
//         return (a + b).length;
// }

/**************************参数类型兼容*****************************/
calculate = function (x: any, y: any): number {
    return x * y;
}

// 错误：类型number和null不兼容
// calculate = function (x: null, y: null): number {
//     return 0;
// }
/**************************返回类型兼容*****************************/
calculate = function (x: number, y: number): any {
    return x - y;
}

// 错误：类型undefined不兼容于number
// calculate = function(x: number, y: number) : undefined {
//     return undefined;
// }


/********兼容任何函数类型的函数类型(...args: any[]) => void*******/
type baseType = (...args: any[]) => void;
let func1: baseType = function () {
    console.log('func1');
}
let func2: baseType = function (n: number, s: string): string {
    return n + s;
}
let func3: baseType = function (b: boolean): boolean {
    return !b;
}
let func4: baseType = function (): never {
    throw 'error..';
}
```

## 函数重载


```typescript
function add(x: number, y: number): number; // 加法运算函数
function add(x: string, y: string): string; // 字符串拼接函数
function add(x: any, y: any): any {
    return x + y; // 加法运算或字符串拼接的实现
}

let sum: number = add(1, 3); // 得到3
let fullName: string = add('L', 'cng'); // 得到Lcng

// 错误，这看上去是在合法地调用类型为(x: any, y: any) => any的实现函数，但TypeScript编译器不允许实现函数被直接调用
// let address: string = add('Baker Street', 211);


function subtract(x: number, y: number): number; // 两个数的减法
function subtract(x: number, y: number, z: number): number; // 三个数的减法
function subtract(x: number, y: number, z?: number): number { // 参数z应是可选参数
    return (z === null || z === undefined) ? (x - y) : (x - y - z)
}

let difference = subtract(1, 2); // 获得-1
difference = subtract(1, 2, 3); // 获得-4
// difference = subtract (1, 2, 3, 4); // 错误，subtract()函数没有接受4个参数的重载
```
