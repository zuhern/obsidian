---
Created: Invalid date
Updated: Invalid date
---
srv 에만 해당되는 내용

/hs_gms_srv_api/src/main/resources/config/config-local.properties

로컬에서 메뉴나 공통 코드 변경시 redis에 재 적용하는건

\#GMS Cache Reload

gms.common.cache.menu.reload=false => true로 변경하고 (로컬에서만)

서버 재실행