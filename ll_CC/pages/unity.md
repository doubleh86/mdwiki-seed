# Unity

## Unity Android 설치 (Mac OSX)
1. Unity 설치
2. Android SDK 설치 
  -> user/username/Library/Android/ ..
  -> Mac OS 버전에 따라 라이브러리 폴더가 안보일 수도 있다. username 폴더 선택 후 'CMD + J' 후에 라이브러리 폴더 보기를 체크
3. JDK 설치

## Unity Trouble Shooting
 - "Unable to merge android manifests. See the Console for more details." 해당 에러 발생 시 Manfest 파일 확인
 ```
 <manifest xmlns:android="http://schemas.android.com/apk/res/android"
          xmlns:tools="http://schemas.android.com/tools"  <- 해당 부분만 추가 해주면 된다.
          package="com.unity3d.player" 
          android:installLocation="preferExternal" 
          android:versionCode="1" 
          android:versionName="1.0">
 ```

 위 와 같이 변경한다.

 ## Facebook Access Token Verify

 https://developers.facebook.com/docs/accountkit/graphapi

