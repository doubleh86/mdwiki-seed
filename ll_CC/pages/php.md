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

