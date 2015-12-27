# sass compass images sprites combines hotcss

## Usage  

```准备
1. 需要先安装sass和compass[安装教程](http://www.w3cplus.com/sassguide/install.html)
2. [mac上ruby安装的教程](http://itcourses.cs.unh.edu/assets/docs/704/reports/fall11/Ruby%20on%20Rails%20Tutorial%20-%20Eric%20Callan.pdf)
```

```bash
> git clone https://github.com/liuyan5258/compass-images-sprites.git
> cd compass-images-sprites
> compass watch
```  

```show
1. 放入icons文件中的图标会自动合并在icons-*.png中，期间不需要做任何操作
2. 在px2rem.scss中有px转换成rem的计算
	
			@function px2rem( $px ){
			  @return $px / 1px *320/$designWidth/20 + rem;
			}

3. 在screen.scss中代码

			// use hotcss radio
			@import 'px2rem';

			// this is psd width
			$designWidth: 750;

			@import "../images/icons/*.png";

			// if you need all icon
			// @include all-icons-sprites;

			// if you need single icon
			nav{
				li.contact{
					@include icons-sprite(contact);
				}
			}

			nav{
				li.contact:hover{
					@include icons-sprite(contact);
				}
			}

			// if you need set icon width and height
			nav{
				li.contact{
					@include icons-sprite(contact);
					width: px2rem(icons-sprite-width(contact));
					height: px2rem(icons-sprite-height(contact));
				}
			}

3. 自动编译后在css中的样子

			.icons-sprite, nav li.contact, nav li.contact:hover { background-image: url('/images/../images/icons-s93de69cda4.png'); background-repeat: no-repeat; }

			nav li.contact { background-position: 0 0; }

			nav li.contact:hover { background-position: 0 0; }

			nav li.contact { background-position: 0 0; width: 0.68267rem; height: 0.68267rem; }

4. 如何你用了hotcss来做页面的适配，需要在你用到的html中加入以下代码：

			<!--引入hotcss.js-->
			<script>
			  (function(window,document){(function(){var viewportEl=document.querySelector('meta[name="viewport"]'),hotcssEl=document.querySelector('meta[name="hotcss"]'),dpr=window.devicePixelRatio||1;if(hotcssEl){var hotcssCon=hotcssEl.getAttribute("content");if(hotcssCon){var initialDpr=hotcssCon.match(/initial\-dpr=([\d\.]+)/);if(initialDpr){dpr=parseFloat(initialDpr[1])}}}var scale=1/dpr,content="width=device-width, initial-scale="+scale+", minimum-scale="+scale+", maximum-scale="+scale+", user-scalable=no";if(viewportEl){viewportEl.setAttribute("content",content)}else{viewportEl=document.createElement("meta");viewportEl.setAttribute("name","viewport");viewportEl.setAttribute("content",content);document.head.appendChild(viewportEl)}})();var hotcss={};hotcss.px2rem=function(px,designWidth){if(!designWidth){designWidth=parseInt(hotcss.designWidth,10)}return parseInt(px,10)*320/designWidth/20};hotcss.mresize=function(){var innerWidth=window.innerWidth;if(!innerWidth){return false}document.documentElement.style.fontSize=(innerWidth*20/320)+"px"};hotcss.mresize();window.addEventListener("resize",hotcss.mresize,false);window.addEventListener("load",hotcss.mresize,false);setTimeout(function(){hotcss.mresize()},300);window.hotcss=hotcss})(window,document);
			</script>

```

```why
			制作“雪碧图”一般是前端优化的重要一步，主要作用当然就是减少HTTP请求数，加快页面的加载速度，当然，在生成雪碧图之前可以利用[智图](http://zhitu.isux.us/)工具先优化一下图标。然后，hotcss是一个很好的解决移动端布局的方案，结合它一块儿使用应该效果更好。
```

```todo
1. 结合gulp使用到自己的项目中
```