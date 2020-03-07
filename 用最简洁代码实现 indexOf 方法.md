# 用最简洁代码实现 indexOf 方法

## 解题思路：

一般遇到这种题目，其实就考验你平时是否有自己的思考的时候了。这种时候一般给出标准答案只能是及格线，你可以给出更多。

思考点：
首先要弄明白 indexOf 的作用是什么？

- 第一，是在于 String 字符，查询元素在字符中出现的第一个位置，如果没有则返回-1
- 第二，是 Array 数组中查询数组中元素的出现的第一个位置，如果没有则返回-1
- 第三，原 indexOf 的参数有两个，indexOf(value, startIndex),value 为需要查找的元素，startIndex 是从哪个索引位置开始查找

总归而知，indexOf 就是从 startIndex 开始查询某个元素在整体元素的索引位置，如果没有则返回-1

代码如下：

```js
function indexOf(target, searchElement = undefined, startIndex = 0) {
  // 数组通过遍历查询
  if (Object.prototype.toString.call(target) === "[object Array]") {
    for (let i = startIndex, len = target.length; i < len; i++) {
      if (target[i] === searchElement) {
        return i;
      }
    }
    return -1;
  }
  // 正则进行查询
  if (Object.prototype.toString.call(target) === "[object String]") {
    const reg = new RegExp(`${searchElement}`, 'gi');
    const match= reg.exec(target.slice(startIndex));
    if(match){
        const resultIndex = match.index + startIndex;
        return resultIndex > target.length ? target.length : resultIndex
    }
    return -1;
  }

  throw new Error("target必须传入为数组Array或String类型");
}
```

## 考点：

1. 对 js 函数 api 是否有足够了解，知道indexOf 的作用和参数
2. 基础编程能力，异常边界思考，如：传入startIndex为小于0如何处理
3. 如果传入非数组或非字符串如何处理，是否也可以实现查询结果，如：传入为数字进行查找呢（虽然没特别大的意义）

## 冷门知识点

- 数组和字符串的 indexOf 实现原理不同，字符串采用的是正则匹配实现， 数组是采用遍历实现，因此会有如下结果：

```js
const str = "123";
str.indexOf(1); // 输出0

const array = [1, 2, 3];
str.indexOf("1"); // 输出-1
```

- 字符串indexOf有个点需要注意就是`传入空字符串的时候，返回为0---str.length 之间`，这其实是实现一个坑吧？或者是有其他理由？

```js
const str = "123";
str.indexOf(""); // 输出0
str.indexOf("", 1); // 输出1
str.indexOf("", 5); // 输出3
```

**因此，说明用indexOf判断一个字符串是否包含某个元素有点不太准确。**

## 加强印象

- [Array.prototype.indexOf()--MDN说明](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)
- [String.prototype.indexOf()--MDN说明](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/indexOf)

## 扩展问题
实现lastIndexOf，现在可以实现吗？