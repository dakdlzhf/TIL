# Gid & GitHub 특강
## 리눅스 잘사용하는 명령어 정리

`- ` pwd
* 현재경로 확인하기

`-` ls 

* 현재 경로에 파일과 폴더 보기

`-` ls -a
* 숨겨진 자료 모두 보기

`-` touch

* 파일만들기

`-` mkdir
* 폴더만들기

`-` cd
* 위치 이동


​	

## Git bash 폴더 파일 만들기
`1.` mkdir 폴더명(폴더만들기)
`2.` cd 폴더명 (폴더경로로 이동하기)
`3.` touch a.txt (파일만들기)
`4.` pwd (현재 경로 확인하고)
`5.` code . (Vs code 로 실행하기)

## Git 기본사용방법
```bash
$ git init
$ git add .
$ git commit -m "메시지"
$ git remote add origin git저장소주소.git
$ git remote -v (주소연결확인해보고 정상이라면)
$ git push origin master
```

## Git Clone ,Pull
1. Clone 
   * git clone 주소 (git init 이되있는 폴더 자체를 복제해 온다)
2. Pull
   * git pull origin (branch명) 보통 master branch 내용을 가지고온다.
## Git Branch (switch,checkout,merge)
1. 브랜치 생성
   1. git branch (생성할branch명)
   2. git branch (현재 어느브랜치위치인지 확인 해보기)
   3. git switch (이동할브랜치명) == git checkout (이동할브랜치명)
