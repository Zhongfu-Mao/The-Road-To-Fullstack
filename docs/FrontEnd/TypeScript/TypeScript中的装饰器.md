# TypeScript中的装饰器

## 开启装饰器

* 使用flag: `tsc --experimentalDecorators`
* 配置`tsconfig.json`文件，添加`experimentalDecorators`项

```json
{
    "compilerOptions": {
        "experimentalDecorators": true
    }
}
```

## 装饰器的种类

* Class decorators
* Method decorators
* Accessor decorators
* Property decorators
* Parameter decorators

```typescript
@ClassDecorator
class SampleClass {
    @PropertyDecorator
    public sampleProperty:number = 0;

    private _sampleField: number = 0;

    @AccessorDecorator
    public get sampleField() { return this._sampleField; }

    @MethodDecorator
    public sampleMethod(@ParameterDecorator paramName: string) {} }

function ClassDecorator (constructor: Function) {}

function AccessorDecorator (target: any, propertyName: string, descriptor: PropertyDescriptor) {}

function MethodDecorator (target: any, propertyName: string, descriptor: PropertyDescriptor) {}

function PropertyDecorator (target: any, propertyName: string) {}

function ParameterDecorator (target: any, propertyName: string, parameterIndex: number) {}
```
