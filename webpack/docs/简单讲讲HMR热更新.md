# 简单讲讲HMR热更新

## 什么是HMR

Hot Module Replacement，是指我们在对代码修改保存之后，webpack会对代码进行重新打包，并将新的模块发送到浏览器，浏览器用新的的模块替换掉旧的模块，这样就做到了不刷新浏览器让页面更新。