---

---

[[예제로 배우는 스프링 입문] 1. 강좌 소개](https://www.youtube.com/watch?v=HACQV_koAIU&list=PLfI752FpVCS8_5t29DWnsrL9NudvKDAKY&index=1)

강의

[spring-projects/spring-petclinic](https://github.com/spring-projects/spring-petclinic)

실습에 이용할 예제 프로젝트

---

## IntelliJ 꿀팁

---

`shift + shift` : 전체검색( file, action 모두 포함 )

`command + e` : 최근 열었던 파일

`command + n` : Generate 기능 → 생성자나 getter, setter 메소드 그냥 만들어주는 기능

스프링 프레임워크(이하, 스프링)를 사용한 예제 코드를 보며 스프링의 주요 철학과 기능을 빠르게 학습한다.

### 강좌 목표

- 실제 코드를 보며 스프링 프레임워크에 대한 소개를 한다.
- 스프링이 개발자에게 주는 가치를 이해한다.
- 스프링의 주요 기능을 짧은 시간 내에 간략하게 이해하는 것을 목표로 한다.

예제 프로젝트를 클론해온다.

이후 프로젝트 폴더에서 `./mvnw package` 명령 진행. → 의존성 받아오기

`java -jar target/*.jar` 명령으로 jar(java archive) 파일 실행

    2020-03-27 10:27:12.813  INFO 60997 --- [           main] j.LocalContainerEntityManagerFactoryBean : Initialized JPA EntityManagerFactory for persistence unit 'default'
    2020-03-27 10:27:13.610  INFO 60997 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
    2020-03-27 10:27:14.759  INFO 60997 --- [           main] o.s.b.a.e.web.EndpointLinksResolver      : Exposing 13 endpoint(s) beneath base path '/manage'
    2020-03-27 10:27:14.836  INFO 60997 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
    2020-03-27 10:27:14.840  INFO 60997 --- [           main] o.s.s.petclinic.PetClinicApplication     : Started PetClinicApplication in 6.302 seconds (JVM running for 6.704)
    2020-03-27 10:28:08.089  INFO 60997 --- [nio-8080-exec-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring DispatcherServlet 'dispatcherServlet'
    2020-03-27 10:28:08.090  INFO 60997 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : Initializing Servlet 'dispatcherServlet'
    2020-03-27 10:28:08.099  INFO 60997 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : Completed initialization in 9 ms

실행 이후 터미널을 살펴보면 `Tomca` 이 8080 포트로 실행되었다는 로그를 볼 수 있음.

로컬호스트 접속

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/062ea628-37c5-4136-b217-6e97d3d7318a/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/062ea628-37c5-4136-b217-6e97d3d7318a/Untitled.png)

정상적으로 접속이 되었다.

git에서 프로젝트를 클론 받아서 `maven` 으로 빌드를 하고 진행.

웹 애플리케이션임에도 불구하고 자바를 통해 빌드할 수 있다.

### 로그분석

---

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e768ed32-7493-450a-be85-27b06ef097bf/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e768ed32-7493-450a-be85-27b06ef097bf/Untitled.png)

src/main/resources/application.properties 파일을 연다.

    # Logging
    logging.level.org.springframework=INFO
    # logging.level.org.springframework.web=DEBUG
    # logging.level.org.springframework.context.annotation=TRACE

로그레벨을 DEBUG로 변경한다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5be94d57-606a-41b5-8dc4-f378da3ce293/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5be94d57-606a-41b5-8dc4-f378da3ce293/Untitled.png)

