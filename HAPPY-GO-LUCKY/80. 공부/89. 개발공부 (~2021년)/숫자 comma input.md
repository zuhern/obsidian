---
Created: Invalid date
Updated: Invalid date
---
var myApp = angular.module('myApp', []);

myApp.controller('MyCtrl', function($scope) {

$scope.currencyVal = 123456;

});

myApp.directive('currencyInput', function($filter, $browser) {

return {

require: 'ngModel',

link: function($scope, $element, $attrs, ngModelCtrl) {

var listener = function() {

var value = $element.val().replace(/,/g, '')

$element.val(commaNumber(value));

//                $element.val($filter('number')(value, false))

}

var commaNumber = function (num) {

var len, point, str;

num = Math.round(num) + "";

point = num.length % 3 + 1;

len = num.length;

console.log('point:', point);

str = num.substring(0, point);

while (point < len) {

if (str !== "") {

str += ",";

}

str += num.substring(point, point + 3);

point += 3;

}

return str;

}

// This runs when we update the text field

ngModelCtrl.$parsers.push(function(viewValue) {

return viewValue.replace(/,/g, '');

})

// This runs when the model gets updated on the scope directly and keeps our view in sync

ngModelCtrl.$render = function() {

//$element.val($filter('number')(ngModelCtrl.$viewValue, false))

$element.val(commaNumber(ngModelCtrl.$viewValue));

}

$element.bind('change', listener)

$element.bind('keydown', function(event) {

var key = event.keyCode

// If the keys include the CTRL, SHIFT, ALT, or META keys, or the arrow keys, do nothing.

// This lets us support copy and paste too

if (key == 91 || (15 < key && key < 19) || (37 <= key && key <= 40))

return

$browser.defer(listener) // Have to do this or changes don't get picked up properly

})

$element.bind('paste cut', function() {

$browser.defer(listener)

})

}

}

})