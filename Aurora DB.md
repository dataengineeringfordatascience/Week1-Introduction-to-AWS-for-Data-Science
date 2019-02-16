- # Aurora DB
  - RDS란? (https://aws.amazon.com/ko/rds/)
    - AWS에서 제공하는 관계형 데이터베이스 서비스 
    - ex) *Amazon Aurora*, PostgreSQL, MySQL, MariaDB, Oracle, Microsoft SQL Server

  ### Structure
  - Amazon Aurora  DB 클러스터 는 하나 이상의 DB 인스턴스와 이 DB 인스턴스의 데이터를 관리하는 클러스터 볼륨으로 구성됨.
    ![Structure](C:\Users\1\Google 드라이브\2019data_engineering_study\Structure.png)
  - SQL / Transaction과 Caching을 분리
  - 빠른 Crash Recovery  
    - storage 수준에서 on-demand로 재생 (개빠름)
    - 최종 check point로부터 log 재생 (안빠름)


  ### 분산 쓰기
  * MySQL
    ![MySQL](C:\Users\1\Google 드라이브\2019data_engineering_study\MySQL.PNG)

  * Aurora

    ![Aurora](C:\Users\1\Google 드라이브\2019data_engineering_study\Aurora.PNG)
  - Mysql의 경우 순차적으로 primary instance와 standby instance에 쓰기 복제
  - aurora는 독립적인 복제 인스턴스에 병렬적으로 write

  

  ### dosen't Aurora support multi AZ?
  - Multi AZ: RDS는 가용성을 높이기 위해서 물리적으로 떨어진 Availability Zone들에 인스턴스를 생성할수 있다.  
    따라서 한개의 AZ가 망가져도 다른 AZ가 살아있다면 서비스에 장애가 생기지 않는다.  
    이 기능을 멀티 AZ라 부르며 이 기능이 적용되면 콘솔상에선 1개의 DB 인스턴스처럼 보이더라도 실제론 여러개의 인스턴스가 생기게 된다. (그만큼 비용이 증가되는건 덤)
  - 하지만 오로라는 이 멀티 AZ를 지원하지 않는다.

  - 대신, 오로라는 Read Replica를 Failover에 사용한다. 
  - 여러 RR이 같은 클러스터로 묶여 있고 Write 권한이 있는 마스터가 다운되면 RR중 하나를 마스터로 자동 승격시켜 대응
  - 이 과정은 수초내로 기존 RDB 대비 굉장히 빨리 이루어진다
  - 이는 Storage가 Computation Unit과 물리적으로 분리되어 있으며 DNS 차원에서 연결을 승격된 RR로 바로 틀수 있기 때문이다
    * (EB의 CNAME Swap 기능)


  ### ETC
  - 최대 15개 replica
  - fail over 시에 데이터 유실 X(mysql의 경우 있음)
  - 캐시 웜업 X (인스턴스와 캐시가 분리)
  - 시점 복구Restore 제공  
  - 보안 강화
  - 보통 쪼끔 비쌈
  - 패치에 따른 downtime(인스턴스 재시작)
  - 64TB까지 storage 자동 증가 (사용한 만큼 과금)
  - 배치 삽입 성능 향상(인덱스 경유 x?)
  - 다차원 데이터 타입 지원: Geometry(R-tree, Z-index)

  ### I/O Traffic
  ![IO_traffic](C:\Users\1\Google 드라이브\2019data_engineering_study\IO_traffic.jpeg)

  ### 요금 (오하이오 기준 예시)
  - 월별 GB당 0.10 USD
  - 요청 1백만 건당 0.20 USD
  - 복제된 쓰기 I/O 백만 건당 0.20 USD
  - 월별 GB당 0.023 USD
  - back tracking; 변경 레코드 1백만 개당 0.013 USD
  - 데이터 송수신
    - Internet to RDS: GB당 0.00 USD
    - RDS to Internet: GB당 0.00 USD
      - 최대 1GB / 월GB당 0.00 USD
      - 다음 9.999TB / 월 GB당 0.09 USD
      - 150TB 초과 / 월 GB당 0.05 USD
    - Amazon RDS에서 데이터 송신: GB당 0.00~0.02 USD

  

  ### References
  - https://www.slideshare.net/awskorea/aws-db-day-auroradeepdive ★★★★
  - https://m.blog.naver.com/sory1008/220950945170 ★★
  - https://medium.com/hbsmith/aws-aurora-%EB%8F%84%EC%9E%85%EC%97%90-%EB%8C%80%ED%95%9C-%EB%AA%87%EA%B0%80%EC%A7%80-%EC%82%AC%EC%8B%A4-45eb602bad58 ★★
  - https://docs.aws.amazon.com/ko_kr/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.html ★★