# Lodop实现web套打

## 基础用法

[Lodop实现web套打](https://www.cnblogs.com/zh719588366/p/5058775.html)

## LodopFuncs.js

了解了Lodop的基本用法后。在OSS系统中，有我们自己对Lodop的封装（LodopFuncs.js）。

之后实现一个打印功能仅仅需要几行代码即可。
```javascript
function print () {
  initDefaultLodop()
  LODOP.PRINT_INIT("打印页面名称") // 打印页面名称
  // ... 在打印设计中生成的布局代码块
  Lodop_Print('P') // P:直接打印 S:打印设置 V:打印预览，一般不用
}
```

