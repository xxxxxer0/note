# fis3

* ## 构建
```javascript
fis.match(reg,opt)

fis3 release ../output -d
```

* ## 调试
```
fis3 server start
fis3 server open
fis3 release -w
```

* ## 原理 
整个 FIS3 的构建流程大体概括分为三个阶段。
   1. 扫描项目目录拿到文件并初始化出一个文件对象列表
   2. 对文件对象中每一个文件进行单文件编译
   3. 获取用户设置的 package 插件，进行打包处理（包括合并图片）