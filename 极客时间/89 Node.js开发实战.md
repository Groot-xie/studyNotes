## 10丨模块：使用模块规范改造石头剪刀布游戏

```js
// 获取用户输入
// node ./index.js rock 
process.arg[process.arg.length - 1] // rock

// 保持运行状态
process.stdin.on('data', e => {
  var palyerAction = e.toString().trim()
  console.log(palyerAction)
  
  // 清除进程
  process.exit()
})
```

