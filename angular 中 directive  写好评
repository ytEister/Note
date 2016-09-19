angularJs 中 directiver 的用法
==
### html
	<div>
		//好评中的五个星星
		<star data-num='order.star'></star>
		<p>
			//好评中的点赞小手
			<p><zan data-num='zan1'></zan></p>
			<p><zan data-num='zan2'></zan></p>
			<p><zan data-num='zan3'></zan></p>
		</p>
	</div>
### directive
	directive('star',function(){
		return {
			restrict: 'EAC',
			template: '<p><span ng-repeat = 'star in starArr' ng-class='{true:\'fa fa-star\',false:\'fa fa-star-o'\}[star.flag]'></span></p>',//引号嵌套需要\转义字符
			scope:{
				num: '='
			},
			link:function(scope,element,attr){
				scope.starArr = [];
				for(var i=1;starArr.length <= 5;i++){
					star.flag = {
						flag:false
					}
					if(i<scope.num && scope.num){
						star.flag = true;
					}
					scope.starArr.push(star);
				}
			}
		}
	})

### //zan 的 directive
	directive('zan',function(){
		restrict: 'EAC',
		template: '<span ng-if='num == null || num == 0' class= 'fa fa-thumb-o'></span><span ng-if='num==1' class='fa fa-thumb'></span>',
		scope: {
			num: '='
		}
	})