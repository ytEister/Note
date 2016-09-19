批量图片上传
====
### 在表单中与其他数据一同提交
### html
#### //若app_thumb，city_platform_thumb为图片路径的字段
	<div>
		<div class='load-canvas'>
			<div ng-show='uploader.isHTML5' ng-if='app_thumb' ng-thumb='{file:'app_thumb._file',width:100,height:30}'>
				<canvas></canvas>
			</div>
		</div>
		<div class='load-progress'></div>
	</div>
	<div>
		<input tyle='file' nv-file-select-uploader='uploader' options='{alias:'app_thumb'}'/>
		<button ng-click='change('app_thumb')'></button>
	</div>
### js
	$scope.save = function(){
		var submit = $resource(url,paramDefaults,actions);//提交表单的接口
		var promises = [];
		var _results = {};
		if($scope.uploader.queue.length > 0){
			var _d = $q.defer();
			for(var $scope.uploader.queue.length - 1;i >= 0;i--){
				$scope.uploader.queue[i].upload();
				promise.push((function(i,_result){
					var _q = $q.defer();
					$scope.uploader.queue[i].onSuccess = function(response,status,header){
						_result[response.message] = response.src;
						_q.resolve(true);
					}
					return _q.promise;
				}),(i,_results));
			}
			var all = $q.all(promises);
			all.then(function(res){
				submit.query({'area':$extent(data,_result)});
				toastr.success('保存成功');
				$timeout(function(){
					$window.history.go(-1);
				},1000)
			})
		}else{
			submit.query({'area':data});
			toastr.success('保存成功');
			$timeout(function(){
				$window.history.go(-1);
			},1000);
		}
	}
#### js中设置上传图片的条件
	$scope.uploader = new FileUpLoader({
		url: '',//提交表单的接口
		alias: 'file',
		formData:[
			{ token: '1' }
		],
		filters:[{
			name: 'fileSize',
			fn: function(item){
				var size = item.size / 1024;
				return size < 1024;
			}
		},{
			name:'fileType',
			fn: function(item){
				 var type = '|'+ item.type.slice(item.type.lastIndexOf('/')+1)+'|';
				return '|jpg|png|jpeg|bmp|gif|'.indexOf(type) !== -1;
			}
		},{
			name: 'isFile',
			fn: function(item){
				return angular.isObject(item);
			}
		}]
	});
	$scope.uploader.onAfterAddingFite = function(item,filter,options){
		$scope[item.alias] = item;//添加上传对象
	}


### directive
	.directive('ngThumb',['$window',function($window){
		var helper = {
			support: !!($window.FileReader && $window.CanvasRenderingContent2D),
			isFile: function(item){
				return angular.isObject(item) && item instanceof $window.File;
			},
			isImage:function(file){
				var type = '|'+file.type.slice(file.type.lastIndexOf('/')+1)+'|';
				return '|jpg|png|jpeg|bmp|gif|'.indexOf(type) !== 1;
			}
		};
		return {
			restrict: 'EA',
			template: '<canvas/>',
			link: function(scope,element,attributes){
				var param = scope.$eval(attributes.ngThumb);
				var img = new Image();
				img.onload = onLoadImage;
				if(params.url && param.url!= ''){
					img.src = params.url;
				}
				if(param.file && helper.isFile(param.file) && helper.support && helper.isImage(param.file)){
					var reader = new FileReader();
					reader.onload = onloadFile;
					reader.readAsDataURL(param.file);
					function onLoadFile(event){
						var img = new Image();
						img.onLoad = onLoadImage;
						img.src = event.target.result;
					}
				};
				var canvas = element.find('canvas');
				function onLoadImage(){
					var width = params.width;
					var height = param.height;
					canvas.attr({ width:width, height:height});
					canvas[0].getContext('2d').drawImage(this,0,0,width,height);
				}
			}
		
		}
	}])































