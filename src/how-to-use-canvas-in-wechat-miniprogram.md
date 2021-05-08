在使用微信小程序开发中，有的需求场景中会需要用户手写签名、或者绘制一些路径，通常会使用 canvas 来实现这种需求

在小程序的开发[官方文档](https://developers.weixin.qq.com/miniprogram/dev/component/canvas.html)中我们可以查找到相关的 canvas 接口使用方法，在文档中我们看到微信官方的提示

> 2.9.0 起支持一套新 Canvas 2D 接口（需指定 type 属性），同时支持[同层渲染](https://developers.weixin.qq.com/miniprogram/dev/component/native-component.html#原生组件同层渲染)，原有接口不再维护。相关api：[获取 canvas 实例](https://developers.weixin.qq.com/miniprogram/dev/api/canvas/Canvas.html)。

而官方文档中的说明也确实是旧版的 canvas 文档，那么在本文中将详细介绍一下新版和旧版的 canvas 绘制签名的方法

在本例中，使用了小程序的开发框架 [mpx](https://github.com/didi/mpx)， `mpx` 使用的是微信小程序原生的标签和语法，因此，可以直接将代码复制到项目中进行使用。

## 使用旧版的 Canvas 接口

介绍一下如何使用旧版的小程序 canvas 接口

1. 首先在页面中添加一个 canvas 容器，并添加上相应的时间监听和处理函数

   ```html
   <view class="main">
     <canvas canvas-id="custom-canvas" class="canvas" bindtouchstart="onStart" bindtouchmove="onMove" bindtouchend="onEnd"></canvas>
   </view>
   ```

   需要注意的是：此处不能在 canvas 的元素中添加 type="2d"，如果添加了该属性，则小程序将会把此 canvas 解析为新版本的 `canvas2D`

2. 在脚本中添加处理函数

   ```js
   <script>
   import { createPage } from '@mpxjs/core'
   let ctx
   
   createPage({
     data: {},
     methods: {
       onStart(e) {
         console.log(e)
         const [touch] = e.touches
         const { x, y } = touch
         ctx.moveTo(x, y)
       },
       onMove(e) {
         const [touch] = e.touches
         const { x, y } = touch
         const point = { x, y }
         this.draw(point)
       },
       draw(point) {
         ctx.lineTo(point.x, point.y)
         ctx.stroke()
         ctx.draw(true)
         ctx.moveTo(point.x, point.y)
       },
       onEnd() {
         console.log('Draw end')
       },
       init() {
         ctx = wx.createCanvasContext('custom-canvas', this)
         ctx.setStrokeStyle('#00ff00')
         // 设置线的宽度
         ctx.setLineWidth(5)
         // 设置线两端端点样式更加圆润
         ctx.setLineCap('round')
         // 设置两条线连接处更加圆润
         ctx.setLineJoin('round')
       }
     },
     onLoad() {
       this.init()
     }
   })
   </script>
   ```

   此处需要注意的是：

   - 由于不需要将 canvas 的实例在模板中使用，因此此处将 `ctx` 声明为了局部变量

   - 使用旧版的 canvas 接口，我们可以将初始化过程放在页面挂载的 `onLoad` 事件中，在初始化过程中通过 `wx.createCanvasContext`方法创建 canvas 实例，使用框架的时候需要将 `this` 值作为第二个参数传入 `wx.createCanvasContext` 方法中，否则获取不到 canvas 的实例

   - 在 `touchstart` 事件开始的时候，我们需要获取到触摸的起始位置，也就是通过事件中的 `touches`，该属性返回点击的位置数组，此时我们将 canvas 的起始位置设置到点击位置

     ```js
     const [touch] = e.touches
     const { x, y } = touch
     ctx.moveTo(x, y)
     ```

   - 在处理绘制事件的时候，我们一定要按照 `lineTo() > stroke() > draw() > moveTo()` 的方式来绘制，有的同学就会说了，为什么要再添加一个 `moveTo()` 呢？我们以动图表现一下0-0

     **没有使用 `moveTo()`的情况：**

     ![](http://cdn.ruxf.com/static/20210508162203-2G1ctm.gif)

     图中可以看出如果我们移动的过快，就会出现虚线的点

     **添加了 `moveTo()`的效果:**

     ![](http://cdn.ruxf.com/static/20210508162729-qY1GZw.gif)

   - 该旧版接口目前微信小程序已经不再继续维护了，但是如果要适配 `v2.9.0` 之前的微信版本基础库的话，就需要使用旧版的接口了

3. 设置画布的大小，此处我设置了整个屏幕的大小

   ```css
   <style lang="stylus">
   .canvas {
     width 100vw
     height 100vh
     background-color red
   }
   </style>
   ```

   

## 使用新版的 canvas

微信小程序中新版的 canvas 是基于 Web 标准的 canvas2D 来做渲染的，因此相关的接口文档可以从 MDN 中的 [canvas2D](https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D) 章节中来查看

下面就介绍一下如何使用 canvas2D 来实现签名

1. 同样的添加 canvas 容器元素

   ```html
   <view class="wrapper">
       <canvas
         wx:ref="SIGNATURE"
         class="signature"
         disable-scroll="{{true}}"
         bindtouchstart="onStart"
         bindtouchmove="onMove"
         bindtouchend="onEnd"
         bindtap="oMouseDown"
         type="2d"
       >
       </canvas>
     </view>
   ```

   注意：此处的 canvas 容器添加了 `type="2d"` 属性，来声明使用的是新版的 canvas2D

2. 实例化 canvas 实例

   ```js
   import { createPage } from '@mpxjs/core'
   let context
   
   createPage({
     data: {
       listData: ['手机', '电视', '电脑']
     },
     properties: {
       orders: Array
     },
     methods: {
       /**
        * 绘制签名
        */
       onStart(e) {
         console.log(e)
         const [touch] = e.touches
         const { x, y } = touch
         context.moveTo(x, y)
       },
       onMove(e) {
         const [touch] = e.touches
         const { x, y } = touch
         const point = { x, y }
         this.draw(point)
       },
       cancel(e) {},
       tap(e) {},
       error(e) {},
       onEnd(e) {
         this.triggerEvent('signature-touch-end')
       },
       draw(point) {
         context.lineTo(point.x, point.y)
         context.stroke()
         context.moveTo(point.x, point.y)
       },
       init() {
         this.$refs.SIGNATURE.node((result) => {
           const canvas = result.node
           context = canvas.getContext('2d')
           const { windowHeight, windowWidth, pixelRatio: dpr } = wx.getSystemInfoSync()
           canvas.width = windowWidth * dpr
           canvas.height = windowHeight * dpr
           context.strokeStyle = 'red'
           context.lineWidth = 5
           context.fillStyle = 'rgba(255, 255, 255, 0)'
           context.scale(dpr, dpr)
         }).exec()
       }
     },
     ready() {
       this.init()
     }
   })
   ```

   对以上代码做一下简单说明：

   - 由于 canvas2D 的实例需要获取到 canvas 的容器元素，因此我们最早只能在页面 `onReady` 中调用初始化函数，如果在 `onLoad` 或者 `onShow` 中调用该函数，则无法获取到 canvas 容器元素

   - 初始化函数中的 `this.$refs.SIGNATURE`是 `mpx` 对小程序的获取元素方法 `wx.createSelectorQuery()`的包装，因此这里完全可以使用小程序原生的方法获取到 canvas 容器

   - canvas2D 的使用需要显式的设置宽和高，小程序中的 canvas 默认为 `300 * 150`的大小，因此在这里我首先获取了整个可用屏幕的大小，然后适配为设备屏幕的 `dpr`，并对画布进行缩放，这样会对 canvas 的展示效果具体到每一个像素，这也是**终极画布**的奥秘

   - 触摸开始的时候和旧版的canvas 接口是一样的，需要 `moveTo` 到起始点

   - 在 canvas2D 绘制的时候和旧版的 canvas 不同：canvas2D 只需要 `lineTo() > stroke() > moveTo()` 即可，不需要显式的调用 `draw()` 方法，如下图动图中显式的效果，要不旧版的 canvas 更为细腻

     ![](http://cdn.ruxf.com/static/20210508165816-XcvSoK.gif)

3. 设置画布容器的宽高

   ```css
   .wrapper {
     width 100vw
     height 100vh
     display flex
     justify-context center
     align-items center
   }
   .signature {
     width 100vw
     height 100vh
     margin:0 auto
   }
   ```

   注意：此处设置的 canvas 元素的宽高和实例化 canvas 时候的宽和高不一样，这里可以认为仅仅只是一个容器，而实例中的宽和高才是画布的宽高

## 其他

canvas2D 和 小程序的 canvas 旧版接口中，还提供了清除画布、生成图片等方法，在本文中我们仅展示画布的绘制部分，想要做更深功能的话可以查阅相关文档即可