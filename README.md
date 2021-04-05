# e-commerce
e-commerce platform 
精美商城开发日志

目标：利用uniapp和tp6.0 PHP或laravel框架，开发全栈多端电子商城项目，需要涵盖商城的大部分功能，前端要同时开发出：H5 微信小程序 APP（安卓、IOS）以及其他平台小程序（支付宝/百度/头条/QQ/钉钉/淘宝）

新建 common 目录，拷贝官方UI库：uni.css到该目录

下载动画库：$ npm install animate.css --save，效果演示地址：https://animate.style/
把animate.css拷贝到common目录common目录

在在common目录common目录建立图标库文件 icon.css
在common目录建立自己的公共样式文件common.css

在App.vue中，引入这四个样式
	/* 官方ui库 */
	@import "/common/uni.css";
	/* 第三方动画库 */
	@import "/common/animate.css";
	/* 自定义图标库 */
	@import "/common/icon.css";
	/* 公共样式 */
	@import "/common/common.css";
	
	粘贴uni.tff文件到static文件夹
	
	到阿里巴巴的矢量图标库：https://www.iconfont.cn/
	调用方法： class="iconfont icon-icon-test25""
	
	在common.css里面设置全局样式：高度100% 默认字体：28rpx 行高：1.8
	page{
		height: 100%;
		font-size: 28rpx;
		line-height: 1.8;
		background-color:  #FFFFFF;
	
	}
	图片默认宽度：100%
	主色调为橙色
