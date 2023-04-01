# 前端笔试题



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



## 手写 Object.create() 方法

`Object.create()` 方法将传入的对象作为新对象的原型：

```js
function createObject(object) {
  function F() {}
  F.prototype = object;
  return new F();
}
```



## 手写 instanceof

`instanceof` 用于判断对象是否是构造函数的实例，原理是判断构造函数的原型对象是否在实例的原型链上。

```js
function instanceOf(instance, object) {
  const prototype = Object.getPrototypeOf(instance);
  if (prototype === object.prototype) {
    return true;
  }
  if (prototype === null) {
    return false;
  }
  return instanceOf(prototype, object);
}
```



## 手写 new

通过 `new` 创建实例包含以下过程：

1. 为新对象分配内存
2. 新对象的原型指针指向构造函数的原型
3. `this` 指向新对象
4. 执行构造函数
5. 如果构造函数返回一个非空对象，则返回该对象，否则返回之前创建的新对象

```js
function newInstance(constructor, ...args) {
  const instance = Object.create(constructor.prototype);
  const obj = constructor.apply(this, args);
  return obj instanceof Object ? obj : instance;
}
```



## 函数防抖和函数节流

函数防抖和函数节流可以避免时间频繁触发而耗费性能，例如：联想搜索、滚动监听、避免按钮重复点击等。

- 函数防抖（`debounce`）：触发事件一段时间后才执行，如果期间重复触发，则重新计时
- 函数节流（`throttle`）：事件在一段时间内只会触发一次

```js
function debounce(func, wait = 200) {
  let timer = null;
  return function () {
    if (!timer) {
      timer = setTimeout(() => {
        timer = null;
        func.apply(this, arguments);
      }, wait);
    }
  };
}
```

```js
function throttle(func, wait = 200) {
  let timer = null;
  return function () {
    if (!timer) {
      func.apply(this, arguments);
      timer = setTimeout(() => {
        timer = null;
      }, wait);
    }
  };
}
```

使用时间戳定义的函数节流：

```js
function throttle(func, wait = 200) {
  let previous = 0;
  return function () {
    let now = Date.now();
    if (now - previous > wait) {
      func.apply(this, arguments);
      previous = now;
    }
  };
}
```



## 手写 AJAX

```js
const xhr = new XMLHttpRequest();
xhr.open('get', 'https://api.github.com/users/JungleHico', true);
xhr.onreadystatechange = () => {
  if (xhr.readyState === 4) {
    if (xhr.status === 200) {
      console.log(xhr.response);
    }
  }
};
xhr.send(null);
```



## 手写深拷贝

深拷贝需要递归遍历对象的属性，如果该属性时基本数据类型，直接返回，如果是引用类型，则递归创建其副本，然后添加到对象的属性上，实现的时候需要区分是不是数组。

```js
function cloneDeep(object) {
  if (object instanceof Object) {
    if (Array.isArray(object)) {
      const array = [];
      object.forEach((item) => {
        array.push(cloneDeep(item));
      });
      return array;
    } else {
      const obj = {};
      for (const key in object) {
        obj[key] = cloneDeep(object[key]);
      }
      return obj;
    }
  }
  return object;
}
```



## 手写数组 push() 方法

`push()` 是数组的共享方法，需要写在其原型链上，`push()` 接受一个参数列表，会将这些参数添加到数组的尾部，然后返回数组的长度。

```js
Array.prototype._push = function () {
  for (let i = 0; i < arguments.length; i++) {
    this.push(arguments[i]);
  }
  return this.length;
};
```



## 手写数组 map() 方法

`map()` 是数组的共享方法，需要写在其原型链上，`map()` 接受一个回调函数，返回原数组的副本，数组中的每一项执行回调函数。

```js
Array.prototype._map = function (callbackFn) {
  if (typeof callbackFn !== 'function') {
    throw new TypeError(`${callbackFn} is not a function`);
  }
  const list = [];
  this.forEach((item) => {
    list.push(callbackFn(item));
  });
  return list;
};
```



### 数组去重

1. 方法一：`filter()`：

```js
function unique(list) {
  return list.filter((item, index) => list.indexOf(item) === index);
}
```

