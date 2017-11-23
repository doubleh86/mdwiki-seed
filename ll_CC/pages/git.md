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

## Git 삭제한 커밋 복구
	
	1. SHA 값 알아내기
		
```
		$ git reflog
			dc09d00 HEAD@{16}: commit: gitignore add
			7cc46ad HEAD@{17}: reset: moving to 7cc46ad381602e859079be4cc821a114b2e4a7be
``` 
	2. 좀 더 자세한 내용을 원하면 아래 명령어를 실행한다.
		
```
		$ git log -g

			commit dc86971db3c0b125f97adc3e4f85faeb049cbf00 (master)
			Reflog: HEAD@{1} (허현 <doubleh86@gmail.com>)
			Reflog message: reset: moving to HEAD
			Author: 허현 <doubleh86@gmail.com>
			Date:   Thu Nov 23 18:58:29 2017 +0900

			    camera 수정 전 코드

			commit dc86971db3c0b125f97adc3e4f85faeb049cbf00 (master)
			Reflog: HEAD@{2} (허현 <doubleh86@gmail.com>)
			Reflog message: reset: moving to HEAD
			Author: 허현 <doubleh86@gmail.com>
			Date:   Thu Nov 23 18:58:29 2017 +0900

```
	3. 복구할 커밋을 가르키는 복구 브랜치를 만들어 복구 한다.
		
```
			$ git branch recover-branch dc86971db3c0b125f97adc3e4f85faeb049cbf00

			$ git log --pretty=online recover-branch

				d9b4fdd49dc4ff327a22e938cfc9f9cf5a745aba (HEAD -> recover-branch) meta add
				dc86971db3c0b125f97adc3e4f85faeb049cbf00 (master) camera 수정 전 코드
				c54547242e5f107fd792dd94dced99781165c398 scene 변경

```
## 참고 사이트
https://stackoverflow.com/questions/19973506/cannot-ignore-idea-workspace-xml-keeps-popping-up
https://git-scm.com/book/ko/v1/Git%EC%9D%98-%EB%82%B4%EB%B6%80-%EC%9A%B4%EC%98%81-%EB%B0%8F-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EB%B3%B5%EA%B5%AC