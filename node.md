[os](https://github.com/nodejs/node/blob/master/lib/os.js)

检查函数返回值
```js
function getCheckedFunction(fn) {
  return hideStackFrames(function checkError(...args) {
    const ctx = {};
    const ret = fn(...args, ctx);
    if (ret === undefined) {
      throw new ERR_SYSTEM_ERROR(ctx);
    }
    return ret;
  });
}
```

双层循环
```js
function cpus() {
  // [] is a bugfix for a regression introduced in 51cea61
  const data = getCPUs() || [];
  const result = [];
  let i = 0;
  while (i < data.length) {
    result.push({
      model: data[i++],
      speed: data[i++],
      times: {
        user: data[i++],
        nice: data[i++],
        sys: data[i++],
        idle: data[i++],
        irq: data[i++]
      }
    });
  }
  return result;
}
```

统计一个数的二进制表示方式1的个数
```js
function countBinaryOnes(n) {
  // Count the number of bits set in parallel, which is faster than looping
  n = n - ((n >>> 1) & 0x55555555);
  n = (n & 0x33333333) + ((n >>> 2) & 0x33333333);
  return ((n + (n >>> 4) & 0xF0F0F0F) * 0x1010101) >>> 24;
}
```