# Git 

## Git Ignore 파일 생성해주는 Web Site

```
	https://www.gitignore.io/
```

## Git pycharm .idea ignore 안될 시

```
	mv .idea ../.idea_backup
	rm .idea # in case you forgot to close your IDE
	git rm -r .idea 
	git commit -m "Remove .idea from repo"
	mv ../.idea_backup .idea
```

https://stackoverflow.com/questions/19973506/cannot-ignore-idea-workspace-xml-keeps-popping-up