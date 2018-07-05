title: 前端加载优化
speaker: Soyal
transition: vertical3d
theme: moon

[slide]

# 前端加载优化

[slide]

## 一次 SPA 的加载过程

- 1.打开页面: 发送 http 请求，请求 html 文件
- 2.首屏渲染: 解析 html 文件
- 3.首次内容渲染: 请求和加载 js
- 4.可交互: 组件初始化
- 5.内容加载完毕: 多媒体内容加载完毕

[slide]

## 打开页面->首屏渲染
##### 主要工作：请求html文件，解析html
<img src="/img/a2b.png" />

[slide]
[magic data-transition="cover-diamond"]
一般我们页面的html和相应的js
<pre>
<code class="html">
&lt;div id="root"&gt;&lt;div&gt;
</code>
</pre>

<pre>
<code class="javascript">
ReactDOM.render(&lt;App /&gt;, document.getElementById('root'))
</code>
</pre>
====
<p>
  在js下载和解析完毕之前，页面 完!全!空!白!
</p>
<img src="/img/a2b-1.png" />
====
可以稍作优化
<pre>
<code class="html">
&lt;div id="root"&gt;Loading...&lt;div&gt;
</code>
</pre>
====
当然最好的方式是画一个SVG
<pre>
<code class="html">
&lt;div id="root"&gt;
  &lt;!-- 画一个svg --&gt;
&lt;div&gt;
</code>
</pre>
====
利用html-webpack-plugin来自动插入svg
<pre>
<code class="javascript">
var HtmlWebpackPlugin = require('html-webpack-plugin');
var path = require('path');

// 读取写好的 loading 态的 html 和 css
var loading = {
    html: fs.readFileSync(path.join(__dirname, './loading.html')),
    css: '<style>' + fs.readFileSync(path.join(__dirname, './loading.css')) + '</style>'
}

var webpackConfig = {
  entry: 'index.js',
  output: {
    path: path.resolve(__dirname, './dist'),
    filename: 'index_bundle.js'
  },
  plugins: [
    new HtmlWebpackPlugin({
      filename: 'xxxx.html',
      template: 'template.html',
      loading: loading
    })
  ]
};
</code>
</pre>


[/magic]

[slide]
## 首屏渲染->首次内容渲染
##### 主要工作：下载和解析js代码
<img src="/img/b2c.png" />

[slide]
## js的组成
* 基础框架: 如 React、Vue 等，这些基础框架的代码是不变的，除非升级框架
* Polyfill: 对于使用了 ES2015+ 语法的项目来说，为了兼容性，polyfill 是必要的存在
* 业务基础库: 业务的一些通用的基础代码，不属于框架，但大部分业务都会使用到
* 业务代码: 特点是具体业务自身的逻辑代码