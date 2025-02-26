---
Created: Invalid date
Updated: Invalid date
---
## Shark/Spark with Tachyon (production) Install

1. 설치위치
2. 참고문서
    1. Shark : [http://shark.cs.berkeley.edu/](http://shark.cs.berkeley.edu/)
    2. Spark : [https://spark.apache.org/docs/latest/index.html](https://spark.apache.org/docs/latest/index.html)
    3. Tachyon : [http://tachyon-project.org/Running-Shark-on-Tachyon.html](http://tachyon-project.org/Running-Shark-on-Tachyon.html) (main)
        1. [http://tachyon-project.org/Running-Tachyon-on-a-Cluster.html](http://tachyon-project.org/Running-Tachyon-on-a-Cluster.html) ( cluster 설치 문서 )
3. 설치버전
    1. Tachyon : 0.5.0 ( compatible with Shark 0.9.1+ )
    2. Shark : 0.9.2 ( compatible with Spark 0.9.1 )
    3. Spark : 0.9.1
4. 설치
    1. Tachyon 0.5.0 ( [http://tachyon-project.org/Running-Shark-on-Tachyon.html](http://tachyon-project.org/Running-Shark-on-Tachyon.html) )
        1. 설치 : [http://tachyon-project.org/Running-Tachyon-on-a-Cluster.html](http://tachyon-project.org/Running-Tachyon-on-a-Cluster.html) Icon
            
            **Tachyon 설치 가이드**
            
            ```Plain
            # installhttp://tachyon-project.org/downloads/tachyon-0.5.0-bin.tar.gz
            ```
            
            `cd tachyon-``0.5``.``0`
            
            `# configuration`
            
            `cd conf`
            
            `mv tachyon-env.sh.template` [`tachyon-env.sh`](http://tachyon-env.sh/)
            
            ```Plain
            http://master002.prod.moneymall.ssgbi.com:19999/home
            ```
            
5. 참고
    1. Tachyon 장점
        - Shark 0.7 adds a new storage format to support efficiently reading data from [Tachyon](http://tachyonproject.org/), which enables data sharing and isolation across instances of Shark. Our meetup [slide](http://files.meetup.com/3138542/2013-05-09%20Shark%20%40%20Spark%20Meetup.pdf) gives a good overview of the benefits of using Tachyon to cache Shark's tables. In summary, the followings are four major ones:
            - In-memory data sharing across multiple Shark instances (i.e. stronger isolation)
            - Instant recovery of in-memory tables
            - Reduce heap size => faster GC in shark
            - If the table is larger than the memory size, only the hot columns will be cached in memory