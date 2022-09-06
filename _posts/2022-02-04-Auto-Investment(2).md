---
title: "Slack을 이용해서 bot과 소통!"
layout: post
date: 2022-02-04 19:53:00 +0900
category: Auto Investment
---

## Slack

( bootcamp에서 slack으로 소통을 했기에 친근 ) slack에서 새로운 워크스페이스를 만들어서 자동투자를 수행한 bot의 진행 결과를 받아보기로 했다.

[slacker github 주소](https://github.com/os/slacker)에서 설명하는 코드를 이용하게 되면 인증에서 slacker.Error: invalid_auth 가 발생하게 된다.

- 그 이유는 2021년 2월 24일 이후로 새로 생성된 bot은 slacker 라이브러리를 이용할 수가 없기 때문이다.

- 그렇기에 해결 방안으로 requests 라이브러리를 이용해서 해결했다.

```py
import requests


def post_message(token, channel, text):
    response = requests.post("https://slack.com/api/chat.postMessage",
                             headers={"Authorization": "Bearer "+token},
                             data={"channel": channel, "text": text}
                             )
    print(response)


myToken = "<인증token>"

post_message(myToken, "#<채널명>", "Hi~")
```

위와 같이 코드를 실행하게 되면,

![image](https://user-images.githubusercontent.com/26592315/152376980-d3577ed4-98dc-4a6d-ada8-c765960cfd4c.png){: width="100%" height="100%"}{: .center}

slack으로 메세지가 오는 것을 확인할 수 있다.

코드를 실행하기 전,

1. slack에서 워크스페이스 만들기
2. [slack-api](https://api.slack.com/)에서 bot(app) 만들기 (1번에서 만든 워크스페이스 이용)
3. slack-api의 OAuth & Permissions 에서 chat:write 권한 부여하기

![image](https://user-images.githubusercontent.com/26592315/152378491-06982379-1f10-4b70-bc30-7d9fb33737eb.png){: width="100%" height="100%"}{: .center}

마지막으로 slack-api에서 install 해서 token 부여받기

- 그 이후에 token을 이용해서 위의 python 코드를 돌려보면, 메세지가 잘 간다.

- 앞으로 bot의 진행 결과를 slack에서 받아보도록 하겠다.
