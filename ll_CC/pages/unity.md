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

아래와 같은 url을 호출하면 유저의 access_token 의 유효한지 확인 할 수 있다.

```
https://graph.facebook.com/debug_token?input_token=app-id|app_secret_id&access_token=user_access_token

```

## Google Sign-In 

plug-in download 

```
https://github.com/googlesamples/google-signin-unity
```

근데 Package는 어디 있는 것일까??

Back-end 인증의 경우 (php)
```
composer require google/apiclient
```

추가 후 

```
require_once 'vendor/autoload.php';

// Get $id_token via HTTPS POST.

$client = new Google_Client(['client_id' => $CLIENT_ID]);
$payload = $client->verifyIdToken($id_token);
if ($payload) {
  $userid = $payload['sub'];
  // If request specified a G Suite domain:
  //$domain = $payload['hd'];
} else {
  // Invalid ID token
}
```

end-point 사용 방법
 
 - https://www.googleapis.com/oauth2/v3/tokeninfo?id_token=XYZ123

해당 방법의 경우 client-id를 비교해야 한다. 

## 참고 사이트

https://stackoverflow.com/questions/5406859/facebook-access-token-server-side-validation-for-iphone-app
https://developers.google.com/identity/sign-in/android/backend-auth