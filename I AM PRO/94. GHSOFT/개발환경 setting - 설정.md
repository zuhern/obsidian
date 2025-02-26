---
tags:
  - GHSoft
Created: Invalid date
Updated: Invalid date
---
1. Web setting
2. HTTP server

Servers > 우클릭 New >하단의 Configure funtime environments >

Add 클릭 > list에서 HTTP Server 선택

Publishing Directory 선택 >

(C:\IDE\servers\httpd2.2.25\conf\httpd.conf 참조)

Admin-web: C:\IDE\servers\httpd2.2.25\admhtdocs

Srv-web: C:\IDE\servers\httpd2.2.25\htdocs

Csrv-web: C:\IDE\servers\httpd2.2.25\csrvhtdocs

1. 우클릭 add and remove 에서 대상 프로젝트 추가
2. Port 설정:
    1. Adm_web: 8081
    2. Srv_web: 8080
    3. Csrv_web: 8280
3. Maven build 오래걸림
4. refresh (F5)
5. API setting ( and directory : srv_dir ( jsp )
6. Server > new > Tomcat 8.0
7. Server 설정
    1. 프로젝트 설정에서 maven user setting에 setting.xml 넣기
    2. 프로젝트 내 Server.xml을 servers의 톰캣 server.xml 로 복사
    3. Port 설정
        1. Adm_api: 49005, 49080, 49009
        2. Srv_api: 8005, 48080, 8009
        3. Csrv_api: 47080
    4. Modules 설정
        1. Path: / 로 변경 (dir: directory-web)
    5. Server 설정 > General Infomation > Open launch configuration > Arguments > VM arguments 에 -Denv="local" 추가
8. Maven build > clean install (dir 경로 : [https://www.handygms.co.kr/directory-web/org.do](https://www.handygms.co.kr/directory-web/org.do))
9. Error case :
    1. 프로젝트에서 spring을 인식 못해서 Bean 에러가 날 경우 메뉴바 > project > clean 을 해본다.
    2. Jdbc 에러가 날 경우 Servers > config > server.xml 에

<Context docBase="hs_gms_srv_dir(gs)" path="/directory-web" reloadable="true" source="org.eclipse.jst.jee.server:hs_gms_srv_dir">

<ResourceLink global="jdbc/gmsDB" name="jdbc/gmsDB" type="javax.sql.DataSource"/>

</Context>

로 되어 있는지 확인한다

- 발생원인
    - 프로젝트의 server.xml을 복사하지 않았거나…
    - Tomcat 구동시 꼬이면 저 부분을 대체하는 소스가 생성되어 있음