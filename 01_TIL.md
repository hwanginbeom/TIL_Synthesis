# GIT

Source Code management(SCM) : 코드 관리 도구 (버전을 통해 관리)

Version Control System(VCS) : 버전 컨트롤 시스템



## 주요사항



### (1) git 폴더를 기준으로 프로젝트(code)를 관리한다.



### (2) git init

- 현재 폴더에서 코드 관리를 시작(init)한다.
- `.git` 폴더 생성 == git으로 폴더가 관리 되고 있다. ( 작업을 진행할 경우 master라는 것이 생긴다.)
- `.git` 폴더 삭제 == git 으로 폴더 관리를 중지 - `rm -rf  .git/`



![image-20200915150956945](C:\Users\hwang in beom\AppData\Roaming\Typora\typora-user-images\image-20200915150956945.png)





### (3) git status(**)

- 현재 상태(status) 출력

```shell
On branch master (master 브랜치에 있음)

No commits yet (아직 commit 없음)

nothing to commit (create/copy files and use "git add" to track)
(commit 할게 없음)
```

![image-20200915151059120](C:\Users\hwang in beom\AppData\Roaming\Typora\typora-user-images\image-20200915151059120.png)



- 새로운 파일 생성 후

```shell
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        a.txt

nothing added to commit but untracked files present (use "git add" to track)

```



![image-20200915151133693](C:\Users\hwang in beom\AppData\Roaming\Typora\typora-user-images\image-20200915151133693.png)



### (3) `git add [파일명]`

- 버전을 만들(commit할 파일에 대해 스냅샷을 찍어준다.)

- git add이후 statue

```shell
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        a.txt

nothing added to commit but untracked files present (use "git add" to track)

```

![](C:\Users\hwang in beom\AppData\Roaming\Typora\typora-user-images\image-20200915151410856.png)



### (4) `git commit -m "메시지"`  

- 버전을 만듬(commit, snapshot)
- message를 필수적으로 입력함



![image-20200915151354496](C:\Users\hwang in beom\AppData\Roaming\Typora\typora-user-images\image-20200915151354496.png)

### (5) `git log` 

- 현재 까지의 버전(스냅샷)

  ![image-20200915151300209](C:\Users\hwang in beom\AppData\Roaming\Typora\typora-user-images\image-20200915151300209.png)



## 반복작업

### (1) 기존 파일에 내용 추가

- a.txt 파일에 hello 라는 내용 추가
- git status 확인

```shell
$ git status
On branch master
Changes not staged for commit: (commit 하기 위해 변화들이 stage에 추가되지 않았다.)
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   a.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

![image-20200915151233426](C:\Users\hwang in beom\AppData\Roaming\Typora\typora-user-images\image-20200915151233426.png)

![image-20200915151505594](C:\Users\hwang in beom\AppData\Roaming\Typora\typora-user-images\image-20200915151505594.png)





![image-20200915151546971](C:\Users\hwang in beom\AppData\Roaming\Typora\typora-user-images\image-20200915151546971.png)



![image-20200915152032740](C:\Users\hwang in beom\AppData\Roaming\Typora\typora-user-images\image-20200915152032740.png)



![image-20200915152315196](C:\Users\hwang in beom\AppData\Roaming\Typora\typora-user-images\image-20200915152315196.png)



![image-20200915152403688](C:\Users\hwang in beom\AppData\Roaming\Typora\typora-user-images\image-20200915152403688.png)

저 위에 마스터 부분이 바뀐다.





----



## 원격 저장소



### (1) `git remote add [저장소의 이름] [저장소의 URL]`

- 저장소의 이름 :  `origin`
- git remote add origin ~

### (2) `git remote -v`

- 원격 저장소 정보 확인

### (3)  `git push origin master`

- origin 이라는 저장소에 master 브랜치를 업로드

### (4) `git remote remove [저장소 이름]`







### 실습2-http://bit.do/01_TIL

> 01_TIL.md 파일을 작성 후, add, commit, & push를 통해 github에 올리기



 origin 은 첫번째 저장을 할 때 관례적으로 사용하는 remote 이름이다.