이후 프로젝트를 빌드하고 접속한 뒤 기능을 실행하면 debug 레벨에 따른 로그들이 나온다.

    2020-03-27 10:56:03.951 DEBUG 75515 --- [nio-8080-exec-1] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped to org.springframework.samples.petclinic.system.WelcomeController#welcome()
    2020-03-27 10:56:03.953 DEBUG 75515 --- [nio-8080-exec-1] o.s.w.s.v.ContentNegotiatingViewResolver : Selected 'text/html' given [text/html, application/xhtml+xml, image/webp, image/apng, application/xml;q=0.9, application/signed-exchange;v=b3;q=0.9, */*;q=0.8]
    2020-03-27 10:56:03.978 DEBUG 75515 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : Completed 200 OK
    2020-03-27 10:56:04.091 DEBUG 75515 --- [nio-8080-exec-2] o.s.web.servlet.DispatcherServlet        : GET "/images/spring-logo-dataflow.png", parameters={}
    2020-03-27 10:56:04.092 DEBUG 75515 --- [nio-8080-exec-2] o.s.w.s.handler.SimpleUrlHandlerMapping  : Mapped to ResourceHttpRequestHandler ["classpath:/META-INF/resources/", "classpath:/resources/", "classpath:/static/", "classpath:/public/", "/"]
    2020-03-27 10:56:04.093 DEBUG 75515 --- [nio-8080-exec-2] o.s.w.s.r.ResourceHttpRequestHandler     : Resource not found
    2020-03-27 10:56:04.094 DEBUG 75515 --- [nio-8080-exec-2] o.s.web.servlet.DispatcherServlet        : Completed 404 NOT_FOUND
    2020-03-27 10:56:04.094 DEBUG 75515 --- [nio-8080-exec-2] o.s.web.servlet.DispatcherServlet        : "ERROR" dispatch for GET "/error", parameters={}
    2020-03-27 10:56:04.095 DEBUG 75515 --- [nio-8080-exec-2] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped to org.springframework.boot.autoconfigure.web.servlet.error.BasicErrorController#error(HttpServletRequest)
    2020-03-27 10:56:04.097 DEBUG 75515 --- [nio-8080-exec-2] o.s.w.s.m.m.a.HttpEntityMethodProcessor  : Using 'application/json;q=0.8', given [image/webp, image/apng, image/*, */*;q=0.8] and supported [application/json, application/*+json, application/json, application/*+json]
    2020-03-27 10:56:04.097 DEBUG 75515 --- [nio-8080-exec-2] o.s.w.s.m.m.a.HttpEntityMethodProcessor  : Writing [{timestamp=Fri Mar 27 10:56:04 KST 2020, status=404, error=Not Found, message=No message available,  (truncated)...]
    2020-03-27 10:56:04.099 DEBUG 75515 --- [nio-8080-exec-2] o.s.web.servlet.DispatcherServlet        : Exiting from "ERROR" dispatch, status 404
    2020-03-27 10:56:04.122 DEBUG 75515 --- [nio-8080-exec-3] o.s.web.servlet.DispatcherServlet        : GET "/resources/images/favicon.png", parameters={}
    2020-03-27 10:56:04.123 DEBUG 75515 --- [nio-8080-exec-3] o.s.w.s.handler.SimpleUrlHandlerMapping  : Mapped to ResourceHttpRequestHandler ["classpath:/META-INF/resources/", "classpath:/resources/", "classpath:/static/", "classpath:/public/", "/"]
    2020-03-27 10:56:04.124 DEBUG 75515 --- [nio-8080-exec-3] o.s.web.servlet.DispatcherServlet        : Completed 200 OK

`DispatcherServlet` 이라는 클래스가 일을 열심히 하는것이 보인다.

스프링이 제공하는 서블릿이다.

웹 페이지에서 `FIND OWNERS` 페이지를 요청하면 url이 아래와 같이 요청된다.

`[localhost:8080/owners/new](http://localhost:8080/owners/new)` 로 요청이된다. 그리고 로그를 살펴보면 

    2020-03-27 13:28:05.858 DEBUG 24767 --- [nio-8080-exec-8] o.s.web.servlet.DispatcherServlet        : GET "/owners/new", parameters={}
    2020-03-27 13:28:05.859 DEBUG 24767 --- [nio-8080-exec-8] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped to org.springframework.samples.petclinic.owner.OwnerController#initCreationForm(Map)
    2020-03-27 13:28:05.860 DEBUG 24767 --- [nio-8080-exec-8] o.s.w.s.v.ContentNegotiatingViewResolver : Selected 'text/html' given [text/html, application/xhtml+xml, image/webp, image/apng, application/xml;q=0.9, application/signed-exchange;v=b3;q=0.9, */*;q=0.8]

위와 같은 로그를 살펴볼 수 있다.

`/owners/new` 페이지 값을 요청하고 `RequestMappingHandeler`가 호출하는 메소드가 무엇인지 로그로 보여준다.

`petclinic.owner.OwnerController#initCreationForm` 메소드를 확인한다.

    @GetMapping("/owners/new")
    	public String initCreationForm(Map<String, Object> model) {
    		Owner owner = new Owner();
    		model.put("owner", owner);
    		return VIEWS_OWNER_CREATE_OR_UPDATE_FORM;
    	}

Owner Type 의 owner 객체를 생성하고 model에 이를 넣는다.

이후, `VIEWS_OWNER_CREATE_OR_UPDATE_FORM` 이라는 문자열을 리턴한다.

