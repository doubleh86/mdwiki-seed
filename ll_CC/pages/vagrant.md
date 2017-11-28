# Vagrant 

## Synced Folder Permission 주기
 
 - Vagrantfile 의 config에 아래 내용 추가

```
	config.vm.synced_folder ".", "/vagrant", owner:"vagrant", group:"vagrant", mount_options: ["dmode=777,fmode=664"]
```
  : Mac에서 Vagrant Synced Folder에 퍼미션이 없어서 파일 복사 등이 안될 경우가 있어서 mount option을 넣어 준다.