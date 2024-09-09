<h1 id="blog-메인페이지-만들기-with-기본문법">Blog 메인페이지 만들기 (with 기본문법)</h1>
<p><strong>src &gt;</strong> <strong>App.js</strong> 파일에 코드 작성하기 / CSS는 상단에 import되어있는 App.css 파일을 열어서 코드 작성</p>
<pre><code class="language-jsx">function App() {
  return (
    &lt;div className=&quot;App&quot;&gt;            
            (/* react에서는 태그에 class를 주고싶으면 **JSX문법**을 사용해야함, class X, className O */}
      &lt;div className=&quot;black-nav&quot;&gt;
        &lt;div&gt;개발 Blog&lt;/div&gt;
      &lt;/div&gt;     
    &lt;/div &gt;
  );
}</code></pre>
<h2 id="reactjsx문법-사용의-가장-큰-장점">React(JSX문법 사용)의 가장 큰 장점</h2>
<ul>
<li>리액트에서 데이터바인딩을 쉽게 할 수 있음 (Angular, Vue 도 가능)</li>
<li>데이터바인딩 - 화면상에 보여지는 데이터(View)와 브라우저 메모리에 있는 데이터(Model)를 묶어서(Binding) 서로 간의 데이터를 동기화하는 것을 의미</li>
<li><strong>중괄호 { }</strong> 를 활용하여 안에 변수명, 함수 등 다양한 것들을 넣어서 사용가능</li>
</ul>
<h3 id="➢-데이터를-넣는-방법은-2가지가-있다">➢ 데이터를 넣는 방법은 2가지가 있다.</h3>
<ol>
<li><strong>변수에 넣기</strong></li>
</ol>
<pre><code class="language-jsx">{/* 중괄호 문법을 통해 원하는 것을 뭐든지 넣을 수 있음 */}

{/* 원하는 내용을 변수에 넣고, 원하는 곳으로 HTML에 꽂을 수 있음 */}
let posts = '서울시 노원구 공릉동';
&lt;h4&gt; { posts } &lt;/h4&gt;

{/* 함수도 만들어서 원하는 곳에 넣을 수 있음 */}
function 함수(){
     return 100
}
&lt;h4&gt; { 함수() } &lt;/h4&gt;

{/* style 적용 */}
{/* 1. style을 직접 줄 떄는 object형식으로 중괄호안에 중괄호로 { { 코드 } } 작성해야함 */}
&lt;div style={ { color : 'blue', fontSize : '30px' } }&gt;개발 Blog&lt;/div&gt;

{/* 2. 변수에 스타일을 넣고, 해당 변수명으로 적용시킬 수도 있음 */}
let posts = { color : 'blue', fontSize : '30px' }
&lt;div style = { posts } &gt;개발 Blog&lt;/div&gt;

{/* 이미지 삽입은 상단에 해당파일을 import하고 */} 
import logo from './logo.svg';
{/* 원하는 위치에 아래와 같이 작성 */}
&lt;img src = { logo } /&gt;</code></pre>
<ol start="2">
<li><strong>state에 넣기</strong><ul>
<li><strong>useState 를 사용하는 이유 :</strong><ul>
<li>state 는 내용이 변경되면 HTML이 자동으로 재렌더링이 됨 (새로고침 없이 스무스하게 변경됨)</li>
<li>자주 바뀌는, 중요한 데이터는 변수 말고 꼭 state 로 저장해서 쓸 것</li>
</ul>
</li>
</ul>
</li>
</ol>
<pre><code class="language-jsx">{/* useState 가져오기 */}
import React, { useState } from 'react';

let [글제목, 글제목변경] = useState('동네 맛집 추천');
let [글제목2, 글제목변경2] = useState('노원 맛집 추천');
let [글제목3, 글제목변경3] = useState('서울 맛집 추천','서울 우동 맛집');</code></pre>
<hr />