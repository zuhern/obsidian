---
Created: Invalid date
Updated: Invalid date
---
$.drawTree = function() {  
console.log("makeTree");  
$('\#categoryTree').remove();  
$('\#treeDiv').append("<div id='categoryTree' class='tree' align='left'></div>");  
$('\#categoryTree').jstree({ 'core' : { 'themes' : { 'stripes' : true }, 'data' : {// url : '  

[http://10.203.5.27:8010/getResultOfCornerSalesCategory](http://10.203.5.27:8010/getResultOfCornerSalesCategory)

',// dataType : "jsonp",  
url : "getResultOfCornerSalesCategory.ssg", dataType : "json", contentType: 'application/json',  
data : function (node) {var nodeid = '0'if(node.id!='#') nodeid =  

[node.id](http://node.id/)

;return {"siteNo" : $("\#comboSite").val(),'parentid' : nodeid  
};  
}, success: function(data) { console.log('callCategoryAjax 성공 - ', data); }  
}  
}  
}) .on('select_node.jstree', function (e, data) { // 테이블에 뿌릴 데이터 가지고 오기 $.callDataAjax(data.  

[node.id](http://node.id/)

);  
});  
}