---
Created: Invalid date
Updated: Invalid date
---
function foo(param1, param2){ console.log(param1); console.log(param2); } var fnText = foo.toString(); console.log(fnText); var FN_ARGS = /^function\s*[^\(]*\(\s*([^\)]*)\)/m; var FN_ARG_SPLIT=/,/; var argDecl = fnText.match(FN_ARGS); var args = argDecl[1].split(FN_ARG_SPLIT); console.log(args);