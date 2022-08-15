---
layout: post
title: "[Linux] Linux 명령어 모음"
date: 2022-08-15 15:12:09 +0600
categories: [Linux]
author: EuiSangYu
post_image: "/assets/images/blog-img1.jpg"
---

## 주로 사용하는 명령어

### pwd (print working directory)
현재 사용자가 위치하고 있는 경로를 출력해줌.

### ls (list)
현재 위치한 디렉토리에 있는 파일과 디렉토리 리스트를 보여줌

[옵션]
```bash
$ ls -l : 파일과 디렉토리에 대한 내용을 구체적으로 출력함
(권한 소유계정 그룹계정 파일크기[Byte] 생성날짜 파일이름)
(== **ll 과 동일**)
$ ls -a : 현재 디렉토리에서 숨김파일을 포함하여 출력함
$ ls -li: ls-l상태에서 inode번호를 함께 출력함
$ ll: ls-l과 동일함
$ ls -alrt: 정렬까지해서 상세하게 출력
```

### chmod (change Mode)
권한 변경
```bash
$ chomd 664 fileName (ex. chomd 664 note.txt)
$ chmod u+x fileName (ex. chomd u+x note.txt)
u(user), g(group), o(other)를 의미하며 +는 권한부여, -는 권한박탈
(ex. u+x => 유저에게 execute권한을 부여)
```

### mkdir (make Directory)
디렉토리를 생성함
```bash
$ mkdir dirName
```

### touch
빈 파일 생성
```bash
$ touch fileName
```

### rm (remove)
파일삭제 명령
```bash
$ rm fileName
$ rm -r dirName (-f 옵션이 없으면 directory는 지워지지 않음)
```

### cd (change Directory)
디렉토리를 이동함
```bash
$ cd path
```

### mv (move)
파일, 디렉토리를 이동시키거나 이름을 변경시키는 명령어
```bash
$ mv file1 file2 (이름변경)
$ mv file1 dir1 (file을 dir로 이동시킴)
$ mv dir1 dir2 (dir1을 dir2 하위로 이동)
```

### cp (copy)
파일, 디렉토리를 복사함
```bash
$ cp file1 copy_file
$ cp -r dir1 copy_dir (-r 옵션이 없으면 directory복사 안됨)
```

### ln (link)
링크파일을 생성함
```bash
$ ln -s source target (softlink, target은 source를 참조)
$ ln source target (hardlink, 같은 inode번호를 가진다.)
```

### cat
파일의 내용을 출력함
```bash
$ cat FileName (fileName의 내용을 출력)
$ cat FileName | more (내용이 많을경우 좀 더 편하게 볼 수 있음)
$ cat source > target
(출력의 방향을 파일로 변경함, source를 target으로 복사했다고 볼 수 있다. 조심해야 하는점은 만약 target으로 지정한 파일의 이름이 이미 존재하는 경우 그 파일에 source의 내용이 덮어씌워진다.)
$ cat source >> target (source의 내용이 target파일에 append됨)
```

### head
파일의 맨 앞에서 몇 라인만을 출력함
```bash
$ head fileName
```
option으로 Line수를 지정할 수 있다.

### tail
파일의 맨 아래부분 몇 라인만을 출력함
```bash
$ tail fileName
$ tail -f fileName (파일의 마지막에 데이터가 추가되는 즉시 파일의 내용을 출력해줌, 개발 시 로그파일을 볼 때 많이 사용한다.
```

### grep
검색하고자 하는 문자를 옵션으로 주면 해당 문자열과 일치하는 파일을 찾아준다.
```bash
$ grep 문자열 파일이름 (ex. grep test *.log)
$ grep -H 문자열 파일이름 (어떤 파일인지를 함께 출력해줌)
$ grep -w 문자열 파일이름 (입력한 문자열과 정확히 일치하는 파일만을 출력)
```

### less
파일을 열고 내용을 볼 수 있는 TextViewer기능을 가진다.<br>
목적도 용도가 vi와는 다르기 때문에 별도로 알아야 할 필요가 있다.<br>
1GB정도 되는 로그파일을 vi로 열게되면 1GB가 모두 메모리에 올라가고, 네트워트 트래픽 또한 1GB만큼 발생하게 된다. <br>
하지만 less명령어를 이용하여 열면 화면에 보이는만큼만 메모리에 올라간다. 즉, 용량이 큰 로그파일을 열때는 less명령어를 사용하는 것이 좋다.

## System 명령어

### tar
압축관련 명령어
```bash
tar cvfz target.tar.gz source1 source2
(source1, source2를 target으로 압축한다. 현재 디렉토리를 모두 압축하고 싶은경우에는 *를 사용한다.)

cvfz중 c가 create를 의미한다는 정도만 알아두어도 된다.

tar.gz는 tar(파일과 디렉토리를 한 묶음으로 만듬)라는 명령어를 이용하여 gzip으로 압축한다는 의미이다.

tar xvfz source.tar.gz

xvfz중 x는 extract를 의미하며 압축을 해제할 때 사용한다.

압축과 압축해제는 옵션까지 한 묶음으로 숙지하는것이 좋다.
```

### sudo
관리자 권한을 사용할 수 있는 명령어
root계정으로 접속하여 etc/sudoers(CentOS 7기준)파일에서 계정에 권한을 주어야 함.

```bash
$ sudo ~~
```