2. 方法二：`Set()`：

```js
function unique(list) {
  return Array.from(new Set(list));
}
```

3. 方法三：`Map()`：

```js
function unique(list) {
  const map = new Map();
  list.forEach((item) => {
    const count = map.has(item) || 0;
    map.set(item, count + 1);
  });
  return Array.from(map.keys());
}
```



## 冒泡排序

第一次遍历，每个元素和下一个元素比较，如果比下一个元素打，则交换这两个元素的位置，最终最大的元素会以“冒泡”的形式排在最后；

第二次遍历，把第二大的元素排到倒数第二位；

以此类推，直到数组完成排序。

```js
function bubbleSort(list) {
  for (let i = 0; i < list.length - 1; i++) {
    for (let j = 0; j < list.length - 1 - i; j++) {
      if (list[j] > list[j + 1]) {
        [list[j], list[j + 1]] = [list[j + 1], list[j]];
      }
    }
  }
}
```



## 选择排序

选择排序从第一个数开始遍历，记录最小值，如果当前元素比之前记录的最小值小，则更新最小值，循环结束后，把最小值排到第二位；

第二次遍历，从第二个数开始记录和遍历，以此类推，直至数组完成排序。

```js
function selectSort(list) {
  for (let i = 0; i < list.length; i++) {
    let minIndex = i;
    for (let j = i + 1; j < list.length; j++) {
      if (list[j] < list[minIndex]) {
        minIndex = j;
      }
    }
    [list[i], list[minIndex]] = [list[minIndex], list[i]];
  }
}
```



## 直接插入排序

直接插入排序将数组分为两部分，已排序和未排序，初始时已排序包含第一个元素，未排序部分从第二个元素开始；

每次遍历时，取出未排序部分的第一个元素，与已排序的元素逐个进行比较（一般是从后往前），插入到正确的位置，直到所有元素都完成排序。

```js
function insertSort(list) {
  for (let i = 1; i < list.length; i++) {
    for (let j = i; j > 0; j--) {
      if (list[j] > list[j - 1]) {
        break;
      }
      [list[j], list[j - 1]] = [list[j - 1], list[j]];
    }
  }
}
```



## 折半（二分）插入排序

折半插入排序的原理和直接插入排序差不多，只不过在比较元素大小时，不是逐个进行比较，而是将未排序元素与已排序数组的中间值进行比较：

如果大于中间值，则以相同方法比较中间值之后的元素；

否则以相同方法比较中间值之前的元素；

当找到元素的正确位置后，将该位置后面的元素后移，将该元素放到该位置。

```js
function binaryInsertSort(list) {
  for (let i = 1; i < list.length; i++) {
    let low = 0;
    let height = list.length - 1;
    while (low <= high) {
      let middle = Math.floor((low + height) / 2);
      if (list[i] > list[middle]) {
        low = middle + 1;
      } else {
        high = middle - 1;
      }
    }
    const tmp = list[i];
    for (let k = i; k > high + 1; k--) {
      list[k] = list[k - 1];
    }
    list[high + 1] = tmp;
  }
}
```



## 快速排序

快排以一个数作为基准值，例如第一个数，并定义两个索引指针，一个从前往后遍历，一个从后往前遍历：

首先从后往前遍历，找到第一个比基准值小的元素，然后从前往后遍历，找到第一个比基准值大的元素，交换这两个元素的位置；

当前后两个指针重叠时，将基准值放到指针重叠位置，这样比基准值小的值都位于基准值前面，比基准值大的值都位于基准值后面；

以基准值为分割点，将数组分成两个区间，两个区间分别使用以上方法进行排序，当区间只剩一个元素时，完成排序。

```js
function quickSort(list, left, right) {
  if (left < right) {
    let low = left;
    let high = right;
    let base = low;
    while (low < high) {
      while (low < high && list[high] >= list[base]) {
        high--;
      }
      while (low < high && list[low] <= list[base]) {
        low++;
      }
      [list[low], list[high]] = [list[high], list[low]];
    }
    [list[base], list[low]] = [list[low], list[base]];
    quickSort(list, left, low - 1);
    quickSort(list, high + 1, right);
  }
}
```





