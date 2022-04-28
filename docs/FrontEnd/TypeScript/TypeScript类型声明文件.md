# TypeScript类型声明文件

> Declaration files give you the ability to give TypeScript more information about how a function or class is structured.  
> Declaration files do not have any implementation code; they simply describe the types and structure for the elements used in the module.  
> Declaration files are used solely for the benefit of the developer and are only utilized by the IDE.

## 三斜线指令

```ts
/// <reference types=“UMDModuleName/globalName” />
```

* TypeScript的早期模块化标签,用来引用其他模块的类型定义文件
* 三斜线指令必须放在文件的最顶端，三斜线指令的前面只允许出现单行或多行注释
* 现在使用`import`替代三斜线指令

## 全局变量

* `declare let/const`: 声明全局变量
* `declare function`: 声明全局方法
* `declare class`: 声明全局类
* `declare enum`: 声明全局枚举类型
* `declare namespace`: 声明全局对象（含有子属性）
* `interface/type`: 声明全局类型

!!! example

    ```ts
    // 变量
    declare let userName: string;

    declare const wx: any;

    // 函数、函数重载
    declare function getName(uid: number): string;
    declare function getName(): string;
    declare function getName(cb: () => any): any;

    // 类
    declare class Course {
      cid: number;
      constructor(cid){};
      getCoursePrice(): number;
    }

    // 枚举
    declare enum Status {
      Loading,
      Success,
      Failed,
    }

    // 接口 interface declare 可以不需要
    interface CourseInfo {
      cid: number;
      name: string;
    }

    interface CGIData<T> {
      data: T;
      retcode: 0;
    }

    // 命名空间
    declare namespace User {
      // 局部 Test.User
      interface User {
        name: string;
        age: number;
      }

      function getUserInfo(name: string): User {
        return "";
      }
      namespace fn {
        function extend(obj: any): any;
      }
    }


    // 声明合并
    declare function User(id: number): string;
    ```

## 编译时自动生成`.d.ts`文件

```json
{
    "compilerOptions": {
        "declaration": true,
    }
}
```
