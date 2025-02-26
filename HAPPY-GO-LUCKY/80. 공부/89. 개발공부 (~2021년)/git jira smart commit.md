---
Created: Invalid date
Updated: Invalid date
---
https://confluence.atlassian.com/adminjiracloud/connect-jira-cloud-to-github-814188429.html

git > setting > OAuth > add

여기서 Homepage랑 Auth callback에 https://ghsoftbiz.atlassian.net 같은 Jira url을 입력

Jira 관리 > 응용프로그램(app) > DVCS accounts > github 연결

여기서 client id, client secret 은 git oauth 상세 페이지에 있다.

git 에 commit message 에

"테스트 중 IV1-178"

라고 입력하면 해당 티켓(IV1-178)에 '개발' 필드에 관련 commit, branch, pull request 등으로 상태가 나뉘어 보이고

"테스트 중 IV1-178 \#closed" 이라고 입력하면 Jira 티켓이 자동으로 closed 된다.

"테스트 중 IV1-178 \#qa" 이라고 입력하면 Jira 티켓이 자동으로 qa 상태가 된다.

즉

티켓명을 메세지에 포함할 것\#작업흐름명 을 대소문자 상관없이 입력하여 티켓 상태 변경 (하단 이미지의 작업흐름명 참조)