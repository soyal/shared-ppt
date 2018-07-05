title: 前端组件化分享
speaker: Soyal
transition: vertical3d
theme: light

[slide]
## outline
* 什么是前端组件化 {:&.moveIn}
* 前端组件化的意义 
* 私有库的意义 
* 怎么使用私有库 
[slide]
## not mentioned
* 详细的组件化思路
* 怎么搭建私有库

[slide style="background-image:url(/img/bg2.jpg)"]
# 什么是前端组件化——所谓的组件化，指的是什么?
[slide]
* 1.模块化的方式
* 2.针对目前技术栈诸如vue,react,preact等的模块化方式

[slide style="background-image:url(/img/bg2.jpg)"]
# 前端组件化的意义——为什么要做前端组件化
[slide]
## 代码复用

[slide]
## 我粘贴复制怎么就不行了？
![粘贴](/img/1-1.jpg)

[slide]
## 1.组件依赖问题
比如有这样的依赖树
* Editor
  - Noty {:&.moveIn}
  - Convert
  - Draft
[slide]
## 2.代码同步问题
比如发布了版本进行bug修复
* 1.0.1
  - improve: 提升了在低版本浏览器下的流畅性
* 1.0.2
  - fix: 修复了上个版本过于流畅的bug

[slide style="background-image:url(/img/bg2.jpg)"]
# 私有库的意义
我们需要一个仓库来存放组件

[slide]
## 为什么公共的npm仓库不能满足需求
* 公共仓库命名空间有限，不方便 {:&.moveIn}
* 公司内部使用的组件很可能带有公司的业务逻辑，不适合放在公共仓库

[slide]
## 私有库解决的问题
私有库并不是为了取代公共仓库而存在的，它只是公共仓库的一个功能补集
* 内部轮子的存放 {:&.moveIn}
* 修改了第三方源码，不方便提PR

[slide style="background-image:url(/img/bg2.jpg)"]
# 怎么使用私有库

[slide]
* 1.编写组件，怎么编写组件参考[这里](http://fe-doc.fishsaying.com/#/component-doc/index)
* 2.往私有库发布组件



```
npm publish --registry=http://npm.fishsaying.com
```
