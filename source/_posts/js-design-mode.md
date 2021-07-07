---
title: js-design-mode
date: 2021-07-06 15:26:55
tags: javascript
keywords: js 设计模式
---

```javascript
        // 代理模式
        var myImage = (function() {
            var imgNode = document.createElement('img')
            document.body.appendChild(imgNode)
            return {
                setSrc(src) {
                    imgNode.src=src
                }
            }
        })()


        var proxyImage = (function() {
            var img = new Image;
            img.onload = function() {
                myImage.setSrc(this.src)
            }
            return {
                setSrc(src) {
                    myImage.setSrc('https://img-blog.csdnimg.cn/20200330145320871.png')
                    img.src = src
                }
            }
        })()

        proxyImage.setSrc('https://img-blog.csdnimg.cn/2020033014534669.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjIwNzM1Mw==,size_16,color_FFFFFF,t_70')

        // 迭代器模式
        // bad
        var appendDiv = function (data) {
            for (var i = 0; i<data.length; i++) {
                var div = document.createElement('div')
                div.innerHTML = data[i]
                document.body.appendChild(div)
            }
        }

        appendDiv([1, 2, 3, 4])

        // good
        var each = function(target, callback) {
            var value,
                i=0,
                length = target.length
            if (Array.isArray(target)) {
                for (; i<length; i++) {
                    callback.call(target[i], i, target[i])
                }
            } else {
                for (i in target) {
                    callback.call(target[i], i, target[i])
                }
            }
        }
        var aD = function(data) {
            each(data, function(i, v) {
                var div = document.createElement('div')
                div.innerHTML = `${i}: ${v}`
                document.body.appendChild(div)
            })
        }

        aD([1, 2, 3, 4])
        aD({a: 1, b: 2})


        // 单例模式
        // bad
        var createModal = (function () {
            var modal
            return function () {
                if (!modal) {
                    modal = document.createElement('div')
                    modal.innerHTML = 'i am a modal 1'
                    modal.style.display = 'none'
                    document.body.appendChild(modal)
                }
                return modal
            }
        })()

        createModal()
        // good
        var getSingle = function(fn) {
            var result
            return function() {
                return result || (result = fn.apply(this, arguments))
            }
        }

        var onlyCreate = function() {
            var modal = document.createElement('div')
            modal.innerHTML = 'i am a modal 2'
            document.body.appendChild(modal)
            return modal
        }
        var createS = getSingle(onlyCreate)
        var singleModal1 = createS()
        var singleModal2 = createS()
        console.log(singleModal1 === singleModal2)


        // 策略

        // bad
        var calculateBonus = function(level, salary) {
            if (level === 'S') {
                return salary * 4
            }

            if (level === 'A') {
                return salary * 3
            }

            if (level === 'B') {
                return salary * 2
            }
        }
        calculateBonus('S', 10000)
        calculateBonus('A', 12000)

        // good
        var performanceS = function() {}
        performanceS.prototype.calculate = function(salary) {
            return salary * 4
        }

        var performanceA = function() {}
        performanceA.prototype.calculate = function(salary) {
            return salary * 3
        }

        var performanceB = function() {}
        performanceB.prototype.calculate = function(salary) {
            return salary * 2
        }

        var Bonus = function() {
            this.salary = null
            this.strategy = null
        }
        Bonus.prototype.setSalary = function(salary) {
            this.salary = salary
        }
        Bonus.prototype.setStrategy = function(strategy) {
            this.strategy = strategy
        }
        Bonus.prototype.getBonus = function(){ // 取得奖金数额
            return this.strategy.calculate( this.salary ) // 把计算奖金的操作委托给对应的策略对象
        }

        var bonus = new Bonus(); // 2
        bonus.setSalary( 10000 );
        bonus.setStrategy( new performanceS() ); // 设置策略对象

        console.log( bonus.getBonus() );

        bonus.setStrategy( new performanceA() ); // 设置策略对象
        console.log( bonus.getBonus() );

        // better
        var bonusMap = new Map[[
            'S', (salary) =>  salary * 4
        ], [
            'A', (salary) =>  salary * 3
        ], [
            'B', (salary) =>  salary * 2
        ]]
        bonusMap['S'](10000)
        bonusMap['A'](12000)
        
        // 发布-订阅模式
        // bad
        login.succ(function(data) {
            header.setAvatar(data)
            nav.refresh(data)
            message.refresh(data)
            cart.refresh(Data)
        })

        // good
        (function() {
            $.ajax('http://login/api', function(data) {
                login.trigger('success',data)
            })
        })()

        var header = (function() {
            login.listen('success', function(data){
                header.setAvatar(data)
            })
        })()

```
