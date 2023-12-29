---
title: "docker Tip"
layout: post
date: 2023-11-29 09:47:00 +0900
category: Tip
---

1. docker 목록 확인
```
# 실행중인 docker 목록 확인
docker ps 

# 전체 docker 목록 확인
docker ps -a
```

-   CONTAINER ID
    컨테이너에게 자동으로 할당되는 고유한 ID
    출력은 고유 ID의 12자리만 나오지만, 전체 정보를 확인하기 위해서 docker inspect를 사용하면 전체 ID를 확인할 수 있다.

-   IMAGE
    컨테이너를 생성할 때 사용된 이미지 이름
    [이미지 이름]:[이미지 버전] 형식으로 출력됨
    
-   COMMAND
    컨테이너가 시작될 때 실행되는 명령어
    대부분 이미지에 미리 내장돼있어 별도로 설정할 필요는 없음
    이미지에 내장된 커맨드는 docker run이나 create 명령어의 맨 끝에 입력해서 컨테이너를 생성할 때 덮어쓸 수 있음

-   CREATED
    컨테이너가 실행되고 난 뒤 흐른 시간을 나타냄

-   STATUS
    컨테이너의 상태를 나타냄
    실행중이면 "Up", 종료된 상태면 "Exited", 일시 중지된 상태면 "Pause" 등을 나타냄

-   PORTS
    컨테이너가 개방한 포트와 호스트에 연결된 포트를 나열함
    컨테이너를 생성할 때 외부에 노출하도록 설정하지 않으면 ps에서 나타나지 않음

-   NAMES
    컨테이너의 고유한 이름
    --name 옵션으로 이름을 설정하지 않으면 도커 엔진이 임의로 형용사와 명사를 무작위로 조합해 이름을 설정함
    컨테이너의 이름은 중복될 수는 없지만 docker rename 명령어로 이름을 변경할 수 있음



2. Add a bind mount using Compose

- local에 있는 파일을 도커에 적용하기 위해서 
```python
todo-app:
    # ...
    volumes:
      - ./app:/usr/src/app
      - /usr/src/app/node_modules
```
처럼 volumes에 경로를 설정하고나서 docker를 다시 compose up 시켜주면 된다.