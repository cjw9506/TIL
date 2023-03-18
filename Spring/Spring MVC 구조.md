# Spring MVC 구조 이해

> -   스프링 MVC 전체 구조
      ​
      ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcDwFvc%2Fbtr4thrridI%2FNiW0tfMienIvMJGL4GWGcK%2Fimg.png)
      
---

-   **디스패처 서블릿**
    
    Spring MVC에서 프론트 컨트롤러 패턴을 구현한 Servlet이다.
    
    **그렇다면 프론트 컨트롤러란?**
    
    프론트 컨트롤러란 서블릿 컨테이너의 가장 앞단으로 HTTP 프로토콜로 들어오는 모든 요청을 받아 적합한 컨트롤러에 위임해주는 컨트롤러이다. 스프링 MVC의 핵심이라 할 수 있다.
    
-   프론트 컨트롤러 패턴 특징
    -   프론트 컨트롤러 서블릿 하나로 클라이언트의 요청을 받음
    -   요청에 맞는 컨트롤러를 찾아서 호출
    -   입구를 하나로
    -   공통 처리 가능
    -   프론트 컨트롤러를 제외한 나머지 컨트롤러는 서블릿을 사용하지 않아도 됨
        ​
-   프론트 컨트롤러 도입 전/후
    
    **도입전**
    
    ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdYkbbd%2Fbtr4v9ljHtt%2FKDUyasrOqp6tw9IjSj7seK%2Fimg.png)
    
    **도입후**
    
    ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Feb8VBq%2Fbtr4tiYa0X0%2FSiOllu8WATeBKDnQRGiOvK%2Fimg.png)
    
---

**디스패처 서블릿의 역할**

서블릿이 호출되면 HttpServlet이 제공하는 service()가 호출된다.  
service()를 시작으로 여러 메서드가 호출되면서 DispatcherServlet.doDispatch()가 호출된다.

doDispatch()를 살펴보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F8j77O%2Fbtr4vnYqcMy%2Fe6okKWpV4wx45ca1bQlIm1%2Fimg.png)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbAAEV3%2Fbtr4xjua0Ng%2FvULUKxwuE7plxSLeHq1KyK%2Fimg.png)


-   **동작 순서**
    
1.  핸들러 조회 - 핸들러 매핑을 통해 요청 URL에 매핑된 핸들러(컨트롤러)를 조회한다.
2.  핸들러 어댑터 조회 - 핸들러를 실행할 수 있는 핸들러 어댑터를 조회한다.
3.  핸들러 어댑터 실행
4.  핸들러 실행
5.  ModelAndView 반환 - 핸들러 어댑터는 핸들러가 반환하는 정보를 ModelAndView로 변환해서 반환한다.
6.  viewResolver 호출 - 뷰 리졸버를 찾고 실행한다.
7.  view반환 - 뷰 리졸버는 뷰의 논리 이름을 물리 이름으로 바꾸고, 렌더링 역할을 담당하는 뷰 객체를 반환한다.
    
---

-   **핸들러 매핑과 핸들러 어댑터**
    
    HandlerMapping - 핸들러 매핑에서 해당 컨트롤러를 찾을 수 있어야 한다.
    
    HandlerAdapter - 핸들러 매핑을 통해 찾은 핸들러를 실행할 수 있는 핸들러 어댑터가 필요하다.
    
-   **스프링부트가 자동 등록하는 핸들러 매핑과 핸들러 어댑터**
    
    ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb8B9DM%2Fbtr4tMScNEq%2FerCbXgbocR1SKmYt89iKFk%2Fimg.png)
    
-    핸들러 매핑으로 핸들러 조회
     1.  HandlerMapping을 순서대로 실행해서 핸들러를 찾는다.
     2.  빈 이름으로 핸들러를 찾아야 하기 때문에 BeanNameUrlHandlerMapping이 실행에 성공하고 Controller를 반환한다.
-   핸들러 어댑터 조회
    1.  HandlerAdapter의 supports()를 순서대로 실행한다.
    2.  SImpleControllerHandlerAdapter가 Controller인터페이스를 지원하므로 대상이 된다.
-   핸들러 어댑터 실행
    1.  디스패처 서블릿이 조회한 SImpleControllerHandlerAdapter를 실행하면서 핸들러 정보도 함께 반환한다.
    2.  SimpleControllerHandlerAdapter는 핸들러(Controller)를 내부에서 실행하고, 그 결과를 반환한다.
        
---

-   **뷰 리졸버**
    
    ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FV2nyZ%2Fbtr4t6iG0Vy%2FSwbWE19M1t3xZ8otD4xg2k%2Fimg.png)
    
-   OldController의 handleRequest()는 ModelAndView를 반환하며 논리적 view 이름은 new-form이다.
-   이 논리적 view 이름을 실제 서버 리소스상에 있는 view파일을 찾아서 물리 뷰 이름을 찾는 과정을 진행하는데 사용되는 것이 viewResolver이다.
    
-   스프링부트가 자동 등록하는 뷰 리졸버
    
    ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FFdKkk%2Fbtr4t5qAPyk%2FlIgkfJbIX2BtoqdUrLjhiK%2Fimg.png)
    
1.  new-form이라는 뷰 이름으로 viewResolver를 순서대로 호출한다.
2.  viewResolver가 호출되면 BeanNameViewResolver는 new-form이라는 이름의 스프링 빈으로 등록된 뷰를 찾아야 하는데 없다.
    
1.  InternalResourceViewResolver가 호출되고, 이 뷰 리졸버는 InternalResourceView를 반환한다.
2.  InternalResourceView는 forward()를 처리할 수 있는 경우에 사용한다.
3.  view.render()가 호출되고 InternalResourceView는 forward()를 사용해서 JSP를 실행한다.
    
    **※ forward() 란**
    
    다른 서블릿이나 JSP로 이동할 수 있는 기능이다. 서버 내부에서 다시 호출이 발생한다.