# TypeScript 常见面试题



## 目录

- [HTML](../html/html.md)

- [CSS](../css/css.md)

- [JavaScript](../js/js.md)

- [笔试题](../code/code.md)

- [TypeScript](../typescript/typescript.md)

- [Vue](../vue/vue.md)

- [Webpack 和前端工程化](../webpack/webpack.md)

- [微信小程序](../mini-program/mini-program.md)

- [计算机网络](../network/network.md)



## 什么是 TypeScript

TypeScript 是一个强类型的 JavaScript 超集，支持 ES6 语法，支持面向对象编程的概念，如类、接口、继承、泛型等。TypeScript 并不直接在浏览器上运行，需要编译器编译成纯 Javascript 来运行。



## TS 中 any 的作用

为编程阶段还不清楚类型的变量指定一个类型。 这些值可能来自于动态的内容，比如来自用户输入或第三方代码库。 这种情况下，我们不希望类型检查器对这些值进行检查而是直接让它们通过编译阶段的检查。



## TS 中的访问修饰符

- `private`：只在类的内部可以访问
- `public`：任何地方都可以访问
- `protected`：在类的内部或者子类中访问
- `readonly`：属实只读，不能修改



## TS 中 const 和 readonly 不同

- `const` 用于变量，`readonly` 用于属性
- `const` 在运行时检查，`readonly` 在编译时检查



## TS 中 any 和 unknown 异同

1. 任何类型都可以赋值给 `any` 和 `unknown`
2. 与 `any` 不同，`unknown` 类型的变量不能直接赋值给非 `any` 类型或非 `unknown` 类型的变量，需要使用 `typeof` 判断类型或者类型断言，因此，**unknown 可以说是类型安全的 any**



## TS 中接口和类型别名有什么异同点

### 相同点

1. 都可以描述对象和函数

```typescript
interface Person {
  name: string;
  age: number;
}
```

```typescript
type Person = {
  name: string;
  age: number;
};
```

2. 都可以被继承

```typescript
interface Person {
  name: string;
  age: number;
}

interface Student extends Person {
  grade: number;
}
```

```typescript
type Person = {
  name: string;
  age: number;
};

// 交叉类型
type Student = Person & {
  grade: number;
};
```

### 不同点

1. 除了对象和函数，`type` 还可以指定基本类型、联合类型、元组等。

```typescript
type Name = string;
type Account = string | number;
```

2. `interface` 可以重复声明，等同于两个接口进行合并。

```typescript
interface Person {
  name: string;
}

interface Person {
  age: number;
}

const person: Person = {
  name: 'Tom',
  age: 18,
};
```



## TS 中 typeof 和 keyof

- `typeof`：TS 中 `typeof` 可以获取变量的声明或者对象的类型。
- `keyof`：`keyof` 可以获取某种类型的所有键，返回值是联合类型。

```typescript
interface Person {
  name: string;
  age: number;
}

const person: Person = { name: 'Tom', age: 18 };

type TypeOfPerson = typeof person; // Person
```

```typescript
interface Person {
  name: string;
  age: number;
}

type KeyOfPerson = keyof Person; // "name" | "number"
```



## TS 泛型

泛型是指在定义函数、接口或类的时候，不指定具体的类型，而是可以和不同类型一起工作，从而实现复用。**简单的说，“泛型就是把类型当成参数”。**

```typescript
function getValue<T>(value: T): T {
  return value;
}

const num = getValue<number>(1);
const str = getValue<string>('a');
```



## TS 模块加载机制

1. 首先，编译器会尝试定位需要导入的模块文件，通过绝对或者相对的路径查找方式；
2. 如果没有查找到对应的模块，编译器会尝试定位一个类型声明文件（`*.d.ts`）；
3. 最后，如果编译器还是不能解析这个模块，则会抛出一个错误。

> `tsconfig.json` 配置文件中，可以通过 `files`、`include` 和 `exclude` 指定编译的文件（`*.ts`和 `*.d.ts`）。



## TS 中 declare 用法

在 TS 的类型声明文件中，通过 `declare` 声明一些全局变量、全局方法、全局对象等。其中，`declare global` 可以扩展全局变量的类型。