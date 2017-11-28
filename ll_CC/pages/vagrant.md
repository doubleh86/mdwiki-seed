# Vagrant 

## Synced Folder Permission 주기

 - Vagrantfile 의 config에 아래 내용 추가

```
	config.vm.synced_folder ".", "/vagrant", owner:"vagrant", group:"vagrant", mount_options: ["dmode=777,fmode=664"]
```
  : 위와 같이 안해 줄 경우 Mac에서 Vagrant Synced Folder에 퍼미션이 없어서 파일 복사 등이 안될 경우가 있어서 mount option을 넣어 준다.
    ( vagrant는 default로 host pc의 VagrantFile의 위치 폴더를 shared folder( ==synced_folder )로 사용한다.)