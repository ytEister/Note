# sass 的用法
	@import ‘xxx’     # sass文件中引入另一个xxx.sass 文件
### 多值变量list和map
	//其中list相当于 js中的一维数组 
	取其值时  eg. color：nth($color,$index)
	//map数据是以key和value成对出现 $data(key:val,key1:val1,key2:val2)
	取其值时  eg. data：map-get($data,$key)  
### 混合声明($mixin) ,可传递参数(参数名用$开始，多个参数用，隔开)，(@include)调用
	@mixin max-screen($res){@media only screen and ( max-width: $res ){@content;}}

@include max-screen(480px) {
  body { color: red }
}
### 条件循环及判断
	//if判断
	p {
	  @if $type == ocean {
	    color: blue;
	  } @else if $type == matador {
	    color: red;
	  } @else if $type == monster {
	    color: green;
	  } @else {
	    color: black;
	  }
	}
	//@each循环
	$animal-list: puma, sea-slug, egret, salamander;
	@each $animal in $animal-list {
	  .#{$animal}-icon {
	    background-image: url('/images/#{$animal}.png');
	  }
	}
### 三目判断
	//语法为：if($condition, $if_true, $if_false) 。三个参数分别表示：条件为真的值，条件为假的值。
	if(true, 1px, 2px) => 1px
	if(false, 1px, 2px) => 2px




