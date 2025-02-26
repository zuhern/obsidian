---
Created: Invalid date
Updated: Invalid date
---
wcm의 grunt는 app → dist copy위주 임

js는 모두 dist 대상으로 설정되어 있음

css, img는 기존에 없었으며

html은 view/cache-template.html만 있었다.

## css, img, html 추가인 경우

- wcm

> 현재 wcm에 css, img, html의 수가 적어서 복사 대상 파일을 상세하게 적어놓았음.. (추후 js처럼 복사할 것 같음.)그렇기 때문에 css, img, html은 추가되면 꼭 gruntfile에 정의해 주어야한다.(안할 경우 local에서는 문제가 없으나, 서버에 올라가면 대상 파일이 누락되어 있음.)// 예시grunt.initConfig({        clean: {                dist: ["dist", "deploy"],        },    copy: {                css: {                        files: [                                        {expand: true, cwd: "app/libs/web-modeler/css/", src: ["{,**/}*.*"], dest: "dist/libs/web-modeler/css/", flatten: false}                        ]                },                img: {                        files: [                                        {expand: true, cwd: "app/libs/web-modeler/img/", src: ["{,**/}*.*"], dest: "dist/libs/web-modeler/img/", flatten: false}                        ]                },                dist: {                        files:[                                        {expand: true, cwd: "app/libs/proc-act/html/", src: ["{,**/}*.html"], dest: "dist/libs/proc-act/html/", flatten: false},                                        {expand: true, cwd: "app/libs/views/", src: ["{,**/}*.html"], dest: "dist/libs/views/", flatten: false}                                ]                }         },

- srv, adm, csrv

> html: copy/vendorHtml 에 선언되어 있음.

> css: copy/vendorCss 에 선언되어 있음

> img: copy/vendorCss 에 선언되어 있음.