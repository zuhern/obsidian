---
Created: Invalid date
Updated: Invalid date
---
.drawGrid = function () {  
jQuery("\#table1").jqGrid({  
datatype: "local",  
height:620, colNames:['사이트번호', '코너ID', '카테고리ID', '사이트명', '코너명', '전시매장' , '방문자수', '매출', '주문건수', '이익', '건단가', '주문전환율', '주문이익율' , '뭔지모름1', '사용여부', '전시여부' ], colModel:[  
{name:'SITE_NO', index:'SITE_NO', width:80, align:'center', hidden:true},  
{name:'CORNR_ID', index:'CORNR_ID', width:100, align:'center'},  
{name:'DISP_CTG_ID', index:'DISP_CTG_ID', width:100, align:'center', hidden:true},  
{name:'SITE_NM', index:'SITE_NM', width:100, hidden:true},  
{name:'CORNR_NM', index:'CORNR_NM', width:160},  
{name:'DISP_CTG_NM', index:'DISP_CTG_NM', width:300},  
{name:'VISIT_CNT', index:'VISIT_CNT', width:80, align:'right'},  
{name:'ORD_AMT', index:'ORD_AMT', width:80, align:'right'},  
{name:'ORD_CNT', index:'ORD_CNT', width:80, align:'right'},  
{name:'PRFT_AMT', index:'PRFT_AMT', width:80, align:'right'},  
{name:'CNTPERAMT', index:'CNTPERAMT', width:80, align:'right'},  
{name:'ORDTRANSPERCENT', index:'ORDTRANSPERCENT', width:80, align:'right'},  
{name:'ORDGAINPERCENT', index:'ORDGAINPERCENT', width:80, align:'right'},  
{name:'DISP_DEMND_PSBL_YN', index:'DISP_DEMND_PSBL_YN', width:80, align:'right', hidden:true},  
{name:'USE_YN', index:'USE_YN', width:80, align:'center'},  
{name:'SET_YN', index:'SET_YN', width:80, align:'center'} ], caption: "코너별 영역 매출"  
});  
}  
$.roadData = function(data) {var ids = $("\#table1").getDataIDs();for(var i in ids){  
$("\#table1").delRowData(ids[i]);  
}var mydata = data;for(var i=0;i<=mydata.length;i++)  
jQuery("\#table1").jqGrid('addRowData',i+1,mydata[i]);  
}