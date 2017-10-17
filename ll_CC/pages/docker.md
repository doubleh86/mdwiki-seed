## Docker 설치 ( for mac )

해당 URL에서 docker.dmg 파일을 다운로드한 후 설치한다.

```
https://store.docker.com/editions/community/docker-ce-desktop-mac
```



## Docker 명령어

현재 실행 중인 container 찾기
```
docker ps -a
```

이미 실행되어 있는 container에 접속.

```
root@~~# docker exec -it  container id /bin/bash
```
