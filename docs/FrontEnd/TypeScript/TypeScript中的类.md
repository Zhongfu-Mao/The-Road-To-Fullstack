# TypeScript中的类

## 可选成员

```typescript
class Calculator {
    precision?: number; // 可选的精度属性

    static maxOperand?: number; // 可选的静态最大操作数属性
    static minOperand: number; // 非可选静态属性

    // 可选的加法计算方法
    add?(x: number, y: number): number;

    // 可选的减法计算方法
    subtract?(x: number, y: number): number {
        return x - y;
    }

    // 可选的最大操作数获取静态方法
    static getMaxOperand?(): number;

    // 可选的最小操作数获取静态方法
    static getMinOperand?(): number {
        return this.minOperand;
    }
}
```

## 静态成员

```typescript
// 计时器类
class Calculator {
    _precision: number = 2;
    static _maxOperand: number = 100;
    static _minOperand: number = -100;

    /**
     * 访问器，访问属性_precision
     */
    get precision(): number {
        console.log('获取属性_precision的值')
        return this._precision;
    }

    /**
     * 设置器，设置属性_precision
     */
    set precision(value: number) {
        console.log('设置属性_precision的值')
        this._precision = value;
    }

    /**
     * 静态读取器，访问静态属性_maxOperand
     */
    static get maxOperand(): number {
        console.log('读取静态属性_maxOperand的值')
        return Calculator._maxOperand;
    }

    /**
     * 静态设置器，设置静态属性_maxOperand
     */
    static set maxOperand(value: number) {
        console.log('设置静态属性_maxOperand的值')
        this._maxOperand = value; // this的是当前类，而非实例
    }

    /**
     * 静态读取器，访问静态属性_minOperand
     */
    static get minOperand(): number {
        console.log('读取静态属性_minOperand的值')
        return Calculator._minOperand;
    }

    /**
     * 静态设置器，设置静态属性_minOperand
     */
    static set minOperand(value: number) {
        console.log('设置静态属性_minOperand的值')
        this._minOperand = value; // this的是当前类，而非实例
    }

    /**
     * 构造计算器实例，不再接受操作数范围参数
     */
    constructor() {
    }

    /**
     * 重置操作数范围
     */
    static resetOperandRange(): void {
        Calculator._maxOperand = 100;
        this._minOperand = -100;
    }

    /**
     * 加法
     * @param x 加数 
     * @param y 加数
     */
    add(x: number, y: number): number {
        let areOperandsLegal: boolean = this.checkOperands(x, y);
        if (!areOperandsLegal) {
            throw '非法的操作数';
        }

        let fixed: string = (x + y).toFixed(this._precision); // 保留指定位数的小数
        return +fixed; // 将字符串转换成数字
    }

    /**
     * 减法
     * @param x 被减数
     * @param y 减数
     */
    subtract(x: number, y: number): number {
        let areOperandsLegal: boolean = this.checkOperands(x, y);
        if (!areOperandsLegal) {
            throw '非法的操作数';
        }

        let fixed: string = (x - y).toFixed(this._precision); // 保留指定位数的小数
        return +fixed; // 将字符串转换成数字
    }

    /**
     * 判断参与运算的两个操作数是否合法
     * @param x 操作数1
     * @param y 操作数2
     */
    checkOperands(x: number, y: number): boolean {
        if (x > Calculator.maxOperand || x < Calculator.minOperand) {
            console.log('操作数x超出了可计算数的范围');
            return false;
        }

        if (y > Calculator.maxOperand || y < Calculator.minOperand) {
            console.log('操作数y超出了可计算数的范围');
            return false;
        }

        return true;
    }
}
```

## 继承

