<h2 id="react에서-배열과-객체-state-관리하기">React에서 배열과 객체 State 관리하기</h2>
<blockquote>
<p>React 개발을 하다 보면 배열이나 객체 형태의 state를 다루는 경우가 많다. 이런 복잡한 데이터 구조의 state를 수정할 때는 주의해야 할 점들이 있다. 이 글에서는 배열 state를 수정하는 과정을 통해 올바른 state 관리 방법과 그 이면의 JavaScript 동작 원리에 대해 알아보자.</p>
</blockquote>
<h3 id="기본적인-배열-state-수정">기본적인 배열 State 수정</h3>
<p>먼저, 간단한 예제로 보자. 글 제목 목록을 state로 관리하고, 버튼을 클릭하면 첫 번째 글의 제목을 수정하는 기능을 구현해보자.</p>
<pre><code>function App() {
  let [글제목, 글제목변경] = useState(['남자코트 추천', '강남 우동맛집', '파이썬 독학']);
  return (
    &lt;button onClick={() =&gt; {
      글제목변경(['여자코트 추천', '강남 우동맛집', '파이썬 독학'])
    }}&gt;
      수정버튼
    &lt;/button&gt;
  )
}</code></pre><p>이 방식은 작동하지만, 글 목록이 많아질수록 코드가 길어지고 관리가 어려워진다. 그래서 우리는 더 효율적인 방법을 찾아야 한다.</p>
<h3 id="배열의-특정-요소만-수정하기">배열의 특정 요소만 수정하기</h3>
<p>다음 단계로, 배열의 특정 요소만 수정하는 방법을 살펴보자.</p>
<pre><code>function App() {
  let [글제목, 글제목변경] = useState(['남자코트 추천', '강남 우동맛집', '파이썬 독학']);

  return (
    &lt;button onClick={() =&gt; {
      let copy = 글제목;
      copy[0] = '여자코트 추천';
      글제목변경(copy);
    }}&gt;
      수정버튼
    &lt;/button&gt;
  )
}</code></pre><p>이 코드는 논리적으로는 맞아 보이지만, 실제로는 동작하지 않는다. 그 이유는 JavaScript의 배열과 객체가 참조 타입(reference type)이기 때문이다.</p>
<h4 id="javascript의-참조-타입-이해하기">JavaScript의 참조 타입 이해하기</h4>
<blockquote>
<p>  JavaScript에서 배열이나 객체를 생성하면, 해당 데이터는 메모리의 특정 위치에 저장되고, 변수에는 그 메모리 위치를 가리키는 참조(reference)가 저장된다.</p>
</blockquote>
<pre><code>  let data1 = [1, 2, 3];
  let data2 = data1; // data1의 참조를 복사

  data2[0] = 1000; // data2를 수정하면 data1도 변경됨
  console.log(data1); // [1000, 2, 3]
  console.log(data2); // [1000, 2, 3]
  console.log(data1 === data2); // true</code></pre><p>  이러한 특성 때문에, 단순히 배열을 복사하는 것으로는 새로운 배열을 만들지 못하고, 원본 배열의 참조만 복사하게 된다.</p>
<h3 id="올바른-배열-복사와-state-업데이트">올바른 배열 복사와 State 업데이트</h3>
<p>이제 올바르게 배열을 복사하고 state를 업데이트하는 방법을 알아보자.</p>
<pre><code>function App() {
  let [글제목, 글제목변경] = useState(['남자코트 추천', '강남 우동맛집', '파이썬 독학']);

  return (
    &lt;button onClick={() =&gt; {
      let copy = [...글제목]; // 스프레드 연산자를 사용해 새로운 배열 생성
      copy[0] = '여자코트 추천';
      글제목변경(copy);
    }}&gt;
      수정버튼
    &lt;/button&gt;
  )
}</code></pre><p>여기서 사용된 [...글제목]은 스프레드 연산자를 이용해 기존 배열의 모든 요소를 새 배열에 복사한다. 이렇게 하면 원본 배열과는 다른 새로운 배열이 생성되어, 참조가 다르게 된다.</p>
<h3 id="state-업데이트의-동작-원리">State 업데이트의 동작 원리</h3>
<p>React의 state 업데이트 함수(여기서는 글제목변경)는 내부적으로 다음과 같은 과정을 거친다:</p>
<ol>
<li>새로 전달받은 state 값과 기존 state 값을 비교 (=== 연산자 사용)</li>
<li>두 값이 다르다고 판단되면 컴포넌트를 리렌더링</li>
<li>같다고 판단되면 리렌더링을 하지 않음</li>
</ol>
<p>따라서 배열이나 객체 state를 업데이트할 때는 항상 새로운 참조를 가진 데이터를 생성해야 React가 변경을 감지하고 리렌더링을 수행할 수 있다.</p>
<h2 id="결론">결론</h2>
<p>React에서 배열이나 객체 형태의 state를 다룰 때는 다음 사항들을 기억해야 한다:</p>
<ul>
<li>항상 원본 데이터를 직접 수정하지 말고, 복사본을 만들어 수정한다.</li>
<li>배열을 복사할 때는 스프레드 연산자([...arr])나 Array.from(), slice() 등의 메서드를 사용한다.</li>
<li>객체를 복사할 때는 스프레드 연산자({...obj})나 Object.assign() 메서드를 사용한다.</li>
<li>복잡한 중첩 구조의 경우, 깊은 복사(deep copy)가 필요할 수 있다.</li>
</ul>
<p>이러한 방식으로 state를 관리하면 예상치 못한 버그를 방지하고, React의 성능 최적화 기능을 제대로 활용할 수 있다.</p>