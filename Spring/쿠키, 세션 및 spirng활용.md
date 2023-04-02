# 쿠키와 세션 정리 + Spring 활용법

**쿠키란?**

-   쿠키는 클라이언트와 서버 간의 상호작용에서 중요한 역할을 한다. 쿠키는 서버에서 생성되어 클라이언트에게 전송되며, 클라이언트 측에 저장된다.
-   쿠키는 일반적으로 사용자 인증, 세션 유지, 개인화 등의 목적으로 사용된다. 예를 들어, 사용자가 웹 사이트에 로그인할 때, 서버는 사용자 인증에 대한 정보를 쿠키에 저장하여 사용자가 다른 페이지를 방문할때마다 인증을 다시 수행하지 않아도 되도록 작용한다.

**쿠키의 특징**

-   상태 유지 - 쿠키는 클라이언트 측에 저장되기 때문에, 클라이언트와 서버 간의 상태를 유지할 수 있다. 이를 통해 사용자 인증, 세션 관리 등의 기능을 구현할 수 있다.
-   개인화 - 쿠키는 사용자의 선호도나 기타 개인 정보를 저장할 수 있기 때문에, 웹 사이트에서 개인화된 콘텐츠를 제공하는 데에 사용된다.
-   성능 향상 - 쿠키는 클라이언트 측에 저장되므로, 서버에 매번 요청을 보내지 않아도 ㄷ클라이언트의 이전 상태를 파악할 수 있다. 이를 통해 성능 향상을 기대할 수 있다.
-   보안 취약점 - 쿠키는 클라이언트에 저장되는 정보이므로, 보안 취약점을 가질 수 있다.

**쿠키의 동작방식**

1.  쿠키는 서버에서 생성되어 클라이언트의 로컬 브라우저에 저장된다.
2.  클라이언트가 동일한 서버에서 재요청할 때마다, 해당 서버는 클라이언트의 쿠키 정보를 참조하여 이전에 저장한 정보를 이용할 수 있다.
3.  쿠키는 클라이언트가 HTTP 요청을 보낼 때, 해당 요청에 포함되어 서버로 전송된다.
4.  서버는 쿠키에 저장된 정보를 이용하여 클라이언트를 식별하거나, 클라이언트의 상태 정보를 유지하는 등의 기능을 수행한다.

---

**세션이란?**

-   세션은 웹 서버와 클라이언트 간의 연결 상태를 유지하기 위한 기술이다. 일반적으로 서버에서 클라이언트의 상태 정보를 저장하고, 클라이언트는 세션ID를 쿠키를 통해 전달받아 해당 세션에 대한 정보를 서버에 요청합니다.
-   세션은 다양한 용도로 사용된다. 예를 들어, 사용자 인증, 장바구니, 선호 설정 등의 정보를 세션에 저장하여 사용자 경험을 개선할 수 있다. 일반적으로 메모리나 데이터베이스에 저장되며, 보안 상의 이유로 세션 데이터는 암호화되어 저장될 수 있다.

**세션의 특징**

-   클라이언트와 서버간의 데이터 전송량이 줄어들어 네트워크 부하를 줄일 수 있다.
-   세션은 클라이언트의 요청과 서버의 응답을 통해 고유한 ID를 발급받는다.
-   발급된 세션 ID를 쿠키를 이용하여 클라이언트에 저장한다.
-   세션은 일저 시간동안 유지되며, 일정 시간이 지나면 자동으로 만료되어 데이터가 삭제된다.
-   서버 측에서 상태 정보를 관리하기 때문에 쿠키보다 보안성이 높다.

**세션의 동작방식**

1.  클라이언트가 서버에 요청을 보낸다.
2.  서버는 클라이언트의 요청에 대한 응답으로 세션 ID를 생성한다.
3.  세션 ID는 쿠키를 통해 클라이언트에게 전달된다.
4.  클라이언트는 이후 요청에서 세션 ID를 쿠키를 통해 서버에 전달한다.
5.  서버는 세션 ID를 기반으로 해당 세션의 상태 정보를 가져오거나 업데이트한다.
6.  클라이언트가 세션을 종료하거나 만료되면, 서버는 세션 정보를 삭제한다.

---

**쿠키와 세션의 차이점**

-   저장 위치 - 쿠키는 클라이언트에 저장되고, 세션은 서버에 저장된다.
-   용도 - 쿠키는 클라이언트 상태를 유지하고, 사용자 정보를 저장하거나, 특정 기능을 사용할 때 사용된다. 세션은 서버에서 사용자 정보를 관리하거나, 로그인 상태를 유지하는 등의 목적으로 사용된다.
-   보안성 - 쿠키는 클라이언트에 저장되므로, 보안 취약점이 있을 수 있고, 세션은 서버에 저장되므로, 보안성이 더욱 높다.
-   데이터 크기 - 쿠키는 저장 가능한 데이터 크기에 제한이 있고, 세션은 서버에서 관리하므로 제한이 없다.
-   수명 - 쿠키는 설정된 만료일까지 유지되거나, 브라우저가 종료될 때까지 유지된다. 세션은 일정 시간이 지나면 만료되거나, 사용자가 로그아웃할 때까지 유지된다.
-   속도 - 쿠키는 클라이언트에서 처리되므로, 데이터를 읽고 쓰는 속도가 빠르다. 세션은 서버에서 처리되므로 상대적으로 느리다.
-   저장 형식 - 쿠키는 텍스트 형식, 세션은 객체 형태로 저장된다.

