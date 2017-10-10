---
title: good-code-test
date: 2017-10-10 15:44:48
tags: 算法逻辑题
---
### 好玩的算法逻辑题总汇
#### 多重数组展开
```
    function flaten1(arr) {
        var narray = [];
        // 定义处理函数
        function flat(arr) {
            arr.forEach((item) => {
                if (Array.isArray(item)) {
                    flat(item);
                } else {
                    narray.push(item);
                }
            });
        }
        // 执行函数
        flat(arr);
        return narray;
    }
    // 不考虑数据类型和 数组里面不存在"2,3"这样的数据的时候可以用这样的巧
    function flaten2(arr) {
        var narray = [];
        var str = arr.join(",");
        narray = str.split(',');
        return narray;
    }
    console.log(flaten1([1, 2, [3, [4, 5, [
        [6]
    ]]]]));
    console.log(flaten2([1, 2, [3, [4, 5, [
        [6]
    ]]]]));
```
#### 数组里面的数据拼接成最大数
```
    // 数组里面的数据拼接成最大数
    function maxNumber(arr) {
        function compare(a, b) {
            var num1 = a + '';
            var num2 = b + '';
            // b-a 从大到小排序
            return (num2 + num1) - (num1 + num2);
        }
        // +输出数据类型是number
        return +(arr.sort(compare).join(""));
    }
    console.log(maxNumber([2, 3, 31, 32, 5, 10, 1]));


```
#### 长度不超过5位数的 数字转为中文大写
```
    // 长度不超过5位数的 数字转为中文大写
    function changeLangue(num) {
        console.log('===========', num, "===========");
        num = num + '';
        var carr = ['十', '百', '千', '万'],
            narr = ['零', '一', '二', '三', '四', '五', '六', '七', '八', '九'],
            strarr = [],
            newcarr = [];
        // 将数字拆分为数组
        for (var i = 0; i < num.length; i++) {
            strarr.push(num.substring(i, i + 1));
        }
        // 数字转化为大写中文
        strarr.reverse().forEach(function(item, index, array) {
            if (item % 10 == 0) {
                index == 0 && array.length > 1 ? '' : array[index+1] % 10 == 0 ? '': newcarr.push(narr[item % 10]);
                return;
            } else {
                if (index) {
                    newcarr.push(carr[index - 1]);
                }
                newcarr.push(narr[item % 10]);
            }
        });
        newcarr = newcarr.reverse();
        // 处理是整万的情况
        if (newcarr[newcarr.length - 1] == '零' && newcarr.length > 1) {
            newcarr.pop();
        }
        return (newcarr.join(""));
    }
    console.log(changeLangue(90991));
```
