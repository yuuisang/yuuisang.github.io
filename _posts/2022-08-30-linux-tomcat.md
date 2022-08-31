---
layout: post
title: "[Linux] Tomcat 서버 시작/종료/재시작"
date: 2022-08-30 22:00:00 +0600
categories: [Linux]
author: EuiSangYu
post_image: "/assets/images/linux/linuxTomcat.png"
---

최근 업무 시간 종료 후 서버에 변경사항을 배포할 일이 있었는데 실수로 명령어를 잘못입력해서 `Tomcat` 이 아닌 `리눅스` 자체를 종료시킨적이 있었다. 서버관리팀에 요청해서 금방 재부팅하고 마저 진행했지만 혹시나 이런 실수를 반복할 수 있으니 정리해둔다.

## 서버 시작
![image](https://user-images.githubusercontent.com/58925978/187592468-ea97a895-8a20-459e-a3f7-b78588376d5f.png)

```bash
$ ./startup.sh
$ ps -ef | grep tomcat 명령어로 톰캣이 제대로 가동되었는지 확인
```

![image](https://user-images.githubusercontent.com/58925978/187592111-31eb0b18-806b-4635-aee9-46e1ec847c30.png)

## Tomcat 서버 종료
![image](https://user-images.githubusercontent.com/58925978/187591967-6902481e-7282-4d0e-9672-45c9317427b0.png)

여기서 만약 `./shutdown.sh` 가 동작하지 않는다면 `tomcat.pid` 파일의 `pid` 값이 현재 돌아가는 톰캣 프로세스와 일치하지 않아서 그럴 확률이 있으니 확인해볼 것.

![image](https://user-images.githubusercontent.com/58925978/187592195-447f6a5e-e836-48c9-ba22-ea1afd94204a.png)

```bash
$ cd 톰캣까지의경로/apache-tomcat-9.0.22/bin
$ ./shutdown.sh
$ ps -ef | grep tomcat 명령어로 톰캣이 제대로 종료되었는지 확인
```

### tomcat.pid 파일 수정
![image](https://user-images.githubusercontent.com/58925978/187592237-eb69688d-9328-4b36-8863-d4220c5e322a.png)

tomcat.pid 파일을 vi 텍스트 모드로 열어서 직접 알맞게 수정 후 다시 서버 종료 시도

```bash
$ vi tomcat.pid
$ 값 수정
$ :wq 저장하고 텍스트모드 나가기
$ ./shutdown.sh 서버 종료
```

### 명령어 주의!
현재 디렉토리를 나타내는 `./` 를 입력하지 않고 그냥 `shutdown` 명령어만 입력하게 되면 톰캣 서버가 아닌 리눅스 서버 자체를 꺼버릴 수 있기 때문에 반드시 명령어 사용에 주의해야한다.


## 서버 재시작
![image](https://user-images.githubusercontent.com/58925978/187592468-ea97a895-8a20-459e-a3f7-b78588376d5f.png)

```bash
$ ./startup.sh
$ ps -ef | grep tomcat 명령어로 톰캣이 제대로 재가동되었는지 확인
```
