<h3 id="git-checkout--git-switch--모두-브랜치를-전환할-때-사용하는-명령어">git checkout / git switch : 모두 브랜치를 전환할 때 사용하는 명령어</h3>
<p>다만 둘의 차이는 git switch 는 Git 2.23버전에서 도입되어 git checkout 명령어의 일부 기능을 더 명확하게 하고, 사용하기 쉽게 만들기 위해 추가되었다는 점이다. 두 명령어의 주요 차이점은 사용 목적과 범위의 명확성에 있다. </p>
<p><strong>1. git checkout :</strong> 브랜치 전환, 파일 체크아웃, 커밋으로 돌아가기 등 다양한 용도로의 사용</p>
<pre><code>git checkout main                  # main 브랜치로 전환
git checkout -b newBranch          # 새 브랜치를 생성하고 그곳으로 전환
git checkout 3d1a123                 # HEAD를 특정 커밋으로 이동
git checkout -- file.txt             # 특정 파일을 마지막 커밋 상태로 복원</code></pre><p><strong>2. git switch :</strong> 오직 브랜치 전환에만 사용</p>
<pre><code>git switch main                   # main 브랜치로 전환
git switch -c newBranch            # 새 브랜치를 생성하고 그곳으로 전환</code></pre>