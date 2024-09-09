<blockquote>
<p>비즈니스 컴포넌트 개발에서 가장 중요한 두가지 원칙은 ① 낮은 결합도 ② 높은 응집도 를 유지하는 것이다. 스프링의 의존성 주입(Dependency Injection)을 이용하면 비즈니스 컴포넌트를 구성하는 객체들의 결합도를 떨어뜨릴 수 있어서 의존관계를 쉽게 변경할 수 있다. 스프링의 IoC가 결합도와 관련된 기능이라면, AOP(Aspect Oriented Programming)은 응집도와 관련된 기능이라 할 수 있다. </p>
</blockquote>
<h2 id="aopaspect-oriented-programming-란">AOP(Aspect Oriented Programming) 란?</h2>
<p>AOP는 소프트웨어 공학에서의 프로그래밍 패러다임 중 하나로, 관점 지향 프로그래밍이라고도 한다. 주요 기능이나 모듈성을 가로지르는 &quot;관심사(Concern)&quot;를 모듈화하는 기술이다. 전통적인 객체지향 프로그래밍(OOP)은 데이터와 해당 데이터를 다루는 메서드를 하나의 클래스로 묶어 관리하는 반면, AOP는 애플리케이션의 트랜잭션 관리, 로깅, 예외 등과 같은 관심사들을 횡단(cross-cutting)하는 방식으로 분리하여 모듈화한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/baenna/post/41788b8b-796a-4add-95c6-0613a44c5241/image.jpg" /></p>
<p><strong>AOP는 특히 중복 코드를 줄이고 코드의 모듈성을 높이며, 시스템의 유지보수성을 개선하는 데 유용하다.</strong> 
AOP는 다음과 같은 주요 구성 요소로 이루어진다.</p>
<p><strong>관심사(Concern):</strong> AOP에서 관리하려는 주요 기능이나 모듈성을 가로지르는 특정 관심 영역이다. 예를 들어, 로깅은 하나의 관심사일 수 있다.
<strong>횡단 관심사(cross-cutting Concerns):</strong> 여러 모듈이나 객체에 걸쳐 있는 관심사를 말하며, AOP에서 이 관심사를 분리하여 모듈화한다.
<strong>Advice:</strong> 횡단 관심사를 언제 실행할 것인지에 대한 규칙이며, Advice는 특정 관심사에 대해 실행될 코드를 정의한다. 예를 들어, 메서드 실행 전에 로깅을 추가하는 Advice가 있을 수 있다.
<strong>Pointcut(포인트컷):</strong> 어떤 위치에서 Advice를 실행할지 결정하는 기준이다. 특정 메서드 호출, 특정 클래스의 모든 메서드 등을 포인트컷으로 정의할 수 있다.
<strong>Weaving:</strong> Advice를 실제 코드에 적용하여 실제 실행 코드에 횡단 관심사를 삽입하는 과정을 말한다. 이는 컴파일 시점, 로드 시점, 런타임 시점에서 발생할 수 있다.</p>
<p><strong>AOP는 OOP와 결합하여 사용되며, 주로 코드의 가독성과 유지보수성을 향상시키는 데 기여한다.</strong></p>
<p>++ 이에 반해 사용자의 요청에 따라 실제로 수행되는 핵심 비즈니스 로직은 <strong>핵심 관심사(Core Concerns)</strong>이라고 한다.</p>
<h3 id="spring-framework의-aspectj-지원을-사용하는-aopaspect-지향-프로그래밍의-간단한-샘플">Spring Framework의 AspectJ 지원을 사용하는 AOP(Aspect 지향 프로그래밍)의 간단한 샘플</h3>
<p>AOP를 사용하여 메서드 실행을 기록하는 기본 시나리오를 만들어보자.</p>
<h4 id="1-의존성-설정">1. 의존성 설정:</h4>
<p>먼저 Maven 또는 Gradle을 사용하여 Spring AOP 의존성을 추가해야 한다.</p>
<pre><code>xml

&lt;!-- pom.xml --&gt;
    &lt;dependency&gt;
        &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
        &lt;artifactId&gt;spring-boot-starter-aop&lt;/artifactId&gt;
    &lt;/dependency&gt;</code></pre><h4 id="2-aspect-클래스-작성">2. Aspect 클래스 작성:</h4>
<p>Advice와 Pointcut을 정의하는 Aspect 클래스를 생성</p>
<pre><code>java

package com.example.demo.aspect;

import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.springframework.stereotype.Component;

@Aspect
@Component
public class LoggingAspect {

    // Advice 정의: 메서드 실행 전에 로깅을 추가
    @Before(&quot;execution(* com.example.demo.service.*.*(..))&quot;)
    public void beforeMethodExecution() {
        System.out.println(&quot;메서드 실행 전에 로깅을 추가&quot;);
    }
}
</code></pre><p><strong>@Aspect:</strong> 이 어노테이션은 이 클래스가 Aspect로 사용됨을 표시한다.
<strong>@Before:</strong> Advice를 정의. 여기서는 execution(* com.example.demo.service.<em>.</em>(..))라는 Pointcut을 정의하였다. 이는 com.example.demo.service 패키지의 모든 메서드 실행 전에 Advice가 실행됨을 의미한다.</p>
<h4 id="3-서비스-클래스-작성">3. 서비스 클래스 작성:</h4>
<p>AOP가 적용될 서비스 클래스를 만든다.</p>
<pre><code>java

package com.example.demo.service;

import org.springframework.stereotype.Service;

@Service
public class MyService {

    public void doSomething() {
        System.out.println(&quot;서비스 클래스에서 핵심 로직을 수행&quot;);
    }
}</code></pre><h4 id="4-메인-애플리케이션-클래스-작성">4. 메인 애플리케이션 클래스 작성:</h4>
<p>Spring을 설정하고 Aspect를 적용할 메인 클래스를 작성한다.</p>
<pre><code>java

package com.example.demo;

import com.example.demo.service.MyService;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.EnableAspectJAutoProxy;

@Configuration
@ComponentScan(&quot;com.example.demo&quot;)
@EnableAspectJAutoProxy
public class DemoApplication {

    public static void main(String[] args) {
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(DemoApplication.class);

        MyService myService = context.getBean(MyService.class);
        myService.doSomething();

        context.close();
    }
}</code></pre><p><strong>@Configuration:</strong> 이 어노테이션은 이 클래스가 Spring의 설정 클래스임을 표시
<strong>@ComponentScan:</strong> Spring에게 com.example.demo 패키지에서 빈을 찾도록 지시
<strong>@EnableAspectJAutoProxy:</strong> Spring AOP를 활성화</p>
<p>이 예제에서는 MyService 클래스의 doSomething() 메서드가 실행될 때 AOP에 의해 Aspect에서 정의한 Advice가 실행되어 &quot;메서드 실행 전에 로깅을 추가&quot;라는 메시지가 출력된다.</p>
<p>이러한 방식으로 AOP를 사용하면 횡단 관심사(로깅, 트랜잭션 관리, 예외 등)를 기존의 핵심 로직에서 분리하여 모듈화할 수 있다. AOP는 코드의 재사용성을 높이고 유지보수성을 개선하는 데 큰 도움이 된다.</p>