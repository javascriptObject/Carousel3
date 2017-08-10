# js3D特效图片切换Carousel3
效果如下：
![](img/img.gif)

all code:
```
<!--文档声明为 html（最新html5）-->
<!doctype html>
<html>
	<head>
		<!--声明当前页面编码格式为国际编码（utf-8）还有一种中文编码（gbk/gb2312）-->
		<meta charset="UTF-8">
		<!--网页三要素-->
		<meta name="Keywords" content="关键词,关键词">
		<meta name="Description" content="描述">
		<title>js3D特效图片切换</title>
		<style id="css">
		*{margin:0;padding:0;}
		#box{
			width:1050px;
			height:361px;
			margin:100px auto 0;
			position:relative;
		}
		#list-pic{
			width:1050px;
			height:361px;
			perspective:1500px;/*景深*/
		}
		#list-pic li{
			list-style:none;
			float:left;
			width:50px;
			height:360px;
			transform-style:preserve-3D;/*3D 表示所有的子元素在3D空间展现*/
			position:relative;
			-webkit-transform-origin:center center -180px;
		}
		#list-pic li a{
			position:absolute;
			width:100%;
			height:100%;
			font-size:30px;
		}
		#list-pic li a:nth-child(1){
			left:0;
			top:0;
			background:url('img/flash1.png');
		}
		#list-pic li a:nth-child(2){
			left:0;
			top:-100%;
			background:green;
			transform-origin:bottom;
			transform:rotateX(90deg);
			background:url('img/flash2.png');
		}
		#list-pic li a:nth-child(3){
			left:0;
			top:0;
			background:blue;
			transform:translateZ(-361px) rotateX(180deg) ;
			background:url('img/flash3.png');
		}
		#list-pic li a:nth-child(4){
			left:0;
			top:100%;
			background:yellow;
			transform-origin:top;
			transform:rotateX(-90deg) ;
			background:url('img/flash4.png');
		}
		#num-btn{
			width:100%;
			height:20px;
			position:absolute;
			left:0;
			bottom:30px;
			text-align:center;
		}
		#num-btn li{
			list-style:none;
			width:20px;
			height:20px;
			border-radius:50%;
			background:#313131;
			display:inline-block;
			cursor:pointer;
			color:#fff;
		}
		#num-btn li.active{
			background:red;
		}
		</style>
	</head>
	<body>
	<div id="box">
		<ul id="list-pic">
		</ul>
		<ul id="num-btn">
			<li class="active">1</li>
			<li>2</li>
			<li>3</li>
			<li>4</li>
		</ul>
	</div>
	</body>
</html>
<script>
	var List = document.getElementById('list-pic');
	var Css = document.getElementById('css');
	var Btn = document.getElementById('num-btn');
	var BtnLi = Btn.getElementsByTagName('li');
	var Iw = 50;
	var ListLi = List.children;
	var num = List.clientWidth/Iw;
	var str = '';//添加元素
	var scss = '';//添加样式
	var Zindex = 0;//层级关系
	for (var i=0;i<num ;i++ )
	{
		i>num/2?Zindex--:Zindex++;
		str = str + '<li><a href=""></a><a href=""></a><a href=""></a><a href=""></a></li>';
		scss += '#list-pic li:nth-child('+(i+1)+') a{background-position:-'+Iw*i+'px 0;}';

		scss += '#list-pic li:nth-child('+(i+1)+'){z-index:'+Zindex+';}';

	}
	List.innerHTML = str;
	Css.innerHTML += scss;
	for (var k=0;k<BtnLi.length; k++ )
	{
		BtnLi[k].index = k;//0 1 2 3
		BtnLi[k].onclick =function(){
			for (var i=0;i<BtnLi.length; i++ ){
				BtnLi[i].className = '';
			}
			for (var j=0;j<num; j++ ){
				ListLi[j].style.transition='0.8s '+j*50+'ms';
				ListLi[j].style.WebkitTransform ='rotateX('+90*this.index+'deg)'
			}
			this.className = 'active';
		}
	}
</script>
```

