---
title: vue3-proxy
date: 2021-09-17 15:54:03
tags:
---

### VUE3 初学

> 本次 vue3 学习主要针对两个点(哈哈，其实 80%内容也是来自 API)，第一个： proxy， 第二个：Composition API(函数组件)，其余 api 文档相关的就不学习太多，我觉得自己也不如 api 说得好，就好似 vue 最好的教程肯定不是去网上各种学习，而是看 api 文档，当遇到不懂的，再去搜一圈例子来理解一样。

#### copy api 的 vue3 重点变化

#### proxy

##### 了解 proxy 代理

> proxy 对象用于创建一个`对象的代理`，从而实现基本操作的拦截和自定义（如属性查找、赋值、枚举、函数调用等）

```javascript
// target 需要代理的目标对象, 可以是 任何类型的对象，包括原生数组，函数，甚至另一个代理
// handle 是以函数为属性的对象，用来定制拦截行文
const proxy = new Proxy(target, handle);
const origin = {};
const obj = new Proxy(origin, {
  get: function (target, propKey, receiver) {
    return "10";
  },
});

obj.a; // 10
obj.b; // 10
origin.a; // undefined
origin.b; // undefined
```

- handler 对象常用的方法
- has(), in 操作符的捕捉器 eg: 'a' in originProxy
- get(), 属性读取的捕捉器， eg: originProxy.a
- set(), 属性设置操作的捕捉器，eg: originProxy.a = '20'
- deleteProperty(), delete 操作符的捕捉器，eg: delete originProxy.a
- ownKeys(), Object.getOwnPropertyNames 和 Object.getOwnPropertySymbols 方法的捕捉器。eg:
- apply(), 函数在调用时捕捉器, eg: sumProxy(1, 2)
- construct(), new 操作符的捕捉器，eg: new sumProxy(1, 2)

##### 了解 vue3.0 之前使用的 defineProperty

> Object.defineProperty() 方法会直接在一个`对象上`定义一个`新属性`，或者修改一个对象的现有属性，并返回此对象。
> 划重点：`对象上，属性`，我们可以理解为是针对对象上的某一个属性做处理的

```javascript
let defineObj = {};
Object.defineProperty(defineObj, "a", {
  enumerable: true,
  configurable: true,
  set(val) {
    console.log("start set val", val);
  },
  get() {
    console.log("start get val");
    return "111";
  },
});
defineObj.b = "bbbb"; // 无
defineObj.a = "aaaaa"; // start set val aaaaa
console.log(defineObj.a); // start get val \n 111
```

> 所以 vue 里面对象新增字段双向绑定数据不更新的原因就很好理解了，因为 defineProperty 本身针对劫持的对象的属性，而非对象本身。

#### Composition API

> 为何要函数组件式编程
> ![图](http://static.zeroyh.cn/aaaaa.image)

- 更好的共享和重用代码，打包尺寸：每个函数都可作为 named ES export 被单独引入，对 tree-shaking 很友好；其次所有函数名和 setup 函数内部的变量都能被压缩，所以能有更好的压缩效率

之前我们的组件大概的样子是

```html
// str.vue
<template>
    <div>{{ infomation }}<div>
</template>

<script>
    export default {
        data () {
            return {
                infomation: ''
            }
        },
        craeted() {
            this.getInfo()
        },
        methods: {
            getInfo() {
                this.axios.get(GET_INFO).then(res=>{
                    this.infomation = res
                })
            }
        }
    }
</script>
```

那么如果父级页面需要获取 infomation 或者调用子组件的 getInfo 方法的时候，常用的有

- 父组件调用： let info = this.$refs.str.getInfo()
- 或者子组件触发回调 this.$emit('info', this.infomation)

现在可以用 setup 函数后改写下当前例子

> setup 函数在组件创建之前就会触发，

```html
// str.vue
<template>
    <div>{{ infomation }}<div>
</template>

<script>
    import { ref, onCreated } from 'vue'
    export default {
        setup() {
            let infomation = ref('')

            const getInfo = async () => {
                infomation = await this.axios.get(GET_INFO)
            }
            onCreated(getInfo)
            return {
                infomation,
                getInfo
            }
        }
    }
</script>
```

上面这个例子不能体现出 vue3 composition 的优势，但是能把一块逻辑统一到一块。这是个热身。

======高能预警了哈！======

列表分页查询方案
1）变量存储 (重复操作过多） 2) mixins (重复空间减少，命名空间冲突，特别是一个页面涉及 2 个的时候）

```html
<Page
  :total="pageData.total"
  :current="pageData.current"
  :pageSize="pageData.pageSize"
  :pageSizeOpts="pageData.pageSizeOpts"
  transfer
  show-elevator
  show-sizer
  show-total
  @on-change="pageChange"
  @on-page-size-change="pageSizeChange"
/>
```

```javascript
export default {
  data() {
    return {
      pageData: {
        total: 0,
        current: 1,
        pageSize: 10,
        pageSizeOpts: [10, 20, 30, 40],
      },
    };
  },
  methods: {
    pageChange(num) {
      this.pageData.current = num;
    },
    pageSizeChange(size) {
      this.pageData.pagesize = size;
    },
  },
};
```

上面代码里面的 pageData 和 methods 的方法，几乎是所有 page 引用都需要 CV 的代码

VUE3 下面就可以提取这块逻辑

```js
// hooks/page.js
import { reactive } from "vue";

export default function usePaging() {
  const conditions = reactive({
    total: 0,
    current: 1,
    pageSize: 10,
    pageSizeOpts: [10, 20, 30, 40],
  });
  const pageChange = (num) => {
    conditions.current = num;
  };
  const pageSizeChange = (size) => {
    conditions.pageSize = size;
  };
  return {
    conditions,
    pageChange,
    pageSizeChange,
  };
}
```

// 组件里面应用

```html
<Page
  :total="pageData.total"
  :current="pageData.current"
  :pageSize="pageData.pageSize"
  :pageSizeOpts="pageData.pageSizeOpts"
  transfer
  show-elevator
  show-sizer
  show-total
  @on-change="pageChange"
  @on-page-size-change="pageSizeChange"
/>
```

```javascript
import { usePage } from "hooks/page";
export default {
  setup() {
    const { conditions: pageData, pageChange, pageSizeChange } = usePage(); // 可监听变化

    watch([() => pageData.page, () => pageData.pageSize], ([val1, val2]) => {
      console.log("conditions changed，do search", val1, val2);
    });
    return { pageData, pageChange, pageSizeChange };
  },
};
```