이를 따라들어가보면 `[OwnerControlle](http://ownercontroller.java)` 클래스가  보인다.

    @Controller
    class OwnerController {
    
    	private static final String VIEWS_OWNER_CREATE_OR_UPDATE_FORM = "owners/createOrUpdateOwnerForm";
    
    	private final OwnerRepository owners;
    
    	private VisitRepository visits;
    
    	public OwnerController(OwnerRepository clinicService, VisitRepository visits) {
    		this.owners = clinicService;
    		this.visits = visits;
    	}
    
    	@InitBinder
    	public void setAllowedFields(WebDataBinder dataBinder) {
    		dataBinder.setDisallowedFields("id");
    	}
    
    	@GetMapping("/owners/new")
    	public String initCreationForm(Map<String, Object> model) {
    		Owner owner = new Owner();
    		model.put("owner", owner);
    		return VIEWS_OWNER_CREATE_OR_UPDATE_FORM;
    	}
    
    	@PostMapping("/owners/new")
    	public String processCreationForm(@Valid Owner owner, BindingResult result) {
    		if (result.hasErrors()) {
    			return VIEWS_OWNER_CREATE_OR_UPDATE_FORM;
    		}
    		else {
    			this.owners.save(owner);
    			return "redirect:/owners/" + owner.getId();
    		}
    	}
    
    	@GetMapping("/owners/find")
    	public String initFindForm(Map<String, Object> model) {
    		model.put("owner", new Owner());
    		return "owners/findOwners";
    	}
    
    

그리고 변수 `VIEWS_OWENR_CREATE_OR_UPDATE_FORM` 에 `owners/createOrUpdateOwnerForm` 라는 리소스를 저장해두었다.

해당 값은 `resource` 디렉토리에 위치한다 이를 살펴보자.

    <html xmlns:th="https://www.thymeleaf.org"
      th:replace="~{fragments/layout :: layout (~{::body},'owners')}">
    
    <body>
    
      <h2>Owner</h2>
      <form th:object="${owner}" class="form-horizontal" id="add-owner-form" method="post">
        <div class="form-group has-feedback">
          <input
            th:replace="~{fragments/inputField :: input ('First Name', 'firstName', 'text')}" />
          <input
            th:replace="~{fragments/inputField :: input ('Last Name', 'lastName', 'text')}" />
          <input
            th:replace="~{fragments/inputField :: input ('Address', 'address', 'text')}" />
          <input
            th:replace="~{fragments/inputField :: input ('City', 'city', 'text')}" />
          <input
            th:replace="~{fragments/inputField :: input ('Telephone', 'telephone', 'text')}" />
            <!--<input
                th:replace="~{fragments/inputField :: input ('Age', 'age', 'text')}" /> -->
        </div>
        <div class="form-group">
          <div class="col-sm-offset-2 col-sm-10">
            <button
              th:with="text=${owner['new']} ? 'Add Owner' : 'Update Owner'"
              class="btn btn-default" type="submit" th:text="${text}">Add
              Owner</button>
          </div>
        </div>
      </form>
    </body>
    </html>

`html` 파일이다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/73ef56f3-9364-4510-9da9-0c203bebe395/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/73ef56f3-9364-4510-9da9-0c203bebe395/Untitled.png)

이 값이 클라이언트에 뿌려지는 것이다.

플로우 흐름을 이해하는 것이 매우 매우 중요함!

 

---

---

코드 수정 과제

-  LastName이 아니라 FirstName으로 검색하는 기능
-  정확히 일치하는 키워드가 아니여도 그냥 키워드가 들어가있으면 검색해주는 기능
-  Owner에 Age 필드 추가

1. **LastName이 아니라 FirstName으로 검색하는 기능**
    - 로그를 보고 호출하는 메소드를 트레이싱하면서 `last` → `first`로 변경하고

    @Query("SELECT DISTINCT owner FROM Owner owner left join fetch owner.pets WHERE owner.lastName LIKE :lastName%")
    	@Transactional(readOnly = true)
    	Collection<Owner> findByLastName(@Param("lastName") String lastName);

기존쿼리와 `findByLastName` 메소드를 firstName을 기준으로 찾아내도록 변경한다.

    @Query("SELECT DISTINCT owner FROM Owner owner left join fetch owner.pets WHERE owner.firstName LIKE :firstName%")
        @Transactional(readOnly = true)
        Collection<Owner> findByFirstName(@Param("firstName") String firstName);

**2. 정확히 일치하는 키워드가 아니여도 검색하는 기능**

핵심은 와일드카드다.

