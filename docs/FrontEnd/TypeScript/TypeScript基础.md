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

tsc --all # 查看参数选项

tsc --init # 初始化`tsconfig.json`

tsc <file> [-w] # 编译文件, -w 可以监视文件变化
```

### tsconfig.json

```js
{
  "compilerOptions": {
    /* Visit https://aka.ms/tsconfig.json to read more about this file */

    /* Projects */
    // "incremental": true,                              /* Enable incremental compilation */
    // "composite": true,                                /* Enable constraints that allow a TypeScript project to be used with project references. */
    // "tsBuildInfoFile": "./",                          /* Specify the folder for .tsbuildinfo incremental compilation files. */
    // "disableSourceOfProjectReferenceRedirect": true,  /* Disable preferring source files instead of declaration files when referencing composite projects */
    // "disableSolutionSearching": true,                 /* Opt a project out of multi-project reference checking when editing. */
    // "disableReferencedProjectLoad": true,             /* Reduce the number of projects loaded automatically by TypeScript. */

    /* Language and Environment */
    "target": "es2016",                                  /* Set the JavaScript language version for emitted JavaScript and include compatible library declarations. */
    // "lib": [],                                        /* Specify a set of bundled library declaration files that describe the target runtime environment. */
    // "jsx": "preserve",                                /* Specify what JSX code is generated. */
    // "experimentalDecorators": true,                   /* Enable experimental support for TC39 stage 2 draft decorators. */
    // "emitDecoratorMetadata": true,                    /* Emit design-type metadata for decorated declarations in source files. */
    // "jsxFactory": "",                                 /* Specify the JSX factory function used when targeting React JSX emit, e.g. 'React.createElement' or 'h' */
    // "jsxFragmentFactory": "",                         /* Specify the JSX Fragment reference used for fragments when targeting React JSX emit e.g. 'React.Fragment' or 'Fragment'. */
    // "jsxImportSource": "",                            /* Specify module specifier used to import the JSX factory functions when using `jsx: react-jsx*`.` */
    // "reactNamespace": "",                             /* Specify the object invoked for `createElement`. This only applies when targeting `react` JSX emit. */
    // "noLib": true,                                    /* Disable including any library files, including the default lib.d.ts. */
    // "useDefineForClassFields": true,                  /* Emit ECMAScript-standard-compliant class fields. */

    /* Modules */
    "module": "commonjs",                                /* Specify what module code is generated. */
    // "rootDir": "./",                                  /* Specify the root folder within your source files. */
    // "moduleResolution": "node",                       /* Specify how TypeScript looks up a file from a given module specifier. */
    // "baseUrl": "./",                                  /* Specify the base directory to resolve non-relative module names. */
    // "paths": {},                                      /* Specify a set of entries that re-map imports to additional lookup locations. */
    // "rootDirs": [],                                   /* Allow multiple folders to be treated as one when resolving modules. */
    // "typeRoots": [],                                  /* Specify multiple folders that act like `./node_modules/@types`. */
    // "types": [],                                      /* Specify type package names to be included without being referenced in a source file. */
    // "allowUmdGlobalAccess": true,                     /* Allow accessing UMD globals from modules. */
    // "resolveJsonModule": true,                        /* Enable importing .json files */
    // "noResolve": true,                                /* Disallow `import`s, `require`s or `<reference>`s from expanding the number of files TypeScript should add to a project. */

    /* JavaScript Support */
    // "allowJs": true,                                  /* Allow JavaScript files to be a part of your program. Use the `checkJS` option to get errors from these files. */
    // "checkJs": true,                                  /* Enable error reporting in type-checked JavaScript files. */
    // "maxNodeModuleJsDepth": 1,                        /* Specify the maximum folder depth used for checking JavaScript files from `node_modules`. Only applicable with `allowJs`. */

    /* Emit */
    // "declaration": true,                              /* Generate .d.ts files from TypeScript and JavaScript files in your project. */
    // "declarationMap": true,                           /* Create sourcemaps for d.ts files. */
    // "emitDeclarationOnly": true,                      /* Only output d.ts files and not JavaScript files. */
    // "sourceMap": true,                                /* Create source map files for emitted JavaScript files. */
    // "outFile": "./",                                  /* Specify a file that bundles all outputs into one JavaScript file. If `declaration` is true, also designates a file that bundles all .d.ts output. */
    // "outDir": "./",                                   /* Specify an output folder for all emitted files. */
    // "removeComments": true,                           /* Disable emitting comments. */
    // "noEmit": true,                                   /* Disable emitting files from a compilation. */
    // "importHelpers": true,                            /* Allow importing helper functions from tslib once per project, instead of including them per-file. */
    // "importsNotUsedAsValues": "remove",               /* Specify emit/checking behavior for imports that are only used for types */
    // "downlevelIteration": true,                       /* Emit more compliant, but verbose and less performant JavaScript for iteration. */
    // "sourceRoot": "",                                 /* Specify the root path for debuggers to find the reference source code. */
    // "mapRoot": "",                                    /* Specify the location where debugger should locate map files instead of generated locations. */
    // "inlineSourceMap": true,                          /* Include sourcemap files inside the emitted JavaScript. */
    // "inlineSources": true,                            /* Include source code in the sourcemaps inside the emitted JavaScript. */
    // "emitBOM": true,                                  /* Emit a UTF-8 Byte Order Mark (BOM) in the beginning of output files. */
    // "newLine": "crlf",                                /* Set the newline character for emitting files. */
    // "stripInternal": true,                            /* Disable emitting declarations that have `@internal` in their JSDoc comments. */
    // "noEmitHelpers": true,                            /* Disable generating custom helper functions like `__extends` in compiled output. */
    // "noEmitOnError": true,                            /* Disable emitting files if any type checking errors are reported. */
    // "preserveConstEnums": true,                       /* Disable erasing `const enum` declarations in generated code. */
    // "declarationDir": "./",                           /* Specify the output directory for generated declaration files. */
    // "preserveValueImports": true,                     /* Preserve unused imported values in the JavaScript output that would otherwise be removed. */

    /* Interop Constraints */
    // "isolatedModules": true,                          /* Ensure that each file can be safely transpiled without relying on other imports. */
    // "allowSyntheticDefaultImports": true,             /* Allow 'import x from y' when a module doesn't have a default export. */
    "esModuleInterop": true,                             /* Emit additional JavaScript to ease support for importing CommonJS modules. This enables `allowSyntheticDefaultImports` for type compatibility. */
    // "preserveSymlinks": true,                         /* Disable resolving symlinks to their realpath. This correlates to the same flag in node. */
    "forceConsistentCasingInFileNames": true,            /* Ensure that casing is correct in imports. */

    /* Type Checking */
    "strict": true,                                      /* Enable all strict type-checking options. */
    // "noImplicitAny": true,                            /* Enable error reporting for expressions and declarations with an implied `any` type.. */
    // "strictNullChecks": true,                         /* When type checking, take into account `null` and `undefined`. */
    // "strictFunctionTypes": true,                      /* When assigning functions, check to ensure parameters and the return values are subtype-compatible. */
    // "strictBindCallApply": true,                      /* Check that the arguments for `bind`, `call`, and `apply` methods match the original function. */
    // "strictPropertyInitialization": true,             /* Check for class properties that are declared but not set in the constructor. */
    // "noImplicitThis": true,                           /* Enable error reporting when `this` is given the type `any`. */
    // "useUnknownInCatchVariables": true,               /* Type catch clause variables as 'unknown' instead of 'any'. */
    // "alwaysStrict": true,                             /* Ensure 'use strict' is always emitted. */
    // "noUnusedLocals": true,                           /* Enable error reporting when a local variables aren't read. */
    // "noUnusedParameters": true,                       /* Raise an error when a function parameter isn't read */
    // "exactOptionalPropertyTypes": true,               /* Interpret optional property types as written, rather than adding 'undefined'. */
    // "noImplicitReturns": true,                        /* Enable error reporting for codepaths that do not explicitly return in a function. */
    // "noFallthroughCasesInSwitch": true,               /* Enable error reporting for fallthrough cases in switch statements. */
    // "noUncheckedIndexedAccess": true,                 /* Include 'undefined' in index signature results */
    // "noImplicitOverride": true,                       /* Ensure overriding members in derived classes are marked with an override modifier. */
    // "noPropertyAccessFromIndexSignature": true,       /* Enforces using indexed accessors for keys declared using an indexed type */
    // "allowUnusedLabels": true,                        /* Disable error reporting for unused labels. */
    // "allowUnreachableCode": true,                     /* Disable error reporting for unreachable code. */

    /* Completeness */
    // "skipDefaultLibCheck": true,                      /* Skip type checking .d.ts files that are included with TypeScript. */
    "skipLibCheck": true                                 /* Skip type checking all .d.ts files. */
  }
}

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

### 自定义类型

```ts
type integer = number & {
    toFixed: (n: number) => string;
};

type Person = [string, string, number?];

type User = {
    name: string;
    age: number;
    sex?: string;
}
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
