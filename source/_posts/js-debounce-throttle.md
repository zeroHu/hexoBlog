---
title: js-debounce-throttle
date: 2020-05-13 17:47:28
tags: javascript
keywords: 节流，防抖，debounce，throttle，lodash节流防抖源码
---

### js 节流(throttle)与防抖（debounce)

#### 定义

-   防抖（debounce）: 一个事件不停的触发，防抖会再指定时间内没有再次触发后才执行一次。（应用场景：input 框联想：可以在用户停止输入 300ms 后再执行联想搜索）
-   节流（throttle）: 一个事件不停的触发，节流会每指定时间执行一次。（应用场景：图片懒加载：鼠标下滑，可以执行 300ms 执行一次，不用不停的执行。 拖拽窗口：拖动过程中没个 30ms 移动一次）

#### 区别

-   当事件持续被触发，如果触发时间间隔短于规定的等待时间（n 秒），那么函数防抖的情况下，函数将一直推迟执行，造成不会被执行的效果；函数节流的情况下，函数将每个 n 秒执行一次

#### 代码实现

> 防抖（debounce）

```javascript
/**
 * 常用版
 * @param {*} func, 回调函数
 * @param {*} wait, 防抖时间
 * */
function debounce(func, wait) {
    let timer
    return functin () {
        const context = this
        const args = arguments
        clearTimeout(timer)
        timer = setTimeout(() => func.apply(context, args), wait)
    }
}

/**
 * 复杂版 有立即执行的函数
 * @param {*} func, 回调函数
 * @param {*} wait, 防抖时间
 * @param {*} immediate, 是否立即执行一次
 */
function debounce(func, wait, immediate) {
    var timeout;
    return function executedFunction() {
        var context = this;
        var args = arguments;

        var later = function () {
            timeout = null;
            if (!immediate) func.apply(context, args);
        };
        var callNow = immediate && !timeout;

        clearTimeout(timeout);
        timeout = setTimeout(later, wait);

        if (callNow) func.apply(context, args);
    };
}
```

> 节流（throttle)

```javascript
/**
 * @param {*} func 回调函数
 * @param {*} limit 每limit时间内只执行一次
 */
function throttle(func, limit) {
    let inThrottle;
    return function () {
        const context = this;
        const args = arguments;
        if (!inThrottle) {
            func.apply(context, args);
            inThrottle = true;
            setTimeout(() => (inThrottle = false), limit);
        }
    };
}
```

#### lodash 源码

> 防抖(debounce)

```javascript
function isObject(value) {
    const type = typeof value;
    return value != null && (type === "object" || type === "function");
}

function debounce(func, wait, options) {
    let lastArgs, lastThis, maxWait, result, timerId, lastCallTime;

    let lastInvokeTime = 0;
    let leading = false;
    let maxing = false;
    let trailing = true;

    //  Bypass `requestAnimationFrame` by explicitly setting `wait=0`.
    //  root 参考https://github.com/lodash/lodash/blob/master/.internal/root.js
    const useRAF =
        !wait && wait !== 0 && typeof root.requestAnimationFrame === "function";

    if (typeof func !== "function") {
        throw new TypeError("Expected a function");
    }
    wait = +wait || 0;
    if (isObject(options)) {
        leading = !!options.leading;
        maxing = "maxWait" in options;
        maxWait = maxing ? Math.max(+options.maxWait || 0, wait) : maxWait;
        trailing = "trailing" in options ? !!options.trailing : trailing;
    }

    function invokeFunc(time) {
        const args = lastArgs;
        const thisArg = lastThis;

        lastArgs = lastThis = undefined;
        lastInvokeTime = time;
        result = func.apply(thisArg, args);
        return result;
    }

    function startTimer(pendingFunc, wait) {
        if (useRAF) {
            root.cancelAnimationFrame(timerId);
            return root.requestAnimationFrame(pendingFunc);
        }
        return setTimeout(pendingFunc, wait);
    }

    function cancelTimer(id) {
        if (useRAF) {
            return root.cancelAnimationFrame(id);
        }
        clearTimeout(id);
    }

    function leadingEdge(time) {
        // Reset any `maxWait` timer.
        lastInvokeTime = time;
        // Start the timer for the trailing edge.
        timerId = startTimer(timerExpired, wait);
        // Invoke the leading edge.
        return leading ? invokeFunc(time) : result;
    }

    function remainingWait(time) {
        const timeSinceLastCall = time - lastCallTime;
        const timeSinceLastInvoke = time - lastInvokeTime;
        const timeWaiting = wait - timeSinceLastCall;

        return maxing
            ? Math.min(timeWaiting, maxWait - timeSinceLastInvoke)
            : timeWaiting;
    }

    function shouldInvoke(time) {
        const timeSinceLastCall = time - lastCallTime;
        const timeSinceLastInvoke = time - lastInvokeTime;

        // Either this is the first call, activity has stopped and we're at the
        // trailing edge, the system time has gone backwards and we're treating
        // it as the trailing edge, or we've hit the `maxWait` limit.
        return (
            lastCallTime === undefined ||
            timeSinceLastCall >= wait ||
            timeSinceLastCall < 0 ||
            (maxing && timeSinceLastInvoke >= maxWait)
        );
    }

    function timerExpired() {
        const time = Date.now();
        if (shouldInvoke(time)) {
            return trailingEdge(time);
        }
        // Restart the timer.
        timerId = startTimer(timerExpired, remainingWait(time));
    }

    function trailingEdge(time) {
        timerId = undefined;

        // Only invoke if we have `lastArgs` which means `func` has been
        // debounced at least once.
        if (trailing && lastArgs) {
            return invokeFunc(time);
        }
        lastArgs = lastThis = undefined;
        return result;
    }

    function cancel() {
        if (timerId !== undefined) {
            cancelTimer(timerId);
        }
        lastInvokeTime = 0;
        lastArgs = lastCallTime = lastThis = timerId = undefined;
    }

    function flush() {
        return timerId === undefined ? result : trailingEdge(Date.now());
    }

    function pending() {
        return timerId !== undefined;
    }

    function debounced(...args) {
        const time = Date.now();
        const isInvoking = shouldInvoke(time);

        lastArgs = args;
        lastThis = this;
        lastCallTime = time;

        if (isInvoking) {
            if (timerId === undefined) {
                return leadingEdge(lastCallTime);
            }
            if (maxing) {
                // Handle invocations in a tight loop.
                timerId = startTimer(timerExpired, wait);
                return invokeFunc(lastCallTime);
            }
        }
        if (timerId === undefined) {
            timerId = startTimer(timerExpired, wait);
        }
        return result;
    }
    debounced.cancel = cancel;
    debounced.flush = flush;
    debounced.pending = pending;
    return debounced;
}
```

> 节流(throttle)

```javascript
function throttle(func, wait, options) {
    let leading = true;
    let trailing = true;

    if (typeof func !== "function") {
        throw new TypeError("Expected a function");
    }
    if (isObject(options)) {
        leading = "leading" in options ? !!options.leading : leading;
        trailing = "trailing" in options ? !!options.trailing : trailing;
    }
    // 上方的debounce函数
    return debounce(func, wait, {
        leading,
        trailing,
        maxWait: wait,
    });
}

export default throttle;
```
