<meta http-equiv="Content-Type" content="text/html; charset=utf-8">


## AngularJS Directive 隔离 Scope数据交互
#### 为什么使用隔离scope
        一个可重复的directive,不能依赖父scope,这时候就需要使用隔离scope代替。
	共享scope可以直接共享父scope，而隔离scope无法共享父scope。
使用共享scope的时候，可以直接从父scope中共享属性。 
#### js代码
	app.controller("myController", function ($scope) {
	    $scope.name = "hello world";
	    }).directive("shareDirective", function () {
	    return {
	            template: 'Say:{{name}}'
	    }
	});
#### html代码：
	<div ng-controller="myController">
		<div share-directive=""></div>
	</div>
#### 输出结果：
	Say:hello world
### 隔离scope，使用隔离scope的时候，无法从父scope中共享属性；
#### directive在使用隔离scope的时候，提供了三种方法同隔离之外的地方交互。这三种方法分别是：
	1.@ 绑定一个局部的scope属性到当前的dom节点的属性值。结果总是一个字符串，因为dom的
	  属性是字符串。
    2.& 提供一种方式执行一个表达式在父scope的上下文中。如果没有指定attr名称，则属性名
	  称为相同的本地名称。
	3.= 通过directive的attr属性值在局部scope的属性和父scope属性名之间建立双向绑定
@ 局部 scope 属性
#### js代码
	'''js
	 app.controller("myController", function ($scope) {
	        $scope.name = "hello world";
	    }).directive("isolatedDirective", function () {
	        return {
	            scope: {
	                name: "@"
	            },
			template: 'Say：{{name}} <br>改变隔离scope的name：<input type="buttom" value="" ng-model="name" class="ng-pristine ng-valid">'
		}
	})
	'''
#### html 代码

	<div ng-controller="myController">
	   <div class="result">
	       <div>父scope：
	           <div>Say：{{name}}<br>改变父scope的name：<input type="text" value="" ng-model="name"/></div>
	       </div>
	       <div>隔离scope：
	           <div isolated-directive name="{{name}}"></div>
	       </div>
	       <div>隔离scope（不使用{{name}}）：
	             <div isolated-directive name="name"></div>
	       </div>
	  </div>

































			