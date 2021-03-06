---
title: JavaScript algorithm
date: 2017-10-10 15:44:48
tags: javascript
keywords: javascript算法，经典算法，冒泡排序，快排，选择排序
---

### 好玩的算法逻辑题总汇

#### 算法排序

##### 冒泡排序

![冒泡排序图_来源于网络](https://camo.githubusercontent.com/bc20131e2ee7ad70c06e7c71eefc04c3a3cc18a2/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313630393136313630373438333839)
算法步骤

-   第一步，比较相邻的元素。如果第一个比第二个大，就交换它们两个
-   第二步，对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对，这样在最后的元素应该会是最大的数
-   第三步，针对所有的元素重复以上的步骤，除了最后一个
-   第四步，重复上面

```javascript
// 普通
function unquieMaoPao(arr) {
    var len = arr.length;
    for (var i = 0; i < len - 1; i++) {
        for (var j = 0; j < len - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                var temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    return arr;
}
// 改良版 主要是避免本来就是排序正常的无效排序
function unquieMaoPaoTwo(arr) {
    var len = arr.length;
    var i = len - 1;
    while (i > 0) {
        var pos = 0;
        for (var j = 0; j < i; j++) {
            if (arr[j] > arr[j + 1]) {
                pos = j;
                var temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
        i = pos;
    }
    return arr;
}
```

##### 选择排序

![选择排序动图_来源网络](https://camo.githubusercontent.com/603dd620708cd52e8d60af45ffbcb1c7986c98ba/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313630393136313634373534303133)
算法步骤

-   第一步，每个第一个与后面的比较如果更大或者更小就交换
-   第二步，重复这个步骤 arr.length 次

```javascript
function unquieSelect(arr) {
    var len = arr.length;
    for (var i = 0; i < len; i++) {
        var temp = arr[i];
        var pindex = i;
        for (var j = i; j < len; j++) {
            if (arr[pindex] < arr[j]) {
                pindex = j;
            }
        }
        arr[i] = arr[pindex];
        arr[pindex] = temp;
    }
    return arr;
}
```

##### 快速排序

![快速排序动图_来源网络](https://camo.githubusercontent.com/253b22840353c9759694d63839fe7565d48f9df6/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313630393137303033303034393036)
算法步骤

-   从一个数组中挑出一个基准元素
-   比之小的放左边，大的放右边
-   循环

```javascript
function unquieKuaiPai(arr) {
    if (arr.length <= 1) return arr;
    var prvoid = Math.floor(arr.length / 2);
    var provoidIndex = arr.splice(prvoid, 1)[0];
    var left = [];
    var right = [];
    for (var i = 0; i < arr.length; i++) {
        if (arr[i] < provoidIndex) {
            left.push(arr[i]);
        } else {
            right.push(arr[i]);
        }
    }
    return unquieKuaiPai(left).concat([provoidIndex], unquieKuaiPai(right));
}
```

#### 数组的排列组合

##### [[1,2],[3,4]] => [[1,3],[1,4],[2,3],[2,4]]

```javascript
function comarr(arr) {
    var narr = [[]]; // empty
    for (var i = 0; i < arr.length; i++) {
        var barr = [];
        for (var m = 0; m < narr.length; m++) {
            for (var n = 0; n < arr[i].length; n++) {
                barr.push(narr[m].concat(arr[i][n]));
            }
        }
        narr = barr;
    }
    return narr;
}
```

###### 解析过程

```javascript
/*解析过程
    [[]]

    [[1],[2]]                                                                                          i=0

    [[1,3],[1,4],[2,3],[2,4]]                                                                          i=1

    [[1,3,5],[1,3,6],[1,3,7],[1,4,5],[1,4,6],[1,4,7],[2,3,5],[2,3,6],[2,3,7],[2,4,5],[2,4,6],[2,4,7]]  i=2
    */
```

##### ['a','b','c'] number:2 => [['a','b'],['a','c'],['b','c']]

```javascript
Array.prototype.combinate = function (number, aIn) {
    debugger;
    if (!aIn) {
        // 如果没有aIn 定义为一个空数组
        var aIn = new Array();
        // 定义result数组 存储结果
        this.combinate.aResult = new Array();
    }
    for (var i = 0; i < this.length; i++) {
        var a = aIn.concat(this[i]);
        var aRest = this.concat();
        aRest.splice(0, i + 1);
        if (number && number - 1 <= aRest.length) {
            aRest.combinate(number - 1, a);
            if (number == 1) {
                this.combinate.aResult.push(a);
            }
        }
    }
    return this.combinate.aResult;
};
```

##### 解析过程

```javascript
combinateEStack = [
        thrid3:{
            thisarray:["c"],
            number:0,
            aIn:["b","a"],
            aResult:[["a","b"],["a","c"]],
            a:["b","a","c"],
            aRest:["c"],
            aRest:[],
            ===============
            becasuse number = 0不执行 if 里面的条件句 pop出栈
            ===============
            开始执行second2.waitetorun1
        },
        thrid2:{
            thisarray:["b"],
            number:0,
            aIn:["a","c"],
            aResult:[["a","b"]],
            a:["a","c","b"],
            aRest:["b"],
            aRest:[],
            ===============
            becasuse number = 0不执行 if 里面的条件句 pop出栈
            ===============
            开始执行second1.waitetorun2
        },
        thrid1:{
            thisarray:["c"],
            number:0,
            aIn:["a","b"],
            aResult:[],
            a:["a","b","c"],
            aRest:["c"],
            aRest:[],
            =================
            becasuse number = 0不执行 if 里面的条件句 pop出栈
            =================
            开始执行second1.waitetorun1
        },
        second2:{
            ****************** //for i=0 循环第一次 总共循环次数 1次
            thisarray:["c"],
            number:1,
            aIn:["b"],
            aResult:[["a","b"],["a","c"]],
            a:["b","c"],
            aRest:["c"],
            aRest:[],
            ====================
            number:1
            // number && number - 1 <= aRest.length
            1 && 0 <= 0
            执行thrid3
            waitetorun1:aResult.push(a)
            =====================
            执行完waitetorun1
            aResult:[["a","b"],["a","c"],["b","c"]]
            =====================================
            for循环完毕 this.length = 1 循环了1次 pop出栈
        },
        second1:{
            ****************** //for i=0 循环第一次   总共循环次数 2次
            thisarray:["b","c"],//上一个的aRest
            number:1,
            aIn:["a"], //上一个的a
            aResult:[],//总函数的
            a:["a","b"],//aIn.concat(this[i]);
            aRest:["b","c"],//thisarray
            aRest:["c"],//thisarray.splice(0,i+1)
            ================
            number:1,
            // number && number - 1 <= aRest.length
            1 && 0 < = 1
            执行thrid1
            waitetorun1:aResult.push(a)
            ================
            执行完waitetorun1
            aResult:[["a","b"]]
            ******************* //for i= 1循环第二次
            a:["a","c"],
            aRest:["b","c"],
            aRest:[],
            ===============
            number:1,
            // number && number - 1 <= aRest.length
            1 && 0 <= 0
            执行thrid2
            waitetorun2:aResult.push(a)
            ==================
            执行完waitetorun2
            aResult:[["a","b"],["a","c"]],
            ==================================
            for循环完毕 this.length = 2 循环了2次 pop出栈

        },
        first:{
            ****************** //for i=0 循环第一次   总共循环次数 3次
            thisarray:["a","b","c"]
            number:2,
            aIn:[],
            aResult:[],
            a:["a"],//aIn.concat(this[i]);
            aRest:["a","b","c"],//this.concat();
            aRest:["b","c"],//aRest.splice(0, i + 1);
            =================
            number:2
            // number && number - 1 <= aRest.length
            2 && 1 < = 2
            开始执行second1
            ****************** //for i=1 循环第二次
            a:["b"],//aIn.concat(this[i]);
            aRest:["a","b","c"],
            aRest:["c"],
            ==================
            number:2,
            // number && number - 1 <= aRest.length
            2 && 1 < = 1
            开始执行second2
            ****************** //for i=2 循环第三次
            a:["c"],
            aRest:["a","b","c"],
            aRest:[],
            // number && number - 1 <= aRest.length
            2 && 1 < = 0  if 条件不执行

        },
        globalcontext
    ]
```

#### 多重数组展开

```javascript
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
    narray = str.split(",");
    return narray;
}
console.log(flaten1([1, 2, [3, [4, 5, [[6]]]]]));
console.log(flaten2([1, 2, [3, [4, 5, [[6]]]]]));
```

#### 数组里面的数据拼接成最大数

```javascript
// 数组里面的数据拼接成最大数
function maxNumber(arr) {
    function compare(a, b) {
        var num1 = a + "";
        var num2 = b + "";
        // b-a 从大到小排序
        return num2 + num1 - (num1 + num2);
    }
    // +输出数据类型是number
    return +arr.sort(compare).join("");
}
console.log(maxNumber([2, 3, 31, 32, 5, 10, 1]));
```

#### 长度不超过 5 位数的 数字转为中文大写

```javascript
// 长度不超过5位数的 数字转为中文大写
function changeLangue(num) {
    console.log("===========", num, "===========");
    num = num + "";
    var carr = ["十", "百", "千", "万"],
        narr = ["零", "一", "二", "三", "四", "五", "六", "七", "八", "九"],
        strarr = [],
        newcarr = [];
    // 将数字拆分为数组
    for (var i = 0; i < num.length; i++) {
        strarr.push(num.substring(i, i + 1));
    }
    // 数字转化为大写中文
    strarr.reverse().forEach(function (item, index, array) {
        if (item % 10 == 0) {
            index == 0 && array.length > 1
                ? ""
                : array[index + 1] % 10 == 0
                ? ""
                : newcarr.push(narr[item % 10]);
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
    if (newcarr[newcarr.length - 1] == "零" && newcarr.length > 1) {
        newcarr.pop();
    }
    return newcarr.join("");
}
console.log(changeLangue(90991));
```

#### 递归经典算法练习

```javascript
// 递归的算法求递加
function countage(wpeo) {
    if (wpeo == 1) {
        return 10;
    } else {
        return countage(wpeo - 1) + 2;
    }
}
console.log(countage(4));

// for循环实现阶乘函数
function jiecheng(num) {
    if (num < 0) {
        return -1;
    } else if (num === 0 || num === 1) {
        return 1;
    } else {
        for (var i = num - 1; i >= 1; i--) {
            num = num * i;
        }
        return num;
    }
}
console.log("阶乘函数结果是===>", jiecheng(10));

// 递归乘法
function recursive(i) {
    if (i == 0) {
        return 1;
    } else {
        return i * recursive(i - 1);
    }
}
console.log(recursive(3));

// 河内塔问题
function heneita(n, a, b, c) {
    if (n == 1) {
        alert("--------" + n + a + b + c);
        // 第二步: 最底下的1个盘子，从A移到C
        document.write(
            "1111111把编号 " + n + " 个盘子从 " + a + " to " + c + "</br>"
        );
    } else {
        alert("*********" + n + a + b + c);
        // 第一步：把上面（n-1）个盘子从A移到B
        heneita(n - 1, a, c, b);
        document.write(
            "22222222把编号 " + n + " 个盘子从 " + a + " to " + c + "</br>"
        );
        alert("=========" + n + a + b + c);
        // 第三步：把（n-1）个盘子从B移到C
        // alert('##########' + n + a + b + c);
        heneita(n - 1, b, a, c);
    }
}
console.log(heneita(3, "A", "B", "C"));
// !!!! 递归数量过大存在栈溢出问题 可以使用尾递归优化，更建议使用for循环 如果是递归数量过大的时候
```

#### js 数组去重方法之一

##### ES5 去重

```javascript
//arr 举例 [1,2,1,2,3] || [1,'2',1,2,3]
function arrUnique(arr) {
    if (Array.isArray(arr) && arr.length > 1) {
        let n = [arr[0]];
        arr.forEach(function (val) {
            if (n.indexOf(val) == -1) {
                n.push(val);
            }
        });
        return n;
    } else {
        return [];
    }
}
// 数组去重 定义了可以去重{key:val}
function arrUnique(arr, key) {
    var n = [arr[0]];
    for (var i = 0; i < arr.length; i++) {
        if (key == undefined) {
            n.indexOf(arr[i]) == -1 ? n.push(arr[i]) : "";
        } else {
            var flag = true;
            for (var j = 0; j < n.length; j++) {
                // 判断是数组的入口
                if (
                    typeof arr[i][key] == "undefined" &&
                    typeof n[j][key] == "undefined"
                ) {
                    n.indexOf(arr[i]) == -1 ? "" : (flag = false);
                } else {
                    if (
                        typeof arr[i][key] != "undefined" &&
                        arr[i][key] == n[j][key]
                    ) {
                        flag = false;
                        break; //已经判断有相同了可以跳出n循环了
                    }
                }
            }
            if (flag) {
                n.push(arr[i]);
            }
        }
    }
    return n;
}
var thenew = arrUnique([12, 3, 1, 12, 1, 5]); //[12, 3, 1, 5]
var thenew = arrUnique(
    [1, { id: "id", name: "jianxia" }, 3, 3, { id: "id", name: "zero" }, 1],
    "id"
); //[1,{"id":"id","name":"jianxia"},3]
console.log(JSON.stringify(thenew));
```

##### ES6 去重

```javascript
Array.from(new Set([1, 2, 1, 2, 3, 4, 5]));
```

##### 相邻同数组归类 eg: [1,1,3,2,2] = [[1,1], [3], [2,2]]

```javascript
let [allArray, setArray] = [[], []];
["a", "a", "c", "d", "d"].map((val, index, array) => {
    if (index !== 0 && val === array[index - 1]) {
        setArray.push(val);
        if (index === array.length - 1) {
            allArray.push(setArray);
        }
    } else {
        index !== 0 && allArray.push(setArray);
        setArray = [val];
        if (index === array.length - 1) {
            allArray.push(setArray);
        }
    }
});
allArray = [["a", "a"], ["c"], ["d", "d"]];
```
