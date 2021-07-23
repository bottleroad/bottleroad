<br/>

# Repositoty 초기화

>초기화하지 않고 저장소를 생성할 때의 커맨드라인 안내 메시지도 main으로 초기화하도록 변경되었다.   
이전에는 git이 알아서 기본으로 master를 기본으로 사용하였지만 main은 그렇지 않기 때문에   
명시적으로 git branch -M main으로 브랜치를 생성하는 명령어가 추가되었다.

```
echo "# example-repo" >> README.md   
git init   
git add README.md   
git commit -m "first commit"   
git branch -M main   
git remote add origin git@github.com:bottleroad/Helloworld.git   
git push -u origin main   
```
<br/><br/>

# 최초 설정

1. git 계정명 등록   
   ``` 
   git config --global user.name 계정명 
   ```   
   
2. git 이메일 등록   
   ``` 
   git config --global user.email 이메일
   ```
   
3. git 설정정보 조회   
   ``` 
   git config --list
   ```
   
4. git editor 변경   
   ```
   git config --global core.editor 에디터
   ```
	- vi로 변경 > git config --global core.editor vi   
  	- vscode로 변경 > git config --global core.editor "code --wait"	
	> **p.s.) vscode를 설치했을 경우 code . 명령어로 vscode 실행 가능**

5. git config에 설정한 editor로 config 파일 열기   
   ``` 
   git config --global -e
   ```   
	> **p.s.) vscode를 diff tool OR merge tool로 이용하고 싶을 경우 config에 추가**

6. 명령어 alias 등록   
   ``` 
   git config --global alias.줄일명령어 원본명령어
   ```   
	> **e.g.) git config --global alias.sts status == git sts**	

<br/><br/>

# 기본

1. 현재 디렉토리를 git local repository[Working Directory]로 지정(생성)   
   ``` 
   git init
   ```
	> ls -al 명령어로 .git 숨김파일 생성 확인   
	> rm -rf .git 명령어로 local repository 삭제
	  
2. 파일 상태 확인(staged, untracked, ..)   
   ```
   git status
   ```
   
3. 해당 파일을 [Staging Area]로 이동(tracking)   
   ``` 
   git add 파일명
   ```
   
4. 현재 폴더의 전체 파일을 이동   
   ``` 
   git add .
   ```
   
5. [Staging Area]에 있는 파일을 원격저장소[Repository]로 커밋   
   ``` 
   git commit
   ```
	> 옵션없이 해당 명령어만 입력할 경우 editor 호출
	  
1. editor 호출없이 바로 커밋   
   ``` 
   git commit -m "커밋메세지"   
   git commit -am "커밋메세지"
   ```	
	> [Staging Area]에 올림과 동시에 커밋(= git add .+ git commit -m "커밋메세지")   
	> 단, 1번이라도 커밋된 대상만 사용 가능
	
1. local repository[Working Directory]와 [Staging Area]의 차이를 보여줌
   ``` 
   git diff
   ```
   
1. commit 로그 확인   
   ``` 
   git log
   ```
 
<br/><br/>

# 브랜치

1. 브랜치 목록 조회(현재 속한 브랜치는 앞에 *가 붙음)
   - git branch
2. 브랜치명으로 브랜치 생성
   - git branch 브랜치명
		> 단, main 브랜치에 1번 이상 commit 해야함
1. 해당 브랜치로 local repository[Working Directory] 변경
   - git branch checkout 브랜치명
1. 브랜치 생성 후 checkout(= git branch 브랜치명 + git branch checkout 브랜치명)
   - git branch -b 브랜치명
1. 브랜치명 브랜치 삭제
   - git branch -d 브랜치명
1. 현재 checkout된 브랜치로 브랜치명의 브랜치 합침
   - git branch merge 브랜치명

<br/><br/>

# 깃허브

1. git 원격저장소[Repository] 목록 확인
   - git remote
2. git 원격저장소 이름과 url 목록 확인
   - git remote -v
3. 저장소URL의 원격저장소를 저장소이름으로 추가
   - git remote add 저장소이름 저장소URL 
4. 저장소이름의 원격저장소 제거
   - git remote rm 저장소이름
5. 원격저장소[Repository]의 내용을 가져와서(fetch) local repository[Working Directory]에 합침(merge)
   - git pull
6. 원격저장소[Repository]에 local repository[Working Directory]의 commit 내용을 올림
   - git push
7. 로컬브랜치명의 commit 내용을 원격저장소로 올림
   - git push -u 원격저장소명 로컬브랜치명
		> -u 옵션을 사용할 경우 해당 원격저장소와 브랜치가 default로 지정되어 git push 명령어만 입력 가능
8. 원격저장소[Repository]의 내용을 local repository[Working Directory]로 가져옴
   - git fetch
		> git checkout 원격저장소명/로컬브랜치명 OR git checkout FETCH_HEAD =가져온 fetch 내용 확인
9. 저장소URL의 원격저장소를 복사하여 추가(remote add 명령 필요없음)
   - git clone 저장소URL
