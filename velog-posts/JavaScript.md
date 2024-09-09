<h1 id="자바스크립트란">자바스크립트란?</h1>
<blockquote>
<aside>
💡 [HTML](https://developer.mozilla.org/ko/docs/Glossary/HTML)은 문단, 제목, 데이터 표를 정의하거나 페이지에 이미지와 동영상을 삽입하는 등 웹 콘텐츠를 구성하고 의미를 부여하는 데 사용하는 마크업 언어

</aside>

<aside>
💡 [CSS](https://developer.mozilla.org/ko/docs/Glossary/CSS)는 배경색과 글꼴을 설정하고 콘텐츠를 여러 열에 배치하는 등 HTML 콘텐츠에 스타일을 적용하는 데 사용하는 스타일 규칙 언어

</aside>

<aside>
💡 [JavaScript](https://developer.mozilla.org/ko/docs/Glossary/JavaScript)는 동적으로 변경되는 콘텐츠를 만들고, 멀티미디어를 제어하고, 이미지에 애니메이션을 적용하는 등 거의 모든 작업을 수행할 수 있는 스크립팅 언어 (모든 것이 가능한 것은 아니지만 몇 줄의 JavaScript 코드로 달성할 수 있는 것은 놀라움)

</aside>

<p>[출처] <a href="https://developer.mozilla.org/">https://developer.mozilla.org/</a></p>
</blockquote>
<ul>
<li>웹 페이지에서 복잡한 기능을 구현할 수 있는 스크립팅 또는 프로그래밍 언어</li>
<li>자바스크릡트를 쓰는 이유 : 웹서버, 모바일앱, 머신러닝 등 다양한 곳에서 쓰인다.</li>
<li>원조는 웹개발할때 많이 쓰임 → HTML 조작과 변경<ul>
<li>탭, 모달 등 웹페이지 UI 만들 수 있음</li>
<li>유저가 입력한 데이터를 검사할 수도 있음</li>
<li>유저가 버튼누르면 서버로 데이터 요청할 수도 있음</li>
</ul>
</li>
</ul>
<h2 id="개발환경-셋팅">개발환경 셋팅</h2>
<ol>
<li><p>자바스크립트를 사용하려면 우선 에디터를 설치한다. </p>
<p> 나는 원래 쓰고 있던 VS Code 사용! (Brackets 등 다른 에디터도 가능)</p>
</li>
<li><p>작업을 진행할 폴더를 원하는 위치에 만들고, 에디터에서 해당 폴더를 열어준다.</p>
</li>
<li><p>에디터에서 새로운 파일 만들기를 클릭하여 index.html 파일을 생성한다.</p>
</li>
<li><p>작업내용을 실시간으로 보면서 확인하고 싶은 경우, VS Code 경우 왼쪽 Extensions 메뉴에서 live server 부가기능 찾아서 설치하고 html 화면에서 마우스 우클릭 - live server 띄우기 누른다.</p>
</li>
</ol>
<h3 id="html조작-변경">HTML조작, 변경</h3>
<pre><code class="language-jsx">&lt;h1 id=&quot;hello&quot;&gt;안녕하세요&lt;/h1&gt;

&lt;script&gt;
  document.getElementById('hello').innerHTML = '안녕';
&lt;/script&gt;</code></pre>
<ul>
<li><p>index.html 파일에서 원하는 내용을 입력, script 태그 안에 자바스크립트 코드를 적는다.</p>
</li>
<li><p>위 코드는 원래 ‘안녕하세요’라고 화면에 나오던 문구를 자바스크립트를 통해 ‘안녕’으로 변경해준 것.</p>
<ul>
<li><p>document.getElementById(' ??? ').???  = '???';</p>
<ul>
<li>기본 문법으로 외우기 /  물음표 자리에 원하는 것들을 채우면서 다양한 효과를 낼 수 있음</li>
<li><strong>.getElementById( )는 셀렉터, .innerHTML / .style / .color는 메소드(함수)라고 부른다.</strong></li>
</ul>
</li>
<li><p>이미지를 삽입하거나, 해당요소의 스타일을 변경할 수도 있음 (워낙 다양하기때문에 그때그때 구글링)</p>
<pre><code class="language-jsx">ex)
document.getElementById('???').src = 'profile.jpg';
document.getElementById('???').style.color = 'red';</code></pre>
</li>
</ul>
</li>
</ul>