위에서 Query를 전송하는 부분

    @Query("SELECT DISTINCT owner FROM Owner owner left join fetch owner.pets WHERE owner.firstName LIKE :firstName%")

맨 꼬리쪽을 보면 LIKE 절에  ` :firstName%` 을 보면 알 수 있듯, 뒷 부분에 와일드카드를 사용한다.

이를 %:firstName% 으로 변경한다.  앞쪽에 와일드카드를 하나 더 준다.

콜론 부분 `:firstName` 이 부분이 입력받은 키워드로 바뀌기 때문에 중간에 넣으면 안된다.

**3. Owner에 age 필드 추가**

    //owner.java
    private Integer age;
    
        public Integer getAge() {
            return age;
        }
    
        public void setAge(Integer age) {
            this.age = age;
        }

Owner 클래스에 age값과 getter, setter 메소드를 추가해준다.

그리고 실행시켜보면 `org.hsqldb.HsqlException: user lacks privilege or object not found: OWNER0_.AGEf` 라는 에러를 확인할 수 있다.

이는 DB에 AGE라는 컬럼이 없기 때문에 발생하는 에러다.

따라서 해당 컬럼을 DB 스키마에 추가 해줘야 한다.

이후 `[application.properties](http://application.properties)` 파일에 들어가면 db 스키마 위치를 알려주는데 이를 따라가서 owners 테이블을 수정한다.

    CREATE TABLE owners (
      id         INTEGER IDENTITY PRIMARY KEY,
      first_name VARCHAR(30),
      last_name  VARCHAR_IGNORECASE(30),
      age        INTEGER,
      address    VARCHAR(255),
      city       VARCHAR(80),
      telephone  VARCHAR(20)
    );

age를 추가한다.

이후 실행시켜보면 `org.hsqldb.HsqlException: row column count mismatch` 에러가 발생한다.

이름 그대로 row&column의 매치가 적절치 못하여 발생하는 에러다.

이거는 데이터에 맞게 값을 INSERT 해주지 않아서 발생하는 에러다.

이후 db의 데이터 파일을 들어가서

    INSERT INTO owners VALUES (1, 'George', 'Franklin', 20,'110 W. Liberty St.', 'Madison', '6085551023');
    INSERT INTO owners VALUES (2, 'Betty', 'Davis', 20, '638 Cardinal Ave.', 'Sun Prairie', '6085551749');
    INSERT INTO owners VALUES (3, 'Eduardo', 'Rodriquez', 20, '2693 Commerce St.', 'McFarland', '6085558763');
    INSERT INTO owners VALUES (4, 'Harold', 'Davis', 20, '563 Friendly St.', 'Windsor', '6085553198');
    INSERT INTO owners VALUES (5, 'Peter', 'McTavish', 20, '2387 S. Fair Way', 'Madison', '6085552765');
    INSERT INTO owners VALUES (6, 'Jean', 'Coleman', 20, '105 N. Lake St.', 'Monona', '6085552654');
    INSERT INTO owners VALUES (7, 'Jeff', 'Black', 20, '1450 Oak Blvd.', 'Monona', '6085555387');
    INSERT INTO owners VALUES (8, 'Maria', 'Escobito', 20, '345 Maple St.', 'Madison', '6085557683');
    INSERT INTO owners VALUES (9, 'David', 'Schroeder', 20, '2749 Blackhawk Trail', 'Madison', '6085559435');
    INSERT INTO owners VALUES (10, 'Carlos', 'Estaban', 20, '2335 Independence La.', 'Waunakee', '6085555487');

아까 삽입한 age위치 (4번째 멤버)에 나이값을 모두 추가해준다.

이후 `View`에 나이를 입력할 수 있는 폼을 만들어준다.

    <h2>Owner</h2>
      <form th:object="${owner}" class="form-horizontal" id="add-owner-form" method="post">
        <div class="form-group has-feedback">
          <input
            th:replace="~{fragments/inputField :: input ('First Name', 'firstName', 'text')}" />
          <input
            th:replace="~{fragments/inputField :: input ('Last Name', 'lastName', 'text')}" />
            <input
                    th:replace="~{fragments/inputField :: input ('Age', 'age', 'text')}" />
          <input
            th:replace="~{fragments/inputField :: input ('Address', 'address', 'text')}" />
          <input
            th:replace="~{fragments/inputField :: input ('City', 'city', 'text')}" />
          <input
            th:replace="~{fragments/inputField :: input ('Telephone', 'telephone', 'text')}" />

이 강의는 한번 더 보기
