* 过滤器
	* 在显示数据时可以对数据进行格式化或过滤
		* 单个--->格式化（将别的类型的数据转换为特定格式的字符串）
		* 多个----》过滤（内部的个数变化， 但类型不变）
		* 不会真正改变被操作数据
	* {{express | 过滤器名：补充说明}}
	* 常用内置：
		* currency 货币格式化(文本)
		* number数值格式化(文本)
		* date 将日期对象格式化(文本)
		* json: 将js对象格式化为json(文本)
		* lowercase : 将字符串格式化为全小写(文本)
		* uppercase : 将字符串格式化全大写(文本)

		* limitTo 从一个数组或字符串中过滤出一个新的数组或字符串
			* limitTo : 3  limitTo : -3
		* orderBy : 根据指定作用域属性对数组进行排序
			* {{[2,1,4,3] | orderBy}}  升序
			* {{[2,1,4,3] | orderBy：‘-’}}  降序
			* {{[{id:2,price:3}, {id:1, price:4}] | orderBy:'id'}  id升序
			* {{[{id:2,price:3}, {id:1, price:4}] | orderBy:'-price'} price降序
		* filter : 从数组中过滤返回一个新数组
			* {{[{id:22,price:35}, {id:23, price:45}] | filter:{id:'3'}} //根据id过滤
			* {{[{id:22,price:35}, {id:23, price:45}] | filter:{$:'3'}} //根据所有字段过滤
	* 自定义过滤器
		* 内置过滤器有限， 有时并不能满足页面显示数据的需求
		* 语法：
			module.filter('myLimitTo'， function(){  //filterFactory
				return function(value, startIndex, endIndex){
					对vlaue进行过滤处理， 并return 处理的结果
					//不要修改value本身
				}
			});
* 编写Angular应用的基本步骤
	* 编写基本静态页面
	* 将angular.js引入工程中， 并在页面中引入
	* 在页面中指定ng-app, ng-controller
	* 在js中定义model和controller
	* 在controller中初始化数据（$scope）
	* 在页面中通过表达式或指令来显示数据
	* 在页面中使用ng-click添加点击监听, 并定义对应的方法进行操作

* 服务
	* 是什么？ 具有特定功能的对象（object对象、函数，数组，基本类型）
	* 内置服务
		* 都以$开头
		* 引入内置服务： 声明式依赖注入（定义形参）, 你不使用它就存在了
		* 常用的几个：
			* $rootScope
			* $scope
			* $filter  :  $filter('过滤器名')(value, params);
			* $timeout 
			* $interval
			* 脏数据检查: 
			    * 当angular定义的函数执行完后, 会对scope内的属性进行检查, 如果发现有改变更新界面
			    * 在非angular定义的回调函数执行完后, 不会进行脏数据检查 --->即使更新了scope页面不会同步更新
		* 页面如何能自动更新的？
			* 在内置的一些函数执行完后， angular会进行脏数据检查的操作
			* controller, $timeout()中的回调函数,  $interval()中的回调函数
			* 如果我们在setTimeout()的回调函数中更新scope， 是不会进行脏数据检查的， 页面不可能更新 
	* 自定义服务
		* 使用module对象来定义服务
		* 定义的方法：
			* factory() : 可以定义任意类型的服务
			* service() ： 只能定义object类型对象
			* value()
			* constant()
			* provider()
		* factory()
			factory('服务名', function(){
				return 服务对象;  //可以是任意类型
			})
		* 如何引入： 声明式依赖注入