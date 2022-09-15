# Transcation
## 트랜잭션이란?
일련의 작업

일련의 작업은 모두 에러 없이 끝나야 하며, 에러 발생 시 에러 발생 이전 시점까지 작업되었던 내용은 모두 원상복구 되어야한다.

데이터 무결성을 보장하기 위한 처리방법 = 트랜잭션 처리

## Spring에서 제공하는 트랜잭션 처리방법
- 선언적 트랜잭션
- @Transactional 어노테이션을 통한 트랜잭션

1. 선언적 트랜잭션
    * Xml 트랜잭션에 대한 설정을 함으로써 트랜잭션을 적용할 범위와 대상을 선언하는 방식
    * context-transaction.xml(전자정부프레임워크 표준)
        * 트랜잭션 설정을 위한 org.springframework.jdbc.datasource.DataSourceTransactionManager 클래스를 transactionManager 이라는 이름의 빈으로 등록
            * \<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager"> 		\<property name="dataSource" ref="dataSource"/>
            \</bean>
        * 선언적 트랜잭션 처리는 AOP를 이용
            \<!-- Transaction을 위한 AOP 설정 --><aop:config proxy-target-class="true">	<aop:pointcut id="servicePublicMethod" expression="execution(public * com.freehoon.web.board..*(int))" />	<aop:advisor advice-ref="txAdvice" pointcut-ref="servicePublicMethod" /></aop:config>
            * aop:pointcut 은 aop pointcut를 지정하기위한 속성.
            * aop의 pointcut 은 공통기능을 적용 할 대상을 지정한다는 뜻.

            * aop:advice 는 공통기능을 가지고 있는 가지고 있는 구현체를 뜻한다.
            * 속성으로 사용된 advice-ref 속성으로 구현체의 빈을 지정하고, 이 구현체를 적용할 대상을 pointcut-ref에 지정합니다.