.main-bg-color{background: #FD6801;}
主点击背景色（淡橙色）
.main-bg-hover-color{background: rgba(253,104,1,0.8);}
/* 主字体颜色 */
.main-text-color{color: #FD6801;}
/* 主边框颜色 */
main-border-color{border-color: #F1F1F1;}

从阿里巴巴的矢量图标库：https://www.iconfont.cn/制作4套底部导航图标，大小为 88*88

在pages.json中配置底部导航 "tarBar":{}

封装常用的ui库

在static目录下建font目录，把字体图标文件iconfont.ttf文件拷贝到此处,用unicode
原生导航栏，按钮的图标需要用到：text

开发主页，
轮播图：快捷键：uswiper

轮播图中的图片，最好设置成固定的宽度：style="height: 350rpx;"，设置成 mode =“widthFix”，加载的时候会有跳动

轮播图加入 circular 保证衔接滑动

把这个轮播图封装成组件，建立一个components 文件夹

通过uni-app的easycom： 将组件引入精简为一步。只要组件安装在项目的 components 目录下，并符合 components/组件名称/组件名称.vue 目录结构。就可以不用引用、注册，直接在页面中使用。
index-swiper.vue组件

封装图标分类导航，使用常用ui库的span-4{ width: 20%;} ，可以把图标分类哦成一行5列

全局组件可在 main.js中引入

开发封装全局分割线

逐步开发card组件，以后逐步完善，为开发做好准备，先做好大图广告功能

采用单标签，替代双标签，更加简便

由于价格的样式用的地方比较多，所以就封装成价格组件price组件中的props price  用法 <price price="1699"/>,不好看，可以采用slot的方法，不用price属性
这样，调用的时候：<price>1688</price>即可

要想让scroll-view组件正常显示，需要加一个.scroll-row{ width: 100%;white-space: nowrap; }的样式
在循环体中加：.scroll-row-item{ display: inline-block; } 的样式

scroll-view的 scroll-into-view 属性，要现在子组件加id属性，然后点击该子组件，可以让该子组件滚动到组件前面

NVUE---原生的vue组件，用于app端，其他端不用，uni-app App端内置了一个基于 weex 改进的原生渲染引擎，提供了原生渲染能力。

nvue 页面结构同 vue, 由 template、style、script 构成。

template： 模板写法、数据绑定同 vue。组件支持2种模式，
weex 组件，同weex写法，参考：weex 内置组件：https://weex.apache.org/zh/docs/components/a.html；
uni-app组件，同uni-app写法。
App端nvue专用组件，详见https://uniapp.dcloud.io/component/barcode。
style：由于采用原生渲染，并非所有浏览器的 css 均支持，布局模型只支持 flex 布局，虽然不会造成某些界面布局无法实现，但写法要注意。详见：样式
script：写法同 vue，并支持3种API：
nvue API ：仅支持App端，uni-app编译模式也可使用。使用前需先引入对应模块，参考：模块引入API
uni API：https://uniapp.dcloud.io/api/README
plus API：仅支持App端。http://www.html5plus.org/doc/h5p.html
3.调试 nvue 页面

nvue开发与vue开发的常见区别：

基于原生引擎的渲染，虽然还是前端技术栈，但和web开发肯定是有区别的。

1.nvue 页面控制显隐只可以使用v-if不可以使用v-show
2.nvue 页面只能使用flex布局，不支持其他布局方式。页面开发前，首先想清楚这个页面的纵向内容有什么，哪些是要滚动的，然后每个纵向内容的横轴排布有什么，按 flex 布局设计好界面。
3.nvue 页面的布局排列方向默认为竖排（column），如需改变布局方向，可以在 manifest.json -> app-plus -> nvue -> flex-direction 节点下修改，仅在 uni-app 模式下生效。详情。
4.nvue页面编译为H5、小程序时，会做一件css默认值对齐的工作。因为weex渲染引擎只支持flex，并且默认flex方向是垂直。而H5和小程序端，使用web渲染，默认不是flex，并且设置display:flex后，它的flex方向默认是水平而不是垂直的。所以nvue编译为H5、小程序时，会自动把页面默认布局设为flex、方向为垂直。当然开发者手动设置后会覆盖默认设置。
5.文字内容，必须、只能在<text>组件下。不能在<div>、<view>的text区域里直接写文字。否则即使渲染了，也无法绑定js里的变量。
6.只有text标签可以设置字体大小，字体颜色。
7.布局不能使用百分比、没有媒体查询。
8.nvue 切换横竖屏时可能导致样式出现问题，建议有 nvue 的页面锁定手机方向。
9.支持的css有限，不过并不影响布局出你需要的界面，flex还是非常强大的。详见
10.不支持背景图。但可以使用image组件和层级来实现类似web中的背景效果。因为原生开发本身也没有web这种背景图概念
11.css选择器支持的比较少，只能使用 class 选择器。详见
12.nvue 的各组件在安卓端默认是透明的，如果不设置background-color，可能会导致出现重影的问题。
13.class 进行绑定时只支持数组语法。
14.Android端在一个页面内使用大量圆角边框会造成性能问题，尤其是多个角的样式还不一样的话更耗费性能。应避免这类使用。
15.nvue页面没有bounce回弹效果，只有几个列表组件有bounce效果，包括 list、recycle-list、waterfall。
16.原生开发没有页面滚动的概念，页面内容高过屏幕高度并不会自动滚动，只有部分组件可滚动（list、waterfall、scroll-view/scroller），要滚得内容需要套在可滚动组件下。这不符合前端开发的习惯，所以在 nvue 编译为 uni-app模式时，给页面外层自动套了一个 scroller，页面内容过高会自动滚动。（组件不会套，页面有recycle-list时也不会套）。后续会提供配置，可以设置不自动套。
17.在 App.vue 中定义的全局js变量不会在 nvue 页面生效。globalData和vuex是生效的。
18.App.vue 中定义的全局css，对nvue和vue页面同时生效。如果全局css中有些css在nvue下不支持，编译时控制台会报警，建议把这些不支持的css包裹在条件编译里，APP-PLUS-NVUE
19.不能在 style 中引入字体文件，nvue 中字体图标的使用参考：加载自定义字体。如果是本地字体，可以用plus.io的API转换路径。
20.目前不支持在 nvue 页面使用 typescript/ts。
21.nvue 页面关闭原生导航栏时，想要模拟状态栏，可以参考文章。但是，仍然强烈建议在nvue页面使用原生导航栏。nvue的渲染速度再快，也没有原生导航栏快。原生排版引擎解析json绘制原生导航栏耗时很少，而解析nvue的js绘制整个页面的耗时要大的多，尤其在新页面进入动画期间，对于复杂页面，没有原生导航栏会在动画期间产生整个屏幕的白屏或闪屏。

注意事项
nvue的css仅支持flex布局，是webview的css语法的子集。这是因为操作系统原生排版不支持非flex之外的web布局。当然flex足以排布出各种页面，只是写法需要适应。
在选择器方面支持的较少，只支持简单的class="classA"。
class 进行绑定时只支持数组语法。
不支持媒体查询
不支持 class 以外的选择器
不支持组合选择器（3.1.0+ 开始支持）
不支持简写样式（3.1.0+ 开始支持）
不能在 style 中引入字体文件
布局不能使用百分比，如width：100%；
有些web的css属性在nvue里无法支持，比如背景图。但可以使用image组件和层级来实现类似web中的背景效果。因为原生开发本身也没有web这种背景图概念
nvue 的各组件在安卓端默认是透明的，如果不设置background-color，可能会导致出现重影的问题
文字内容，必须只能在text组件下，text组件不能换行写内容，否则会出现无法去除的周边空白
只有text标签可以设置字体大小，字体颜色


单位只支持px，不支持em，rem，pt，%。upx
宽度问题：750px = 100% 高：1250px=100%
每个元素都是默认flex布局，所以可以直接用flex的特性
不能合着写
背景只能：background-color
选择器只支持单类
引用 要用：<style src="@/commom/nvue-common.css"></style>
text组件里面不可以有空格或者换行，否则会渲染到页面

WEEX的轮播图slide中的样式，必须写在当前文件之内，引入的方式无法使用

nvue的样式导入，必须用 <style src="@/common/zlx-main-nvue.css"></style> 方式

nvue的样式，不支持 !important

ES6模板对象，Template Literals（模板对象） in ES6，在字符串中输出变量

ES5：
var name = 'Your name is ' + first + ' ' + last + '.';
var url = 'http://localhost:3000/api/messages/' + id;

在ES6中，以使用新的语法$ {NAME}，并把它放在反引号里：
ar name = `Your name is ${first} ${last}. `;
var url = `http://localhost:3000/api/messages/${id}`

不用拼接字符串

WEEX 的slider组件，之中加入 list组件后，导致list组件不上下滚动，，需要在slider中及爱如高度属性，class=“flex-1” 加入固定高度都不管用，真实个坑

排序，升降的两个上下三角 之间的间距，通过行高来调节：
.line-h05{ line-height: 0.4!important; }

在flex布局 纵向排列 column下，某一子元素采用.mb-auto { margin-bottom: auto;}，可以让元素下面往下移动

上面是图片，下面是文字，把文字设置成 d-block 即可

API-节点信息：uni.createSelectorQuery()，应该在生命周期，onReady的时候调用,onLoad的时候，节点不一定出来
const query = uni.createSelectorQuery().in(this);
query.select('#id').boundingClientRect(data => {
  console.log("得到布局位置信息" + JSON.stringify(data));
  console.log("节点离页面顶部的距离为" + data.top);
}).exec();

《scroll-view组件中的 scroll-top	Number		设置竖向滚动条位置，

分类页中，右边滚动的时候，要左边随着滚动，这个方法要写在 监听左边激活项： activeIndex 改变的时候发生，而不是写在右边</scroll-view>的组件的滚动事件之中(@scroll="onRightScroll),因为右边可能滚动很长的距离，才可以使左边的索引发生改变，卸载那里会出现很多次的请求

//query.selectAll('#left').boundingClientRect查询节点的布局位置 ，query.selectAll('#left').fields 获取节点的相关信息。第一个参数是节点相关信息配置（必选）；第二参数是方法的回调函数，参数是指定的相关节点信息

this.$nextTick 用在onLoad 生命周期，要等到onLoad()的下一个生命周期，就是onReady()的时候执行

style="lines:1;" 限制1行"

.d-block{ display: block; } 可以让两个文本上下排列
<text class="font-md">{{item.username}}</text>
<text class="d-block text-light-muted">{{item.create_time}}</text>

在flex布局中，使用左边自动样式，可以把本组件推向最左边
ml-auto .ml-auto { margin-left: auto;}

富文本解析插件：detail页面引入
// uParse插件说明地址:https://ext.dcloud.net.cn/plugin?id=364
import uParse from '@/components/gaoyia-parse/parse.vue'
	export default {
		components:{
			uParse
		},
		data() {
			return {
				article:'<p style="color:red">html代码</p>',
				
去掉富文本图片之间的间距 padding，到浏览器找到其上级的css，调节为0
.wxParse .p{ padding: 0!important; }
.wxParse view,.wxParse uni-view{ line-height: 0!important; }

CSS类选择器之间有空格和无空格的区别：1、有空格，为子节点，2、无空格选择到同时拥有.class1和.class2的节点空格选择到同时拥有.class1和.class2的节点：.class1.class2 { color: blue; }  <div class="class1 class2">I'm class1class2,son of class1</div>

newList(state){
					 return state.list.filter(v=>v.status)

console.log(JSON.stringify(this.newList)) 只返回status为true的元素 [{"id":2,"name":"商品二","status":true}]

Vuex在使用了模块后，数据归纳到了 以模块名为键值的json数据
console.log(JSON.stringify(this.$store.state.cart.list   cart为模块名

)
{"cart":{"number":1,"list":[{"id":1,"name":"商品一","status":false,"num":1},{"id":2,"name":"商品二","status":true,"num":10},{"id":3,"name":"商品三","status":false,"num":15},

所以采用模块后取值要his.$store.state.cart.list   cart为模块名

模块对：getters mutations actions 没有影响

不用<radio-group >  <radio :value="item.value" :checked="index === current" /> 就可以当作多选来用

flex布局，左侧是图，右侧是文字，为了防止右侧文字变长后，挤压左侧的图片，就给左侧加入：.flex-shrink{flex-shrink: 0;}，这样就不会被挤压

getters:{//此处为计算属性，购物车多用计算属性，可以节省很多代码

组件中的模板：	<slot name="title">
				<text v-if="headTitle" class="font-md " :class="headTitleWeight ? 'font-weight' : '' ">{{headTitle}}</text>
			</slot>
						
			如果用到 title 插槽，则是添加的插槽的内容，
			如果不用 title 插槽，则默认内容是：<text v-if="headTitle" class="font-md " :class="headTitleWeight ? 'font-weight' : '' ">{{headTitle}}</text>
			
slot 的默认值 终于理解了！
switch组件通过change方法，来传递是否被选中的值
change返回的参数，$event，为点击开罐按钮后返回来的值
<switch
 :checked="form.isdefault" class="ml-auto" color="#FD6801" @change="form.isdefault = $event，为点击开罐按钮后返回来的值.detail.value"></switch>	
 
 //修改收货地址，难点 {index,item}为解够赋值，传来的对象必须是{index:   ,  item:   ,}
 updatePath(state,{index,item}){
 	for(let key in item){
 		//此处是重点，不这样写，数据修改不过来
 		state.list[index][key] = item[key]
 	}
 }
 
 <uni-swipe-action>
 	<uni-swipe-action-item    组件：
	left-options="options" :right-options="options" 为滑动后出现的菜单：
	options: [{
			text: '修改',
			style: {
				backgroundColor: '#007aff'
			}
		},
		{
			text: '删除',
			style: {
				backgroundColor: '#dd524d'
			}
		}
	]
	
	 @click="bindClick($event.index === 0 为左侧按钮 1 为右侧按钮,index)
	 $event.index === 0 为左侧按钮 1 为右侧按钮
	 
	 //最好演示50ms之后再跳转，可以<uni-swipe-action> 滑动选项收回去
	 uni.navigateTo({
	 	url:'../user-path-edit/user-path-edit?data='+obj
		
		:class 中放两个变量 样式名，中间要用空格 ：
		<view class="d-flex line-h" :class="priceSize + ' ' +color">
		
优化首次加载白屏问题，这个是因为uniapp本身的性能导致的，利用nvue就可以避免app端这个问题。

现行解决方法是，在页面的上层，放置一个“加载中...”的提示，在inReady之后，再隐藏这个层

可以利用mixin混入对象，开发全局组件组件，
步骤：
1、在common下建立mixin目录，
创建：loading.js ，和loading-plus.vue文件，loading.js导出变量，已经onReady的状态
2、在main.js中引入loading-plus模板，并注册成全局变量
import loadingPlus from "@/common/mixin/loading-plus.vue"
Vue.component('loading-plus',loadingPlus)
3、在用到白屏组件的页面，引入loading.js ，并在代码的上层，使用loading-plus组件
4、在该页面注册： mixins:[loading],这样的话，在本页面找不到的变量和方法，都会去loading中优先寻找

在页面加入动画，效果更好：class="animated fadeIn faster" 

<!-- <navigator url="../order-coupon/order-coupon"> uni-list-item组件内部有link 和to属性，点击方法失效-->
