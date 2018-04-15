# vue_seller

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
## 安装better-scroll  
注意npm的命令执行，之前就是不记得npm i better-scroll -S  
[github地址](https://github.com/ustbhuangyi/better-scroll)  
## better-scroll使用  
在html标签中设置需要使用的标签。  
```html
<div class="menu-goods" ref="menuWrapper">
      <ul>
        <li v-for="good in goods" class="goods-li">
          <span class="goods-li-span">
            <span>{{good.name}}</span>
          </span>
        </li>
      </ul>
    </div>
```
这里调用this.menuScroll=new BScroll(this.$refs.menuWrapper,{});初始化后就会可以滚动了。  
![image](./wikiImage/betterScroll.PNG)  
就可以看到图中会添加样式了。  
better-scroll 的初始化时机很重要，因为它在初始化的时候，会计算父元素和子元素的高度和宽度，来决定是否可以纵向和横向滚动。因此，我们在初始化它的时候，必须确保父元素和子元素的内容已经正确渲染了。如果子元素或者父元素 DOM 结构发生改变的时候，必须重新调用 scroll.refresh() 方法重新计算来确保滚动效果的正常。所以同学们反馈的 better-scroll 不能滚动的原因多半是初始化 better-scroll 的时机不对，或者是当 DOM 结构发送变化的时候并没有重新计算 better-scroll。  
我们在 mounted 这个钩子函数里，this.$nextTick 的回调函数中初始化 better-scroll。this.$nextTick 是一个异步函数，为了确保 DOM 已经渲染  
Vue.js 提供了我们一个获取 DOM 对象的接口—— vm.$refs。
```js
this.menuScroll=new BScroll(this.$refs.menuWrapper,{});
```
this.$refs.foodsWrapper.getElementsByClassName("good-li-hood");通过这样获取到的html节点是一个htmlConlection的节点，并不是一个数组，所以不能使用forEach（）这样的函数来进行迭代。  
注意在使用列表index的时候可以这样获取index的值。<li v-for="(good,index) in goods" class="goods-li" :class="{'active':currentIndex===index}">  
在需要获取滚动的位置时，初始化时需要配置probeType为3，这样在设置滚动监听。代码如下
```js
this.foodsScroll=new BScroll(this.$refs.foodsWrapper,{
          probeType:3//能实时监听滚动的位置
        });
        this.foodsScroll.on("scroll",(pos)=>{
          this.scrollY=Math.abs(Math.round(pos.y));
        });
```
同样设置滚动条里的click事件也需要进行配置
```html
<div class="menu-goods" ref="menuWrapper">
      <ul>
        <li v-for="(good,index) in goods" class="goods-li" :class="{'active':currentIndex===index}" @click="selectMennu(index,$event)">
          <span class="goods-li-span">
            <span>{{good.name}}</span>
          </span>
        </li>
      </ul>
    </div>
```
```js
this.menuScroll=new BScroll(this.$refs.menuWrapper,{
          click:true
        });
```
[better-scroll还有一些其他实用的地方可以参考](https://juejin.im/post/59b777015188257e764c716f)
