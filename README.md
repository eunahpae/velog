# Velog to Github : 자동 커밋

밸로그에 글 작성시, 깃헙에 자동으로 커밋되도록 설정할 수 있다. 

### 1. Github 에 새 레포지토리 생성
	- public 으로 생성 후 다음과 같이 디렉토리를 구성한다.
    
    ```
    생성한 레포지토리/
    ├── .github/
    │   └── workflows/
    │       └── update_blog.yml
    ├── scripts/
    │   └── update_blog.py
    └── ...
    ```
    
### 2.Github Action 작성
- .github/workflows/update_blog.yml : 아래 코드는 매일 지정한 시각 또는 해당 레포지토리가 push 될 때 파이썬 스크립트(update_blog.py)를 실행하는 코드이다.
    
	```
    name: Update Blog Posts


    on:
      push:
          branches:
            - main  # 또는 워크플로우를 트리거하고 싶은 브랜치 이름
      schedule:
        - cron: '0 0 * * *'  # 매일 자정에 실행 (분 / 시 로 원하는 시간 지정 가능)

    jobs:
      update_blog:
        runs-on: ubuntu-latest

        steps:
        - name: Checkout
          uses: actions/checkout@v2

        - name: Push changes
          run: |
            git config --global user.name 'github-actions[bot]'
            git config --global user.email 'github-actions[bot]@users.noreply.github.com'
            git push https://${{ secrets.GH_PAT }}@github.com/깃헙아이디/레포지토리.git

        - name: Set up Python
          uses: actions/setup-python@v2
          with:
            python-version: '3.x'

        - name: Install dependencies
          run: |
            pip install feedparser gitpython

        - name: Run script
          run: python scripts/update_blog.py

    ```
    
### 3. Python 스크립트 작성
- scripts/update_blog.py

	```
      import feedparser
      import git
      import os

      # 벨로그 RSS 피드 URL
      rss_url = 'https://api.velog.io/rss/@[벨로그 아이디]'

      # 깃허브 레포지토리 경로
      repo_path = '.'

      # 'velog-posts' 폴더 경로
      posts_dir = os.path.join(repo_path, 'velog-posts')

      # 'velog-posts' 폴더가 없다면 생성
      if not os.path.exists(posts_dir):
          os.makedirs(posts_dir)

      # 레포지토리 로드
      repo = git.Repo(repo_path)

      # RSS 피드 파싱
      feed = feedparser.parse(rss_url)

      # 각 글을 파일로 저장하고 커밋
      for entry in feed.entries:
          # 파일 이름에서 유효하지 않은 문자 제거 또는 대체
          file_name = entry.title
          file_name = file_name.replace('/', '-')  # 슬래시를 대시로 대체
          file_name = file_name.replace('\\', '-')  # 백슬래시를 대시로 대체
          # 필요에 따라 추가 문자 대체
          file_name += '.md'
          file_path = os.path.join(posts_dir, file_name)

          # 파일이 이미 존재하지 않으면 생성
          if not os.path.exists(file_path):
              with open(file_path, 'w', encoding='utf-8') as file:
                  file.write(entry.description)  # 글 내용을 파일에 작성

              # 깃허브 커밋
              repo.git.add(file_path)
              repo.git.commit('-m', f'Add post: {entry.title}')

      # 변경 사항을 깃허브에 푸시
      repo.git.push()
    ```
    
### 4. PAT 권한 받기
	1. github 계정 - Settings - Developer Settings - Personal access tokens (classic) - Generate New Token(classic) - 이름 쓰고 repo, workflow 클릭 - Generate new token
	2. 받은 토큰 복사 (발급시 한번만 확인가능하기 때문에 복사 필수!!!!)
	3. 위에서 생성한 레포지토리 - Settings - Security - Secrets and variables - Actions - New Repository Secret
	4. Name : GH_PAT, Secret : [2번에서 발급받은 토큰]
    
### 5. Test
- Velog 에 글을 작성하고, 지정시간에 확인시 velog-posts 폴더에 자동으로 .md 파일로 저장되는 것을 확인한다!