### chown (change Owner)
파일 또는 디렉토리의 소유자, 그룹명을 변경하는 명령어

소유권을 뺏을수도 있는것이기 때문에 관리자 권한이 필요하다. (sudo)

```bash
$ chown user: group(or user) target
```

### find
파일이나 디렉토리를 찾을 때 사용하는 명령어이다. 검색조건이 매우 다양함

find 경로 조건 target 
```bash
$ find / -name system.log
$ find / -name debug.log* //뒤에 * 을 붙이면 해당 이름이 포함된 전체를 조회
```

### which
명령어의 위치를 조회하는 명령어

which 찾을명령어 
```bash
$ which ls => /bin/ls
```

### top
운영중인 서버의 CPU, Memory등의 상태를 확인하는 명령어<br>
상단에는 CPU사용률과 메모리 사용률을 표시한다.<br>
하단에는 프로세스 별 CPU사용률과 메모리 사용률을 표시한다.<br>
갱신하는 주기는 default 3초이다.<br>
매 초마다 갱신하고 싶다면 화면에서 d를 누르고 1을 입력하거나 top명령어를 실행할 때 top -d 1처럼 옵션을 입력하여 실행해도 된다.<br>
실행화면에서 h를 누르면 사용할 수 있는 명령어가 나온다.

### w
현재 리눅스 장비에 접속한 사용자가 누구인지 조회하는 명령어<br>
사용자 아이디, 접속한 시간, IP, CPU사용률, 어떤 작업을 수행중인지 출력한다.<br>
간단하게 보고싶으면 who명령어를 사용하면 된다.

### ping
네트워크 설정이 잘 되어 있는지 알아보는 경우에 많이 사용함
```bash
$ ping domain(or IP) (ex. ping google.com)
```

### nslookup !!
domain을 이용하여 IP를 알아낼 때 사용하는 명령어
```bash
$ nslookup domain
```

### ps (process status)
현재 구동중인 모든 프로세스 정보를 조회할 때 사용하는 명령어<br>
너무많은 정보를 보여주기 때문에 주로 옵션과 함께 사용한다.<br>
```bash
$ ps -ef |grep apache (프로세스 중 apache가 들어간 것을 조회)
```

PID는 각 프로세스마다 할당되는 유니크한 번호이다.<br>
PID오른쪽에는 해당 프로세스의 부모 프로세스 PID를 나타낸다.

### kill
프로세스를 종료하는 경우 사용하는 명령어<br>
PID를 이용하여 종료시킨다.<br>
kill은 관리자 권한이 필요하다.
```bash
$ kill -9 PID (-9옵션을 주면 강제종료 한다.)
```

### df
파일 시스템 디스크 사용량을 조회하는 명령어

![](https://velog.velcdn.com/images/clothes/post/dda55e95-6772-4ea8-90d1-1c6a7f5a91c9/image.png)

#### 옵션들
![](https://velog.velcdn.com/images/clothes/post/dd907507-1312-4c28-99fd-283495dc8441/image.png)

일반적으로 **df -h** 가 가장 많이 사용된다.
```bash
$ df -h
```

### du
df 명령어가 시스템 전체의 디스크 공간을 확인하는 명령어라면, du 명령은 특정 디렉토리를 기준으로 디스크 사용량을 확인할 수 있다.

![](https://velog.velcdn.com/images/clothes/post/afcfaca7-73ad-470b-8bc0-7ac48c43e9c0/image.png)

디렉토리 안에 있는 서브 디렉토리의 디스크 사용량도 표시함.
```bash
$ du -h
```

### man
명령어에 대한 메뉴얼을 제공

man 3 sleep처럼 3을 옵션으로 주면 프로그래밍에 대한 메뉴얼도 제공받을 수 있다.

### adduser
새로운 사용자를 추가하는 경우에 사용하는 명령어

관리자 권한이 필요한 명령어
```bash
$ adduser 사용자ID
```

### su
사용자를 변경할 때 사용하는 명령어
```bash
$ su - (root계정 접속)
$ su -l userID (해당 userID로 접속)
```

### deluser
사용자를 삭제하는 경우에 사용하는 명령어

관리자 권한이 필요한 명령어
```bash
$ deluser 사용자ID
```

## 권한
**ls -l**을 이용하여 디렉토리 정보를 출력하면 맨 앞쪽에 **drwxrwxrwx**처럼 권한에 대한 내용이 출력된다.<br>
가장 먼저 나오는 알파벳은 파일의 유형을 의미하며 d, l, -로 나뉘고 각각 directory, link, file을 의미한다.<br>
권한정보인 rwx는 각각 read write execute를 의미한다.<br>
예를들어 --x권한을 가지고 있다면 읽거나 쓰지는 못하고 실행만 할 수 있다.<br>
권한정보는 rwx(User 권한) rwx(Group 권한) rwx(Other 권한)처럼 3자리씩 끊어서 하나의 세트로 볼 수 있다.<br>
또한 rwx를 숫자로 표현하면 421로 표현할 수 있다 (이진수 표기법)

## 경로
/   : 절대위치 기준 경로 (root가 시작점)<br>
./  : 현재위치 기준 경로 (현재 디렉토리가 시작점, 생략가능)<br>
../ : 현재 위치의 상위 기준 (root/home 이라면 ../는 root임)<br>
~/  : Home 위치 기준