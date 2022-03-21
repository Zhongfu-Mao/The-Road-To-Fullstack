```typescript
class Plane {
    fly() {
        console.log("I'm flying..");
    }
}

class Ship {
    sail() {
        console.log("I'm sailing..");
    }
}

let seaplane: Plane & Ship;
function createSeaplane(plane: Plane, ship: Ship): Plane & Ship {
    let seaplane: any = {};

    for (let key in plane) {
        seaplane[key] = plane[key];
    }

    for (let key in ship) {
        seaplane[key] = ship[key];
    }

    return seaplane;
}
seaplane = createSeaplane(new Plane(), new Ship);
seaplane.fly();
seaplane.sail();
```


```typescript
interface Hero {
    name: string;
    power: Record<string, number>; // Record
}

const hero: Partial<Hero> = { // Partial
    name: "Iron man"
}
```


```typescript

let someValue: any = "this is a string";
let strLength1: number = (<string>someValue).length;  // データタイプ断言、方法1
let strLength2: number = (someValue as string).length;  // データタイプ断言、方法2

const a: number | undefined = undefined;
const b: number = a!; // nullとundefinedを排除する
```


```typescript
// 所有类型的父类型
let n: {} = 1;
let s: {} = "2";
let f: {} = () => { console.log(123) };
```


```typescript
/** タイプをガイド */

//　方法１：`in`
interface Admin {
    name: string;
    privileges: string[];
}

interface Employee {
    name: string;
    startDate: Date;
}

type UnknownEmployee = Employee | Admin;

function printEmployeeInformation(emp: UnknownEmployee) {
    console.log(`Name: ${emp.name}`);
    if ("privileges" in emp) {
        console.log(`Privileges: ${emp.privileges}`);
    }
    if ("startDate" in emp) {
        console.log(`Start Date: ${emp.startDate}`);
    }
}

//　方法２: `typeof`
function padLeft(value: string, padding: string | number) {
    if (typeof padding === "number") {
        return Array(padding + 1).join(" ") + value;
    }
    if (typeof padding === "string") {
        return padding + value;
    }
    throw new Error(`Expected string or number , get '${padding}'`)
}

// 方法３：　`instanceof`
interface Padder {
    getPaddingString(): string;
}

class SpaceRepeatingPadder implements Padder {
    constructor(private numSpaces: number) {}
    getPaddingString() {
        return Array(this.numSpaces + 1).join(" ");
    }
}

let padder: Padder = new SpaceRepeatingPadder(6);

if (padder instanceof SpaceRepeatingPadder) {

}

// 方法4：自分で定義する
function isNumber(x: any): x is number {
    return typeof x === "number";
}

function isString(x: any): x is string {
    return typeof x === "string";
}
```


```typescript
/** タイプの結合と別名 */

const sayHello = (name: string | undefined) => {

};

type EventNames = "click" | "scroll" | "mousemove";

enum CarTransmission {
    Automatic = 200,
    Manual = 300
}

interface MotorCycle {
    vType: "motorcycle";
    make: number;
}

interface Car {
    vType: "car";
    transmission: CarTransmission;
}

interface Truck {
    vType: "truck";
    capacity: number;
}

type Vehicle = MotorCycle | Car | Truck;

const EVALUATION_FACTOR = Math.PI;

function evaluatePrice(vehicle: Vehicle) {
    switch (vehicle.vType) {
        case "car":
            return vehicle.transmission * EVALUATION_FACTOR;
        case "truck":
            return vehicle.capacity * EVALUATION_FACTOR;
        case "motorcycle":
            return vehicle.make * EVALUATION_FACTOR;
    }
}

const myTruck: Truck = { vType: "truck", capacity: 9.5 };
evaluatePrice(myTruck);

type PartialPointX = { x: number; };
type Point = PartialPointX & { y: number; };

let point: Point = {
    x: 1,
    y: 1
}

interface X {
    c: string;
    d: string;
}

interface Y {
    c: number;
    e: string;
}

type XY = X & Y;
type YX = Y & X;

let p: XY;
let q: YX;

p = { c: 6, d: "d", e: "e"}; // string & numbet -> never
q = { c: "c", d: "d", e: "e"};

interface D { d: boolean; }
interface E { e: string; }
interface F { f: number; }

interface A { x: D; }
interface B { x: E; }
interface C { x: F; }

type ABC = A & B & C;

let abc: ABC = {
    x: { // OK
        d: true,
        e: "hello",
        f: 666
    }
}
```


```typescript
// 函数类型接口
interface functionType {
    (x: number, y: number): number;
}

// class FunctionClass implements functionType { // 错误，函数类型接口无法被类实现
// }

let add: functionType = (x: number, y: number): number => {
    return x + y;
}
let sum: number = add(1, 2); // 得到3

```


```typescript
class Calculator {
    precision: number = 2;
    static maxOperand: number = 100;
    static minOperand: number = -100;

    constructor(precision: number) {
        this.precision = precision;
    }

    static checkOperands(x: number, y: number): boolean {
        return true;
    }
}

// 类的类型接口
interface CalculatorClassType {
    new(precision: number): Calculator;
    maxOperand: number;
    minOperand: number;
    checkOperands: (x: number, y: number) => boolean
}

let calculatorClass: CalculatorClassType = Calculator;
let calculator: Calculator = new calculatorClass(2);
// 错误：calculatorClass是计算器类Calculator的对象一侧，而非类型一侧
// let calculator1: calculatorClass = new calculatorClass(2);

// 获取计算器类Calculator的类型部分
type calculatorType = Calculator;
let calculator2: calculatorType = new calculatorClass(2);

```


```typescript
// 接口VS抽象类

// 耳机接口
interface Earphone {
    // 输出声音
    output(voice: string):void;
}

// 耳机抽象类
abstract class AbstractEarphone {
    // 输出声音
    abstract output(voice: string):void;
}

// 小米耳机类
class XiaoMiEarphone implements Earphone {
    // 输出声音
    output(voice: string): void {
        console.log(`来自小米耳机的输出：${voice}`);
    }

    // 声音输入
    input(voice: string): void {
        console.log(`小米耳机接收到的输入：${voice}`);
    }
}

// 苹果耳机
class AppleEarphone extends AbstractEarphone {
    // 输出声音
    output(voice: string): void {
        console.log(`来自苹果耳机的输出：${voice}`);
    }
}

// 另一个耳机接口：接口合并
interface Earphone {
    // 输入声音
    input(voice: string): void;
}

// 小米耳机接口：通过接口对类进行扩展
interface XiaoMiEarphone {
    // 降噪
    denoise():void;
}

let xiaoMiEarphone: XiaoMiEarphone = new XiaoMiEarphone();
// xiaoMiEarphone.denoise(); // 运行时错误：xiaoMiEarphone.denoise不是一个方法

// 在原型上实现降噪方法
XiaoMiEarphone.prototype.denoise = function() {
    console.log('降噪功能开启');
}
let xiaoMiEarphone1: XiaoMiEarphone = new XiaoMiEarphone();
xiaoMiEarphone1.denoise();
```
