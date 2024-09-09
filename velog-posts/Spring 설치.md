<p><img alt="" src="https://velog.velcdn.com/images/baenna/post/ca40a57e-c814-40f4-b2de-59bc8a9b8d54/image.png" /></p>
<h3 id="1-스프링-사이트에-접속">1. <strong><a href="https://api.velog.io/rss/spring.io">스프링</a></strong> 사이트에 접속</h3>
<pre><code>상단 메뉴 중 ** Project &gt; Spring Tools 4** 클릭</code></pre><p>   <img alt="" src="https://velog.velcdn.com/images/baenna/post/cc0efdfb-09d4-4746-bf8d-c7a9cba175a4/image.png" /></p>
<h3 id="2-페이지를-아래로-스크롤하여-3-버전-다운로드-페이지로-이동">2. 페이지를 아래로 스크롤하여 3 버전 다운로드 페이지로 이동</h3>
<pre><code>Spring Tool Suite 3 wiki 클릭 </code></pre><p>   <img alt="" src="https://velog.velcdn.com/images/baenna/post/4bf9741c-aef6-4770-939d-b456cc187d6a/image.png" /></p>
<h3 id="3-spring-tool-suite-3917-버전-다운로드">3. Spring Tool Suite 3.9.17 버전 다운로드</h3>
<pre><code>자신의 운영체제에 맞는 STS 다운로드
필자는 &quot;spring-tool-suite-3.9.17.RELEASE-e4.20.0-win32-x86_64&quot; 파일 다운로드
    * 압축 해제할 때, 알집은 파일 이름이 잘려서 압축이 완전히 안 될 수 있으므로 다른 프로그램으로 압축풀기! (ex. 반디집)

&quot;sts-3.9.17.RELEASE&quot;폴더는 STS 플러그인을 포함하고 있는 이클립스이다. 
따라서 해당 폴더를 워크스페이스가 있는 폴더로 복사-붙여넣기</code></pre><h3 id="4-이클립스-설정-파일-수정">4. 이클립스 설정 파일 수정</h3>
<pre><code>STS가 포함된 이클립스를 설치했다면, 이제 이클립스 설정 파일을 수정해야 한다.
이클립스 설정 파일 : &quot;sts-3.9.17.RELEASE&quot; &gt; 'STS.ini'
위 파일을 메모장으로 열어 표시한 부분을 추가하여 저장!</code></pre><p>   <img alt="" src="https://velog.velcdn.com/images/baenna/post/ff21a131-bfae-4358-8f9f-e1f265e83318/image.png" /></p>
<h3 id="5-dsts-3917releasestsexe-실행">5. D:\sts-3.9.17.RELEASE\STS.exe 실행</h3>
<pre><code>이클립스 구동시, 이클립스에서 생성한 파일들이 물리적으로 저장될 워크스페이스 폴더를 지정하여 &lt;Launch&gt; 한다. </code></pre><p>   <img alt="" src="https://velog.velcdn.com/images/baenna/post/81a01794-4e84-4da5-bf5c-4a68a008fe40/image.png" /></p>
<p><em>** 정상 구동시 보여지는 화면</em>
<img alt="" src="https://velog.velcdn.com/images/baenna/post/19435c30-e2f1-4f5b-9e63-7f6a6dbf66e5/image.png" /></p>
<h3 id="6-file--new--spring-legacy-project-실행">6. File &gt; New &gt; Spring Legacy Project 실행</h3>
<p><img alt="업로드중.." src="blob:https://velog.io/f4d15899-4165-4919-b526-dabe1f164dec" />
    MVC Project를 사용하기 위해  &quot;https-content.xml&quot; 파일을 인터넷에서 검색하여 다운로드 -&gt; 워크스페이스 폴더의 .metadata.plugins\org.springsource.ide.eclipse.commons.content.core 에 밑에 파일 넣고 프로그램을 재실행한다. 여기서 반드시 처음에 Spring Legacy Project를 실행했어야 &quot;org.springsource.ide.eclipse.commons.content.core&quot; 폴더가 생성되니 참고!          </p>