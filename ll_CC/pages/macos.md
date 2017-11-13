# Mac OS X

## SSH Tunneling

아래와 같은 명령어로 터널링을 연다.

```
ssh -N -L (local port):(destination IP):(destination Port) -l tunnel_server_id tunnel_server_ip -p(Tunnel_server_connect_port)
```

로컬에서 터널서버를 통한 리모트 서버 접속 방법

```
ssh -l (remote_server_id) localhost -p(위 명령어에서 설정한 로컬 호스트 포트)
```