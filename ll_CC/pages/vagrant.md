# Vagrant 

## Synced Folder Permission 주기

```
	config.vm.synced_folder ".", "/vagrant", owner:"vagrant", group:"vagrant", mount_options: ["dmode=777,fmode=664"]
```