---

**※쿠키의 보안 취약점**

쿠키만 사용할 경우, 심각한 보안 문제가 있다.

-   쿠키 값은 임의로 변경할 수 있다.
    -   클라이언트 쿠키를 강제로 변경하면 다른 사용자가 된다.
    -   실제 웹 브라우저 개발자모드에서 cookie값을 바꿀 수 있다.
-   쿠키에 보관된 정보는 훔쳐갈 수 있다.
    -   쿠키에 중요한 정보가 있다면, 이 정보가 웹 브라우저에도 보관되고, 요청 때마다 서버로 전달된다.
    -   이 과정에서 로컬 PC가 털릴 수도 있고, 전송 구간에서 털릴 수도 있다.

---

**Spring에서 쿠키 사용하기**

```java
//쿠키 생성 로직
Cookie cookie = new Cookie("memberId", String,valueOf(loginMember.getId()));
response.addCookie(idCookie);
//쿠키에 시간 정보를 주지 않으면 브라우저 종료시 모두 종료(세션 쿠키)
```

쿠키는 controller에서 생성해준다.

```java
@GetMapping("/")
public String homeLogin(@CookieValue(name = "memberId", required = false) Long memberId, 
Model model) {
```

-   보통 쿠키 정보가 필요한 controller에 @CookieValue를 사용하면 된다.
-   @CookieValue를 사용하면 편리하게 쿠키를 조회할 수 있다.
-   로그인 하지 않은 사용자도 홈에 접근할 수 있기 때문에 required = false를 사용한다.
-   쿠키는 보안 취약점이 크기 때문에 단독으로 사용하는 경우가 거의 없다.

---

**세션 코드로 이해하기**

```java
@Component
public class SessionManager {

    private static final String SESSION_COOKIE_NAME = "mySessionId";
    private Map<String, Object> sessionStore = new ConcurrentHashMap<>(); // 동시성 문제

    //세션 생성
    public void createSession(Object value, HttpServletResponse response) {

        //session id 생성, 값을 세션에 저장
        String sessionID = UUID.randomUUID().toString();
        sessionStore.put(sessionID,value);

        //쿠키 생성
        Cookie mySessionCookie = new Cookie(SESSION_COOKIE_NAME, sessionID);
        response.addCookie(mySessionCookie);
    }

    //세션 조회
    public Object getSession(HttpServletRequest request) {
        Cookie sessionCookie = findCookie(request, SESSION_COOKIE_NAME);

        if (sessionCookie == null) {
            return null;
        }
        return sessionStore.get(sessionCookie.getValue());
    }

    //세션 만료
    public void expire(HttpServletRequest request) {
        Cookie sessionCookie = findCookie(request, SESSION_COOKIE_NAME);
        if (sessionCookie != null) {
            sessionStore.remove(sessionCookie.getValue());
        }
    }

    // 쿠키 찾는 로직
    private Cookie findCookie(HttpServletRequest request, String cookieName) {
        if (request.getCookies() == null) {
            return null;
        }
        return Arrays.stream(request.getCookies())
                .filter(cookie -> cookie.getName().equals(cookieName))
                .findAny()
                .orElse(null);
    }
}
```

-   세션은 sessionStore라는 ConcurrentHashMap(동시성 이슈 해결) 저장된다. 세션을 생성하면 UUID를 생성하여 이를 sessionStore에 저장하고, 클라이언트에게 쿠키를 보낸다.
-   세션 조회시, HttpServletRequest 객체에서 세션 쿠키를 찾아 sessionStore에서 해당 세션 값을 반환한다.
-   세션 만료시, HttpServletRequest 객체에서 세션 쿠키를 찾아 sessionStore에서 해당 세션을 제거한다.
-   findCookie() 에서는 HttpServletRequest 객체에서 getCookies()메소드를 이용하여 쿠키 배열을 가져오고, 이 배열에서 찾고자 하는 쿠키 이름과 일치하는 쿠키를 찾아 반환한다.

---

**Spring에서 Session 사용하기**

```java
@GetMapping("/") //로그인
public String homeLogin( 
	@SessionAttribute(name = SessionConst.LOGIN_MEMBER, required = false) 
    Member loginMember, Model model) {
 
 	//세션에 회원 데이터가 없으면 home
 	if (loginMember == null) {
 		return "home";
 	}
 	//세션이 유지되면 로그인으로 이동
 	model.addAttribute("member", loginMember);
 	return "loginHome";
}

@PostMapping("/logout") //로그아웃
    public String logout(HttpServletRequest request) {
        HttpSession session = request.getSession(false);
        if (session != null) { //세션이 있으면 만료시켜버리기!
            session.invalidate();
        }
        return "redirect:/";
    }
```

@SessionAttribute를 사용하면 spring에서 세션을 생성해준다.

또한 session.invalidate()를 사용해서 로그아웃 처리까지 수월하게 해준다.