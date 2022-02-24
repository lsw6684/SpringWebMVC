# SpringWebMVC
- [Web Server](#web-server)
- [WAS](#was)
- [Servlet](#servlet)

## Web Server
1. HTTP 기반으로 동작 <br />
2. 정적 리소스 제공, 기타 부가 기능<br />
3. 정적(파일) HTML, CSS, JS, 이미지, 영상 등 <br />
ex) NGINX, APACHE

## WAS
1. HTTP 기반으로 동작<br />
2. 웹 서버 기능 포함 + (정적 리소스 제공 가능)<br />
3. 프로그램 코드를 실행하여 애플리케이션 로직 수행 가능.<br />
-   - 동적 HTML, HTTP API(JSON)
    - 서블릿, JSP, 스프링 MVC
ex) Tomcat Jetty, Undertow

### Web Server VS WAS
- 웹 서버는 정적 리소스, WAS는 애플리케이션 로직. 하지만, 둘의 경계는 모호합니다.
    - 웹 서버도 프로그램을 실행하는 기능을 포함할 수 있습니다.
    - WAS도 웹 서버의 기능을 제공합니다.
- WAS는 애플리케이션 코드를 실행하는 데 더 특화되어 있습니다.

## Servlet
- urlPatterns(/hello)의 URL이 호출되면 서블릿 코드가 실행됩니다.
- **HttpServletRequest** : HTTP 요청 정보를 편리하게 사용할 수 있습니다.
- **HttpServletResponse** : HTTP 응답 정보를 편리하게 제공합니다.
- HTTP 스펙을 매우 편리하게 사용할 수 있습니다.
```java
@WebServlet(name = "helloServlet", urlPatterns = "/hello")
public class HelloServlet extends HttpServlet {

    @Override
    protected void service(HttpServletRequest request, HttpServletResponse response) {
        //애플리케이션 로직
    }
}
```
### Servlet - HTTP 요청, 응답 흐름
HTTP 요청 시
 - WAS는 Request, Response 객체를 새로 만들어서 서블릿 객체 호출.
 - 개발자는 Request 객체에서 HTTP 요청 정보를 편리하게 꺼내서 사용.
 - 개발자는 Response 객체에 HTTP 응답 정보를 편리하게 입력.
 - WAS는 Response 객체에 담겨있는 내용으로 HTTP 응답 정보를 생성.

### 서블릿 컨테이너
서블릿 객체를 자동으로 생성해 줍니다.
- 톰캣처럼 서블릿을 지원하는 WAS를 서블릿 컨테이너라고 합니다.
- 서블릿 컨테이너는 서블릿 객체를 생성, 초기화, 호출, 종료하는 **생명주기**를 관리합니다.
- 서블릿 객체는 **싱글톤**으로 관리합니다.
    - 고객 요청이 올 때 마다 객체를 생성하는 것은 비효율.
    - 최초 로딩 시점에 서블릿 객체를 미리 만들어서 재활용.
    - 모든 고객 요청은 동일한 서블릿 객체 인스턴스에 접근.
    - **공유 변수(멤버 변수) 사용 주의**
    - 서블릿 컨테이너 종료시 함께 종료
- JSP도 서블릿으로 변환 되어서 사용.
- 동시 요청을 위한 멀티 쓰레드 처리 지원.
