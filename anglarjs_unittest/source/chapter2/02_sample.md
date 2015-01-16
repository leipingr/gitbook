
# 应用举例
-----------------

在语法章节的官方文档中已经详细的说明了如何使用。

这里以项目中 tableCtrl_test.js 测试用例编写步骤：

- 定义待测试的module : mainApp
- 定义待测试的controller: tableCtrl
- 测试用例在 it 中定义


下面是 tableCtrl_test.js 的例子：
```javascript
/**
 * Created by reifurther on 14/11/19.
 */

describe('Controller: tableCtrl', function(){

    var $scope, ctrl;

    beforeEach(module('mainApp'));
    beforeEach(inject(function($rootScope, $controller){

        $scope = $rootScope.$new();

        ctrl = $controller('tableCtrl',function(){
            $scope: $scope;

        });
    }));

    it('Should have item in items ', function(){
        expect($scope.item.settleDate).toEqual("");
    })

});

describe('Sample test', function(){

    var a;
    it('sample test', function(){
        a = true;
        expect(a).toBe(true);
    });

});
```
