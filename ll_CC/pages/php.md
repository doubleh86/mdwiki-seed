# PHP

## PHP 7.x 에 phpRedis 3.1.4 설치하기 ( CentOS )
 
 1. sudo yum --enablerepo=remi-test install php-pecl-igbinary 설치
 2. sudo yum --enablerepo=remi-test install php71-php-pecl-redis 설치
 3. 설치 완료 후 redis.so, igbinary.so 파일을 찾아 php가 로드하는 Module 디렉토리에 복사한다.
    ex ) $ sudo cp /opt/remi/php71/root/usr/lib64/php/modules/redis.so /usr/lib64/php/modules/redis.so
    	 $ sudo cp /opt/remi/php71/root/usr/lib64/php/modules/igbinary.so /usr/lib64/php/modules/igbinary.so

 4. php.ini 파일에 redis.so와 igbinary.so 모듈을 추가한다. 
 5. "$ php --ini" 명령어 실행
 6. "$ sudo service httpd restart" 명렁어로 웹서버 재실행

 -> yum --enablerepo=remi-php71 <= 여기로 변경되었습니다. 위와 같이 쓰지 마세요!

## php array 마지막 데이터 가져오기
```php
	$temp_array = ['1', '2', '3'];
	$last_data = end($temp_array);
```

## phpdocumentor 
 
 1. phpdocumentor.phar 파일 다운 ( composer로 할 시 디펜던시 에러가 남. twig 같은 놈들... )
 2. php phpdocumentor.phar ./src -t ./docs/api 명령어 실행

## php version update for centOS

```
	https://blog.asamaru.net/2018/02/14/install-php-7-2-on-centos-with-remi-rpm-repository/
```

## apidoc
 - http://apidocjs.com/

## laravel Eloquent using without laravel framework
 - composer.json add to 'composer require illuminate/database'
 - github : https://github.com/illuminate/database