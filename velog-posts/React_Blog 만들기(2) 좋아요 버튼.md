<pre><code>** 변수를 만들고 사용하지 않는 등 문법적인 warning을 제거해 주는 코드
   파일 상단에 작성

  /* eslint-disable */</code></pre><h3 id="➢--좋아요-버튼-생성-→-클릭시-좋아요-수-증가-ui">➢  좋아요 버튼 생성 → 클릭시 좋아요 수 증가 UI</h3>
<ul>
<li><p>원하는 위치에 좋아요 아이콘 또는 버튼 생성</p>
<pre><code class="language-jsx">   &lt;div className=&quot;list&quot;&gt;
      &lt;h3&gt; {글제목[0]} &lt;span&gt;👍&lt;/span&gt; 0 &lt;/h3&gt;
      &lt;p&gt;11월 5일 발행&lt;/p&gt;
      &lt;hr/&gt;
   &lt;/div&gt;</code></pre>
</li>
<li><p>따봉 누를 떄마다 숫자가 증가하도록 설정</p>
<ul>
<li><p>이벤트 리스너(핸들러) 문법</p>
<pre><code class="language-markdown">  **onClick = {클릭될 떄 실행할 함수}
  onClick = { ( ) ⇒ {실행할 내용} }**

  ** onClick 속성을 사용하여 안의 공식을 실행해줌
     속성은 {} 중괄호를 사용해야하고, 바로 공식이 들어갈 수는 없음.
     반드시 함수가 들어가야함. function이라는 키워드 대신에 ES6부터는 **()=&gt;{ }** 이렇게만 적어도 됨.</code></pre>
<ul>
<li><p>useState 를 활용하여 state로 만들기</p>
<pre><code class="language-jsx">let [따봉, 따봉변경] = useState(0);          </code></pre>
</li>
<li><p>state 변경방법 → 아래와 같이 작성해야 재렌더링이 스무스하게 진행됨</p>
<pre><code class="language-markdown">let [따봉, 따봉변경] = useState(0);
따봉이랑 같이 만들었던 따봉변경은 함수임 : **따봉변경()**</code></pre>
<pre><code class="language-jsx">&lt;div className=&quot;list&quot;&gt;
&lt;h3&gt; {글제목[0]} &lt;span onClick={ ()=&gt;{ **따봉변경**(따봉 + 1) } }&gt;👍&lt;/span&gt;{ 따봉 }&lt;/h3&gt;
   &lt;p&gt;11월 5일 발행&lt;/p&gt;
   &lt;hr/&gt;
&lt;/div&gt;</code></pre>
</li>
</ul>
</li>
</ul>
</li>
</ul>