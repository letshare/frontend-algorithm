## 一些有用的代码片段

### javascript

#### 检测代码运行时间太长
hack的方式
```javascript
(function detectLongFrame() {
  var lastFrameTime = Date.now();
  requestAnimationFrame(function() {
    var currentFrameTime = Date.now();

    if (currentFrameTime - lastFrameTime > 50) {
      // Report long frame here...
    }

    detectLongFrame(currentFrameTime);
  });
}()); 
```

更现代更好的方式
```javascript
const observer = new PerformanceObserver((list) => {
  for (const entry of list.getEntries()) {
    // `entry` is a PerformanceEntry instance.
    console.log(entry.entryType);
    console.log(entry.startTime); // DOMHighResTimeStamp
    console.log(entry.duration); // DOMHighResTimeStamp
  }
});

// Start observing the entry types you care about.
observer.observe({entryTypes: ['resource', 'paint']});
```

#### 如何优雅的实现金钱格式化：1234567890 --> 1,234,567,890

用正则魔法实现：
```javascript
var test1 = '1234567890'
var format = test1.replace(/\B(?=(\d{3})+(?!\d))/g, ',')

console.log(format) // 1,234,567,890
```

非正则的优雅实现：

```javascript
 function formatCash(str) {
       return str.split('').reverse().reduce((prev, next, index) => {
            return ((index % 3) ? next : (next + ',')) + prev
       })
}
console.log(formatCash('1234567890')) // 1,234,567,890
```

#### 使用reduce匹配圆括号
```javascript
//Returns 0 if balanced.
const isParensBalanced = (str) => {
return str.split('').reduce((counter, char) => {
if(counter < 0) { //matched ")" before "("
return counter;
    } else if(char === '(') {
return ++counter;
    } else if(char === ')') {
return --counter;
    }  else { //matched some other char
return counter;
    }

  }, 0); //<-- starting value of the counter
}
isParensBalanced('(())') // 0 <-- balanced
isParensBalanced('(asdfds)') //0 <-- balanced
isParensBalanced('(()') // 1 <-- not balanced
isParensBalanced(')(') // -1 <-- not balanced
```

#### 获得一个10位长度的随机字符串
```javascript
Math.random().toString(36).substr(2,10)
```

#### 评分
```javascript
function getRating(rating) {
    if(rating > 5 || rating < 0) throw new Error('数字不在范围内');
    return '★★★★★☆☆☆☆☆'.substring(5 - rating, 10 - rating );
}
```