```typescript
class Car {
    color: string;
    run(): void {
        console.log(`${this.color}车在跑。。`);
    }

    beep(): string {
        return '嘟嘟';
    }
}

class SportsCar extends Car {
}

class SuperSportsCar extends SportsCar {
    nos: number; // 氮氧化物加速系统
    accelerate(): void {
        console.log(`加速1分钟，N2O剩余${--this.nos}千克。。`);
    }

    // 非法的重写：类型() => void不兼容于类型() => string
    // beep(): void {
    //     console.log('滴滴');
    // }

    beep(): string {
        return '滴滴';
    }
}

class ElectroCar extends Car {
    // 重写继承自父类的run()方法
    run(): void {
        super.run(); // 调用父类的run()方法
        console.log('我是烧电的。。');
    }
}

class Hovercar extends Car {
    constructor(color: string) {
        super(); // 调用父类的构造函数
        this.color = color;
    }
}

// 类型为Car的SportsCar实例
let superSportsCar: Car = new SuperSportsCar();
let beep = superSportsCar.beep(); // 获得“滴滴”
// superSportsCar.accelerate(); // 错误：汽车类Car未定义方法accelerate()
let _superSportsCar = superSportsCar as SuperSportsCar; // 类型断言
_superSportsCar.nos = 10;
_superSportsCar.accelerate(); // 输出“加速1分钟，N2O剩余9千克。。”

// 汽车质量检车函数
function checkCar(car: Car): boolean {
    try {
        car.beep();
        car.run();
        return true; // 车辆合格，返回true
    }
    catch {
        return false; // 车辆不合格，返回false
    }
}

// 检测超级跑车和电动汽车是否合格
let electroCar: ElectroCar = new ElectroCar();
let isSuperSportsCarQualified: boolean = checkCar(superSportsCar);
let isElectroCarQualified: boolean = checkCar(electroCar);

```

## 索引

```typescript
// 使用下标访问背包对象的颜色属性
let knapsack = { color: 'orange', material: 'canvas', capacity: 10 };
let knapsackColor = knapsack['color']; // 得到“orange”

// 背包类
class Knapsack {
    [index: string]: string;
    material: string; // 包含索引的类可以封装属性
    // capacity: number; // 错误：属性的类型必须和索引值的类型一致
}

let knapsack1: Knapsack = new Knapsack();
knapsack1['color'] = 'orange'; // 向knapsack的索引中添加键为color值为orange的索引
let owner = knapsack1['owner']; // 获得到undefined，因为我们没有向knapsack1添加键为owner的索引项

// 索引键类型为number的背包类
class Packsack {
    [index: number]: string;
}

// 封装两个索引的帆布包类
class Rucksack {
    [index: string]: string;
    [index: number]: any;
}
```

## 访问性修饰符

```typescript
class Calculator {
    protected readonly precision: number = 2;
    private static _maxOperand: number = 100;
    public static readonly minOperand: number = -100;

    // 读取私有属性_maxOperand的公共读取器
    static get maxOperand(): number {
        return this._maxOperand;
    }

    public constructor(precision: number) {
        this.precision = precision;
    }

    // 受保护的操作数检查方法
    protected checkOperands(x: number, y: number): boolean {
        if (x > Calculator.maxOperand || x < Calculator.minOperand) {
            console.log('操作数x超出了可计算数的范围');
            return false;
        }

        if (y > Calculator.maxOperand || y < Calculator.minOperand) {
            console.log('操作数y超出了可计算数的范围');
            return false;
        }

        return true;
    }
}
```

## 抽象类

```typescript
abstract class Discount {
    // 折扣描述
    abstract description: string;

    /**
     * 折扣策略构造函数
     * @param totalAmount 总金额
     */
    constructor(protected totalAmount: number) {
    }

    // 获取折扣金额
    abstract getDiscountAmount(): number;
}

class NewbieDiscount extends Discount {
    description: string = '新用户一律5折';

    getDiscountAmount(): number {
        return this.totalAmount * 0.5;
    }
}

class RichDiscount extends Discount {
    description: string = '满额100打8折';

    getDiscountAmount(): number {
        return this.totalAmount < 100 ? this.totalAmount : this.totalAmount * 0.8;
    }
}
```
