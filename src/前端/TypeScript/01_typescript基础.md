# typescript

## 安装

```
npm install -g typescript
```

## 数据类型

- 基础类型:
  boolean,string,number,array,tuple,enum,null,undefined,object,void,never,any
- 高级类型: union,Nullable,Literal

## Number

- 对数字的定义只有一个很笼统的 number 来表示。
- 既能表示整数、也能表示浮点数，甚至可以表示正负数。

```TypeScript
function add(a:number, c:number) {
  return a+b
```

## String

```JavaScript
let a="hello"
let b='hello'
// 字符串模板，与js一致
let c =`hello${a}`
```

## boolean

- 真，假

```TS
let istrue: boolean = true;
```

## Array（数组）

- 数组中可以存放任意类型的数据
- js 中数组宽容度非常大，而 TS 也很好的继承了这一点

```TypeScript
// 单一类型数组
let list:number = [1,2,3,4]
let list2: Array<number>=[1,2,3,4]
let list3=[1,2,3,4]
// 混合类型数组
let list4 = [1, "ddd"]
let list5: any[]=[1,"123",true]
```

## Tupple（元组）

```TypeScript
// 不可以改变数据类型与修改元组长度
let person1: [number, string] = [1, "jerry"]
// 注意元组目前有bug，可以通过push来修改元组长度，且定义时一定要声明数据类型
```

## Union（联合）

```TypeScript
let a: string|number=1
a="aaaa"
```

## Literal（字面量）

```TypeScript
// 变量只可以在0,1，2中取值
let b: 0|1|2=1
```

## Enum（枚举类型）

```TypeScript
// 默认从0开始
enum Color {
  red=5,
  green,
  blue
}
```

## any 与 unknown

## tsconfig.json

```JSON
{
  "compilerOptions": {
    "noImplicitAny": false, // 不需要显式地声明变量的类型any
    "target": "es5", // 编译后的目标javascript版本,ES5, ES6/ES2015, ES2016, ES2017, ES2018, ES2019, ES2020, ESNext
    "lib": [
      "dom", // document.getElementById("root")
      "dom.iterable",
      "esnext"
    ],
    "allowJs": true, // 允许混合编译JavaScript文件
    "skipLibCheck": true,
    "esModuleInterop": true, // 允许我们使用commonjs的方式import默认文件,  import React from 'react'
    // "esModuleInterop": false, import * as React from 'react'
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "noFallthroughCasesInSwitch": true,
    "module": "esnext", // 配置的是我们代码的模块系统, Node.js的CommonJS、ES6标准的esnext、requirejs的AMD
    "moduleResolution": "node", // 决定了我们编译器的工作方式，"node" and "classic"
    "resolveJsonModule": true,
    "isolatedModules": true, // 编译器会将每个文件作为单独的模块来使用
    "noEmit": true, // 表示当发生错误的时候，编译器不要生成 JavaScript 代码
    "jsx": "react", // 允许编译器支持编译react代码
    "plugins": [
      {
        "name": "typescript-plugin-css-modules"
      }
    ]
  },
  "include": [
    "src"
  ]
}
```
