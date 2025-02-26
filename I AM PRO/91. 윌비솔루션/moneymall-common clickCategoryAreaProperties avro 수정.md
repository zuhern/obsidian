---
Created: Invalid date
Updated: Invalid date
---
로 검색한 뒤 clickCategoryAreaProperties 가 맞는지 확인한 후 밑에 추가

**currCtgId, currTemplId 두가지**

, { "name": "currCtgId", "type": [ "null", "string" ] }, { "name": "currTemplId", "type": [ "null", "string" ] }

6개 파일 수정

// 2014-07-29 클릭카테고리에 필드 추가  
String [] p = {"currCtgId","currTemplId"};  
jsonBytes = JsonUtil.clickCategoryAreaPropertiesAdd(jsonBytes, p);  

catch (JSONException e) {  
System.out.println("Invalid Json Type for [CampaignEvent]: [" + new String(jsonBytes) + "]");  
}