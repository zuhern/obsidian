---
Created: Invalid date
Updated: Invalid date
---
1. filesystem 에러

: ~ 밑에 (mkdir ~/filesystem)

2. Incompatible namespaceIDs

:

- 현재 네임노드의 매타정보는 namespaceID 와, 현재 데이터 노드의 namespaceID가 달라서 뜨지 않는 문제이다. 데이터는 중요하기 때문에 덮어쓰지 않는다고 한다.

hdfs-site.xml 에 설정했던 디렉토리 안의 파일을 모두 삭제 해야 한다. (DataNode에만 적용된다.) (dfs.data.dir)

data 폴더를 rmdir -rf data;mkdir data

- namenode namespaceID와 datanode namespaceID가 일치하지 않을 경우 발생하는 에러이다.

이 에러는 namenode -format 을 하였을 경우 주로 발생한다.

초기설치가 아닌 하둡 사용중에 namenode를 포맷하여야 하는 상황이 온다면

hdfs의 data 폴더를 지우고 다시 생성한 후, namenode를 포맷하여야 정상적으로 작동

3.