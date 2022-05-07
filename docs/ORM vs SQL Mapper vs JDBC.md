# ORM vs SQL Mapper vs JDBC

### 주제 흐름도

Jdbc의 단점 → 이를 해결하기 위한 SQL Mapper → ORM

**Persistance (영속성)**

**데이터를 생성한 프로그램이 종료되더라도, 사라지지 않는 데이터의 특성**

### Jdbc (Java DataBase Connectivity)

![Untitled](https://user-images.githubusercontent.com/80089860/167233272-166e8064-a9b3-41a5-b6ae-50b2f63f87bb.png)

자바 애플리케이션에서 DBMS의 종류에 상관 없이, 하나의 JDBC API를 이용하여 DB작업을

처리할 수 있다

각각의 DBMS (Oracle, MySQL 등)은 이를 구현한 JDBC 드라이버를 제공한다

![Untitled 1](https://user-images.githubusercontent.com/80089860/167233274-18ed657d-e03a-4ba0-9262-688168e137c2.png)

### JDBC을 이용하여 영속성을 유지함에 있어서 단점이 있다

**우리는 이를 위해, Persistence Framwork를 사용한다**

: JDBC 프로그래밍의 복잡함이나 번거로움 없이 간단한 작업만으로 데이터베이스와 연동되는

시스템을 빠르게 개발

### Persistence Framework (내부적으로 JDBC api를 사용)

영속성 프레임워크는 아래와 같이 크게 두 가지로 나뉠 수 있다

1. **SQL Mapper** 
    - 객체와 sql 쿼리를 Mapping 시켜 데이터를 객체화 시킨다

![Untitled 2](https://user-images.githubusercontent.com/80089860/167233278-2420b6e2-fe81-41e1-b28c-b445f3bdaa98.png)

- **JDBC Template**
    - 쿼리 수행결과와 객체의 필드를 Mapping & RowMapper 재활용
    - JDBC에서 반복적으로 해야하는 많은 작업들을 대신해준다

- **Mybatis**
    - ***SQL Mapper의 대표적인 Framework***
        - 반복적인 JDBC 프로그래밍을 단순화 SQL 쿼리들을 xml 파일에 작성하여 코드와 sql을 분리하여 관리한다
        - JDBC만 사용하면 결과를 가져와서 객체의 인스턴스에 매핑하기 위한 많은 코드가 필요하겠지만 Mybatis는 그 코드들을 작성하지 않아도 되게 해준다
        - 
- 자동으로 Connection 관리를 해주면서 JDBC를 사용할 때의 중복작업 대부분을 없애준다
- 복잡한 쿼리나 다이나믹하게 변경되는 쿼리 작성이 쉽다
- DAO로부터 sql문을 분리하여 코드의 간결성 및 유지보수성 향상
    
![Untitled 3](https://user-images.githubusercontent.com/80089860/167233281-65b164f8-a805-4ba1-95ae-c08b9f2bf84a.png) 

**Persist Framework인 SQL Mapper를 통해 많은 편리함을 느낄 수 있었지만,**

**단점도 분명 존재한다**

1. **특정 DB에 종속성으로 사용하기 쉽다**
    1. 테이블마다 비슷한 CRUD SQL = DAO 개발이 매우 반복되는 작업
    2. 테이블 필드가 변경될 시 이와 관련된 모든 DAO의 SQL문, 객체의 필드 등을 수정해야 한다
    3. 코드상으로 sql과 jdbc api를 분리했다 하더라도, 논리적으로 강한 의존성을 가지고 있다

![Untitled 4](https://user-images.githubusercontent.com/80089860/167233285-8b54d432-fa1f-4b52-bfa3-9b5d85ddf767.png)

1. **ORM(Object Relational Mapping)**

![Untitled 5](https://user-images.githubusercontent.com/80089860/167233290-7a553351-6d9c-4690-9787-7508f938dd6d.png)

![Untitled 6](https://user-images.githubusercontent.com/80089860/167233292-192d2bfb-dc58-4f62-a412-367661e4494b.png)

ORM의 대표적인 예로는 JPA가 있다

### **ORM이란?**

참고 : [https://sanseongko.github.io/java-orm](https://sanseongko.github.io/java-orm)

Object Relational Mapping, 말 그대로 객체-관계 매핑이라는 것이다. 

다만 RDB는 테이블로 이루어져 있고, OPP 객체지향 프로그래밍에서는 클래스를 사용하게 된다.\

하지만 객체와 관계형 데이터베이스가 애초에 호환을 염두 하고 만들어 진 것이 아니다보니, 자연스럽게 불일치가 발생하게 된다. 

**이럴때 ORM을 사용하여 객체의 관계를 바탕으로 SQL문을 자동적으로 생성 불일치를 해결한다.**

ORM Framwork는 하이버네이트, 이클립스 링크 등 위의 세 가지가 있는데,

가장 많이 쓰이는 프레임워크는 하이버네이트 이다.

### 패러다임 불일치

![Untitled 7](https://user-images.githubusercontent.com/80089860/167233298-2c7f89d4-bb8f-48cf-9740-0f24b388ca69.png)

상속이라는 개념이 없기 때문에, 아래와 같이 번거로움이 생긴다

![Untitled 8](https://user-images.githubusercontent.com/80089860/167233300-c068b113-a1a4-47f1-ae89-85507fff1180.png)

### JPA가 번거로움을 해결해준다

![Untitled 9](https://user-images.githubusercontent.com/80089860/167233307-8b638340-01df-4728-8527-492489368929.png)

![Untitled 10](https://user-images.githubusercontent.com/80089860/167233308-f21b13e9-6459-4cef-9e74-f01fb79ba7b4.png)

### 결론

![Untitled 11](https://user-images.githubusercontent.com/80089860/167233314-1d71af23-f8a6-4d3b-a9c3-98b96cae89ce.png)

![Untitled 12](https://user-images.githubusercontent.com/80089860/167233315-be0ff50f-244c-465c-9ccb-71fe51565676.png)
