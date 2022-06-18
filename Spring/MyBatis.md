## Mybtis HikariCP 설정관련 

package com.study.shop;

```java
import javax.sql.DataSource;

import org.apache.ibatis.session.SqlSessionFactory;
import org.mybatis.spring.SqlSessionFactoryBean;
import org.mybatis.spring.SqlSessionTemplate;
import org.mybatis.spring.annotation.MapperScan;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.PropertySource;

import com.zaxxer.hikari.HikariConfig;
import com.zaxxer.hikari.HikariDataSource;

@Configuration
@PropertySource("classpath:/application.properties")  // 설정 파일 위치
@MapperScan(basePackages= {"com.study.*"})
public class DatabaseConfiguration {
  @Autowired
  private ApplicationContext applicationContext;

  @Bean
  @ConfigurationProperties(prefix="spring.datasource.hikari") // 설정 파일의 접두사 선언 
  public HikariConfig hikariConfig() {
      return new HikariConfig();
  }

  @Bean
  public DataSource dataSource() throws Exception{
      DataSource dataSource = new HikariDataSource(hikariConfig());
      System.out.println(dataSource.toString());  // 정상적으로 연결 되었는지 해시코드로 확인
      return dataSource;
  }

  @Bean
  public SqlSessionFactory sqlSessionFactory(DataSource dataSource) throws Exception{
      SqlSessionFactoryBean sqlSessionFactoryBean = new SqlSessionFactoryBean();
      sqlSessionFactoryBean.setDataSource(dataSource);
      sqlSessionFactoryBean.setMapperLocations(applicationContext.getResources("classpath:/mybatis/**/*.xml"));   
      return sqlSessionFactoryBean.getObject();
  }

  @Bean
  public SqlSessionTemplate sqlSessionTemplate(SqlSessionFactory sqlSessionFactory){
      return new SqlSessionTemplate(sqlSessionFactory);
  }
}
```



application.properties

```properties
server.port=8000
# DEVTOOLS (DevToolsProperties)
spring.devtools.livereload.enabled=true
#jsp설정
spring.mvc.view.prefix=/WEB-INF/views/
spring.mvc.view.suffix=.jsp
#mysql
spring.datasource.hikari.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.hikari.jdbc-url=jdbc:mysql://127.0.0.1:3306/webtest?useUnicode=true&characterEncoding=utf8
spring.datasource.hikari.username=아이디
spring.datasource.hikari.password=비번
# All DBMS
spring.datasource.hikari.maximum-pool-size=10
spring.datasource.hikari.minimum-idle=5
spring.datasource.hikari.connection-timeout=5000
```





.mxl 기본설정



```xml
<?xml version="1.0" encoding="UTF-8" ?> 
<!DOCTYPE mapper
PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.study.member.매퍼클래스이름"> //경로 
    

    </mapper>
```



build.grade dependencies 추가

```xml
//myBatis
	implementation 'org.mybatis.spring.boot:mybatis-spring-boot-starter:2.2.2'

//mySQL
	runtimeOnly 'mysql:mysql-connector-java'
```



**1. application.properties의 설정 정보를 토대로 HikariCP 설정**

**2. SqlSessionFactory에 HikariCP의 Datasource, Mybatis Mapper 경로, TypeAliase 패키지 경로 설정**

* Mybatis Mapper : Mybatis의 SqlSession에서 불러올 쿼리 정보가 담겨있다.

* TypeAliase : DB 테이블과 매칭될 자바 VO 객체를 지정해준다.



```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="board">
    <insert id="insertBoard" parameterType="board">
        INSERT INTO BOARD(TITLE, CONTENT)
        VALUES (#{title}, #{content})
    </insert>
    <select id="findBoardAll" resultType="board">
        SELECT BOARD_NO as boardNo
            , TITLE as title
            , CONTENT as content
            , REG_DATE as regDate
        FROM BOARD
    </select>
    <select id="findBoardById" parameterType="int" resultType="board">
        SELECT BOARD_NO as boardNo
            , TITLE as title
            , CONTENT as content
            , REG_DATE as regDate
        FROM BOARD
        WHERE BOARD_NO = #{boardNo}
    </select>
</mapper>
```

**· namespace** : 자바의 SqlSession에서 사용할 매퍼의 별칭

**· id** : 자바의 SqlSession에서 사용할 쿼리문의 별칭

**· parameterType** : 쿼리에서 사용될 매개변수의 타입 지정

**· resultType** : 쿼리의 결과를 담을 자바 클래스 지정

 

 SqlSession에서 namespace와 id는 'namespace.id'와 같은 형식으로 사용된다.

* ex. board.insertBoard

 

 parameterType을 지정해준 후 '**#{java 변수명}'**의 형식으로 쿼리에 넣어주면 된다. 

 

 parameterType과 resultType의 경우 위에서 TypeAliase를 설정해주었기 때문에 자바 클래스 이름의 lowercase만 작성해도 정상적으로 매핑이 된다. 만약 따로 지정을 해주지 않은 경우에는 패키지명까지 전부 명시해주어야 한다. 

* ex. board -> hello.test.domain.Board

 

이제 스프링 빈으로 등록된 SqlSession으로 매퍼에 등록된 쿼리를 실행시킬 수 있다.



### :star_of_david: Hikari CP 는 스프링부트 2.0 이상 프로젝트를 생성하면 property 설정만으로 사용이가능하다

* build.gradle 에 dependencies 설정 추가해야하는것은 필수적으로
  * jdbc
  * mysql
  * myBatis

```xml
//myBatis
	implementation 'org.mybatis.spring.boot:mybatis-spring-boot-starter:2.2.2'

//mySQL
	runtimeOnly 'mysql:mysql-connector-java'
	
//Jdbc
	implementation 'org.springframework.boot:spring-boot-starter-jdbc'
```

