RDS에는 Oracle, MSSQL, PostgreSQL 등이 있다.

## MariaDB를 추천하는 이유


- 가격
    
    RDS의 가격은 라이센스 비용 영향을 받는다. 상용 데이터베이스인 Oracle, MSSQL이 오픈소스인 MySQL, MariaDB, PostgreSQL 보다는 **동일한 사양 대비 더 가격이 높다.** 
    
- Amazone Aurora 교체 용이성
    
    Amazone Auroras는 AWS에서 MySQL과 PostgreSQL을 클라우드 기반에 맞게 재구성한 데이터베이스이다. 공식자료에 의하면 RDS MySQL 대비 5배, RDS PostgreSQL보다 3배의 성능을 제공한다. 더불어 **AWS에서 직접 엔지니어링** 하고 있어 지속적으로 발전하고 있다.
    
    즉 클라우드 서비스에서 가장 적합한 데이터베이스이기 때문에 많은 회사들이 Amazone Aurora를 선택한다. 
    

## MariaDB란


국내외 오픈소스 데이터베이스 중 가장 인기 있는 제품은 MySQL이다. (**단순 쿼리 처리 성능**이 압도적이며 오래 사용되어와 성능과 신뢰성 등에서 꾸준히 개선되어 왔기 때문)

발전하던 MySQL이 2010년에 썬마이크로시스템즈와 오라클이 합병되면서 많은 MySQL 개발자들은 썬마이크로시스템즈를 떠나며 본인만의 프로젝트를 진행하게 되었고 이 중 MySQL의 창시자인 몬티 와이드니어가 만든 프로젝트가 MariaDB이다.

MySQL을 기반으로 만들어져 쿼리를 비롯한 전반적인 사용법이 MySQL과 유사하며 다음과 같은 장점이 있다.

- 동일 하드웨어 사양으로 MySQL보다 향상된 성능
- 좀 더 활성화 된 커뮤니티
- 다양한 기능
- 다양한 스토리지 엔진
- [10 reasons to migrate to MariaDB (if still using MySQL)](https://linuxnatives.net/2015/10-reasons-to-migrate-to-mariadb-if-still-using-mysql)
