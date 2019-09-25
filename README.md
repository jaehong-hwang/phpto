# phpto

`phpto` 는 쉘에서 동작하는 PHP 멀티 버전 메니져입니다.  
MacOS 기준으로 동작하고, brew에 의존성을 지니고 있으며, PHP는 무조건 `php@${version}` 와 같은 패키지로만 설치가 필요합니다.  

## 동작 방식

``` bash
> phpto 5.2
```

`phpto`는 위와 같은 간단하고, 단순한 명령어로 동작합니다.  
  
만약 변경하고 싶은 PHP 버전이 현재 로컬에 설치되어있지 않은 경우  
설치 여부를 묻고, 원할경우 설치까지 자동으로 이루어집니다.  
  
또한 개인적으로 아파치와 연동하여 작업을 진행하고있는데, 아파치의 PHP 모듈 변경 및 재시작을 위한 스크립트도 작성되어있습니다.  

``` bash
echo "LoadModule php${after:0:1}_module /usr/local/opt/php@$after/lib/httpd/modules/libphp${after:0:1}.so" > /usr/local/etc/httpd/extra/httpd-php.conf

echo ""

echo "apache restart..."
sudo apachectl restart
echo "success!"
```

위 내용인데 이를 위해 `httpd.conf` 파일에 아래와 같은 내용 작성이 필요합니다.
```
# PHP setting
Include /usr/local/etc/httpd/extra/httpd-php.conf
```
