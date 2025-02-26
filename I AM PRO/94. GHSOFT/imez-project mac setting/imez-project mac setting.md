---
Created: Invalid date
Updated: Invalid date
---
1. java 설치 (jdk 9버전으로 설치할 경우 api 빌드가 되지 않음)[jre-8u151-macosx-x64.dmg](https://ghsoftbiz.atlassian.net/wiki/download/attachments/13828097/jre-8u151-macosx-x64.dmg?version=1&modificationDate=1512527104355&cacheVersion=1&api=v2)
    
    ![[untitled 18.jpg|untitled 18.jpg]]
    
2. imez-project 압축해제 후 root로 이동
3. Hosts 파일 변경
    1. 귀차니즘을 위한 스크립트복사 대상 파일은 /scripts/hosts에 있으므로 편한대로 변경해서 쓰세요
    2. /private/etc/hosts 직접 고치기
4. imez-project 내 작업
    1. 터미널에서
    2. imez-project 내에 있는 eclipse를 실행
5. tunnel 설정
    1. ssh -i ~/imez-dev-jump.pem root@imez-dev-jump -L 18018:10.20.0.245:18018 -L 38080:10.20.0.245:38080 -L 43306:10.30.0.10:43306 -L 46379:10.30.0.13:46379 -L 56379:10.30.0.13:56379 -L 58080:10.20.0.245:58080 -L 6379:10.30.0.5:6379 -L 8983:10.30.0.5:8983
    2. iterm의 경우: Profiles > Edit Profiles > + 버튼 > command 에 위 ssh 명령어 입력 후 저장
    3. 그 후 profile에서 선택하면 바로 jump 서버 연결 되고 tunnel 설정 됨
6. apach start, stop, status

- 추천 툴
    - iterm(terminal): 다중 탭, ,
    - forklift(finder 유료)