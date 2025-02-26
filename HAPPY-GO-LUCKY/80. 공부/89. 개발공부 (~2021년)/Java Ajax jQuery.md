---
Created: Invalid date
Updated: Invalid date
---
$.callDataAjax = function(nodeid) {  
console.log("callDataAjax");var jsonData = $.ajax({  
type: "GET",// url : "  

[http://10.203.5.27:8010/getResultOfCornerSalesData](http://10.203.5.27:8010/getResultOfCornerSalesData)

",// dataType : "jsonp",  
url : "getResultOfCornerSalesData.ssg", dataType : "json",  
async: false,  
data : {"dt" : $("\#todate").val(),"siteNo" : $("\#comboSite").val(),"nodeid" : nodeid  
}, success: function(data) { console.log('callDataAjax 성공 - ', data); $.roadData(data); }, error: function(xhr) { console.log('callDataAjax 실패 - '); }  
});  
console.log("callDataAjax_end");  
}