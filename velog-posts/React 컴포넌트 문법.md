<blockquote>
<p><strong>컴포넌트(Component)</strong>는 복잡한 HTML 코드를 깔끔하게 줄여주는 문법이다. 이를 사용하면 함수처럼 코드를 관리하고, 어디에서든 재사용할 수 있다.</p>
</blockquote>
<h3 id="1-html-및-css-레이아웃-디자인">1. HTML 및 CSS 레이아웃 디자인</h3>
<p>우선 모달 윈도우와 상세 페이지의 기본 HTML 및 CSS 코드를 작성한다. CSS는 별도의 파일에 저장하고, HTML 코드는 컴포넌트로 구성할 예정이다.</p>
<pre><code>&lt;div className=&quot;modal&quot;&gt;
  &lt;h4&gt;제목&lt;/h4&gt;
  &lt;p&gt;날짜&lt;/p&gt;
  &lt;p&gt;상세 내용&lt;/p&gt;
&lt;/div&gt;</code></pre><pre><code>.modal {
  margin-top: 20px;
  padding: 20px;
  background: #eee;
  text-align: left;
}</code></pre><h3 id="2-jsx-문법-이해하기">2. JSX 문법 이해하기</h3>
<blockquote>
<p>React에서 컴포넌트를 만들 때, return() 내부에 여러 개의 HTML 태그를 <strong>병렬로 작성할 수 없다</strong>. 이를 해결하기 위해 div로 감싸주거나, 이런 의미 없는 div 사용을 피하고 싶을 때는 <strong>Fragment(&lt;&gt; &lt;/&gt;) 문법</strong>을 사용한다.</p>
</blockquote>
<pre><code>return (
  &lt;div&gt;
    &lt;div&gt;&lt;/div&gt;
    &lt;div&gt;&lt;/div&gt;
  &lt;/div&gt;
)</code></pre><p>또는</p>
<pre><code>return (
  &lt;&gt;
    &lt;div&gt;&lt;/div&gt;
    &lt;div&gt;&lt;/div&gt;
  &lt;/&gt;
)</code></pre><h3 id="3-컴포넌트-문법으로-모달-윈도우-구현하기">3. 컴포넌트 문법으로 모달 윈도우 구현하기</h3>
<p>이제 위에서 작성한 모달 윈도우를 컴포넌트로 만들어 보자. React에서는 컴포넌트 문법을 통해 HTML 코드를 한 단어로 줄일 수 있다.</p>
<pre><code>function App() {
  return (
    &lt;div&gt;
      &lt;h1&gt;게시물 상세 보기&lt;/h1&gt;
      &lt;Modal /&gt;
    &lt;/div&gt;
  );
}

function Modal() {
  return (
    &lt;div className=&quot;modal&quot;&gt;
      &lt;h4&gt;제목&lt;/h4&gt;
      &lt;p&gt;날짜&lt;/p&gt;
      &lt;p&gt;상세 내용&lt;/p&gt;
    &lt;/div&gt;
  );
}
export default App;</code></pre><p>이렇게 작성하면 을 사용하여 HTML 코드를 간결하게 나타낼 수 있다. 컴포넌트는 함수처럼 이름을 붙여 어디서든 재사용이 가능하다.</p>
<h3 id="4-컴포넌트를-만드는-방법">4. 컴포넌트를 만드는 방법</h3>
<p>컴포넌트는 보통 함수로 생성되며, HTML 코드를 return() 내부에 작성한다. 여러 태그를 반환할 때는 하나의 div로 감싸거나 Fragment를 사용해야 한다. 또한 컴포넌트 이름은 관례적으로 대문자로 시작한다.</p>
<pre><code>function Modal() {
  return (
    &lt;div className=&quot;modal&quot;&gt;
      &lt;h4&gt;제목&lt;/h4&gt;
      &lt;p&gt;날짜&lt;/p&gt;
      &lt;p&gt;상세 내용&lt;/p&gt;
    &lt;/div&gt;
  );
}</code></pre><p>혹은 화살표 함수로도 작성 가능하다:</p>
<pre><code>const Modal = () =&gt; {
  return (
    &lt;div className=&quot;modal&quot;&gt;
      &lt;h4&gt;제목&lt;/h4&gt;
      &lt;p&gt;날짜&lt;/p&gt;
      &lt;p&gt;상세 내용&lt;/p&gt;
    &lt;/div&gt;
  );
}</code></pre><h3 id="5-컴포넌트를-사용하는-기준">5. 컴포넌트를 사용하는 기준</h3>
<p>컴포넌트는 아래의 경우에 사용하는 것이 좋다:</p>
<ol>
<li>사이트에서 반복적으로 등장하는 HTML 코드</li>
<li>내용이 자주 변경될 가능성이 있는 HTML 부분</li>
<li>다른 페이지를 만들 때 그 페이지의 내용을 하나의 컴포넌트로 구성</li>
<li>팀원과 협업 시 페이지를 여러 컴포넌트로 나누어 작업 분배</li>
</ol>
<h3 id="6-props를-사용한-상태-전달">6. props를 사용한 상태 전달</h3>
<p>컴포넌트를 많이 만들다 보면 다른 함수에서 선언한 변수를 컴포넌트에서 사용하고 싶을 때가 있다. 이때는 props라는 문법을 사용해 상태를 전달할 수 있다.</p>
<pre><code>function App() {
  const postTitle = &quot;게시물 제목&quot;;

  return (
    &lt;div&gt;
      &lt;h1&gt;게시물 상세 보기&lt;/h1&gt;
      &lt;Modal title={postTitle} /&gt;
    &lt;/div&gt;
  );
}

function Modal(props) {
  return (
    &lt;div className=&quot;modal&quot;&gt;
      &lt;h4&gt;{props.title}&lt;/h4&gt;
      &lt;p&gt;날짜&lt;/p&gt;
      &lt;p&gt;상세 내용&lt;/p&gt;
    &lt;/div&gt;
  );
}</code></pre><p>이런 방식으로 props를 통해 부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달할 수 있다.</p>
<h2 id="결론">결론</h2>
<p>이번 글에서는 React에서 컴포넌트를 사용하여 모달 윈도우와 상세 페이지를 구현하는 방법을 알아보았다. 컴포넌트를 사용하면 코드가 깔끔해지고, 재사용성이 높아지며 유지보수가 쉬워진다. 앞으로는 컴포넌트를 적절히 활용하여 효율적인 코드를 작성해 보자!</p>