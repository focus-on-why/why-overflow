## 왜 Spark vs. Hadoop 를 비교하는 것일까?

### [Apache Spark](https://spark.apache.org/)
- 오픈 소스로 된 분산 처리 프레임워크

### 왜 Spark vs. Hadoop 를 비교하는 것일까?

- **둘다 분산 병렬처리이지만 Spark 는 In-Memory 이기 때문에 속도가 빠르다.**
  - In-Memory: Ram을 통해 연산하는 것
- **데이터를 메모리에 놓고 하느냐 vs. 디스크에 놓고 하느냐**
  - Hadoop
      - 디스크로부터 map/reduce할 데이터를 불러오고, 처리결과도 디스크에 씀
      - 그래서 데이터를 읽고 쓰는 속도가 느림
      - 하지만, 디스크 용량만큼 데이터를 한번에 처리할 수 있음
  - Spark
      - 메모리로부터 map/reduce할 데이터를 불러오고, 처리결과도 메모리에 씀
      - 그래서 데이터를 읽고 쓰는 속도가 빠름.
      - 하지만 메모리 용량만큼의 데이터만 처리할 수 있음
- **속도**: 스파크가 하둡 맵리듀스보다 100배 빠르다.
  - MapReduce
      - “데이터를 쪼개어 수 많은 머신들에게 분산시켜 로직을 수행한 다음 결과를 하나로 합치자”는 것이 핵심 아이디어
      - 쪼개기(Split) -> 데이터 처리하기(Map) -> 처리된 데이터 합치기(Reduce)
- **개발언어**: Scala vs. Java
  - Spark 내부는 scala로 개발이 되었지만 java, scala, python, r, sql 을 지원함.
      - 단 속도는 scala 로 작성한 코드가 더 빠르다고 함.
- **데이터처리**
  - Spark: 배치, 실시간, 반복, 대화형, 그래프
  - Hadoop: 배치
- **캐싱**
  - spark: 데이터를 메모리에서 캐싱해서 처리하기 때문에 빠르다.
  - hadoop: 캐싱을 지원하지 않음.

### 왜 Spark를 알고 배워야 할까?

- Spark는 Hadoop과의 호환성이 높음.
- Spark는 Hadoop MapReduce와 중복됨.
  - **=>** 즉, Spark는 Hadoop에서 사용하는 MapReduce를 사용하고, In-Memory 연산을 통해 속도가 더 빠름. 그러면 Spark 쓸만하지? 라는 느낌을 받음.
- Spark는 Java, Scala, Python, R 과 같은 다양한 플랫폼에서 프로그램을 실행할 수 있음.
- [RDD 를 알아야 Spark 를 아는 것이다 ?!](https://www.slideshare.net/yongho/rdd-paper-review)
  - RDD: Resilient Distributed Dataset, 탄력적인 분산 데이터셋

### 느낀점

- MapReduce, RDD 가 무엇인지 알아야 이해가 더 빠르고 Spark를 정확히 알 수 있을 것 같다.
- 대부분의 자료를 읽어보면 Spark와 Hadoop은 비교 대상이지만, 내 생각은 파트너(?) 같은 느낌이다. Spark와 Hadoop을 함께 사용할 때 효과를 더 많이 낼 수 있지 않을까?
- 대충 Spark가 어떤 느낌인지는 알겠지만, 실제로 어떻게 사용하는지 감이 오지 않는다.실제 간단한 프로젝트를 통해 Spark를 사용해봐야 정확히 알 것 같은 느낌이다.


### 참고

- [최신 데이터 인프라 이해하기 #5 - Spark, Python, Hive](https://www.youtube.com/watch?v=Wo6utoIC2Jw)
- [갈아먹는 BigData [1] MapReduce 이해하기](https://yeomko.tistory.com/31)
- [데엔잘하고싶은데엔 블로그](https://pearlluck.tistory.com/category/Big%20Data/Spark)
- [5 Reasons Why You Should Learn Apache Spark Now](https://www.projectpro.io/article/5-reasons-why-you-should-learn-apache-spark-now/192)
- [왜 Spark를 써야할까](https://www.brainbackdoor.com/data/spark-characteristics)
- [스파크에 대한 아주 대략적인 정리](https://boomkim.github.io/2019/12/11/what-is-spark/)
- [[빅데이터] 하둡(Hadoop)과 아파치 스파크(Spark) 파헤치기](https://m.blog.naver.com/acornedu/221083892521)
- ["하둡을 제압한 빅데이터 플랫폼" 아파치 스파크란 무엇인가](https://www.itworld.co.kr/news/147556)