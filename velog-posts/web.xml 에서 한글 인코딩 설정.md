<p>스프링은 우리나라에서만 사용하는 프레임워크가 아니고, web.xml 파일에 등록된 DispatcherServlet 클래스는 우리가 만들지 않았기 때문에 한글 인코딩 처리를 해주어야 한다. 
스프링에서는 인코딩 처리를 위해 CharacterEncodingFilter 클래스를 제공하며, web.xml에 CharacterEncodingFilter를 등록하면 모든 클라이언트의 요청에 대해서 일괄적으로 인코딩 처리를 할 수 있다. </p>
<h4 id="web-app-태그-내부에-아래와-같이-설정한다">web-app 태그 내부에 아래와 같이 설정한다.</h4>
<pre><code>&lt;web-app&gt;

&lt;!-- 한글 인코딩 Strat --&gt;
&lt;filter&gt;
    &lt;filter-name&gt;encodingFilter&lt;/filter-name&gt;
    &lt;filter-class&gt;
        org.springframework.web.filter.CharacterEncodingFilter
    &lt;/filter-class&gt;
    &lt;init-param&gt;
        &lt;param-name&gt;encoding&lt;/param-name&gt;
        &lt;param-value&gt;UTF-8&lt;/param-value&gt;
    &lt;/init-param&gt;
    &lt;init-param&gt;
        &lt;param-name&gt;forceEncoding&lt;/param-name&gt;
        &lt;param-value&gt;true&lt;/param-value&gt;
    &lt;/init-param&gt;
&lt;/filter&gt;
&lt;filter-mapping&gt;
    &lt;filter-name&gt;encodingFilter&lt;/filter-name&gt;
    &lt;url-pattern&gt;/*&lt;/url-pattern&gt;
&lt;/filter-mapping&gt;
&lt;!-- 한글 인코딩 End --&gt;

&lt;/web-app&gt; </code></pre>