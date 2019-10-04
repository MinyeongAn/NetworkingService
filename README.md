# NetworkingService

# 라우터 R1
  - Window Server2012에서 라우팅<br>
  - 네트워크 어댑터 2개 사용<br>
  - rrasmgmt.msc에서 RIP 사용 인접라우터 등록<br>
  - 외부망 : 10.10.10.1/30<br>
  - 내부망 : 192.168.55.254/24<br>
  ![R1 rras](https://user-images.githubusercontent.com/49672285/66183557-50772c80-e6b4-11e9-93ef-1ef183a7e6f4.PNG)<br>

### DNS
<br>
- 운영체제 : Window Server 2012<br>
- ip 주소 : 192.168.55.10/24<br>
- 작업내역<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ DNS 서비스 제공<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ 서버 IP들의 DNS주소를 192.168.55.10으로 설정<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ 정방향에서 각 서버의 IP마다 도메인 네임 제공<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ 각 도메인 네임의 동작 확인<br>

### WEB
<br>
- 운영체제 : Window Server 2012<br>
- ip 주소 : 192.168.55.20/24<br>
- 작업내역<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ IIS 서비스로 IIS 웹페이지 띄우는 것 확인<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ IIS Default 웹에서 이미지파일 변경 후 적용내역 확인 [그림 IIS 확인]<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ XE를 설치, DB서버에서 DB만 받아와서 테스트 진행<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ 다른 서버장비에서도 접속되는지 확인<br>

# 라우터 R2
  - Window Server2012에서 라우팅<br>
  - 네트워크 어댑터 2개 사용<br>
  - rrasmgmt.msc에서 RIP 사용 인접라우터 등록<br>
  - 외부망 : 10.10.10.2/30<br>
  - 내부망 : 192.168.77.254/24<br>
  ![R2 rras](https://user-images.githubusercontent.com/49672285/66183830-24a87680-e6b5-11e9-8aaa-3a0cfd08d099.PNG)<br>

### DB
<br>
- 운영체제 : Linux CentOs 7<br>
- ip 주소 : 192.168.77.10/24<br>
- 작업내역<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ mariaDB 사용 방화벽에 3306포트와 mysql 서비스 등록<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ 테스트를 위한 Apache Web Server 사용<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ httpd 패키지, 방화벽 80번포트, httpd 서비스 등록<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ 편의를 위해 yum 사용, rpm 사용법 숙지완료<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ 그림 [Linux Firewall] 확인<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ /var/www/html/phpmyadmin에 위에 툴 설치<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ yum -y install --skip-broken php-*<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ /etc/httpd/conf/httpd.conf 165번줄<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ DirectoryIndex index.php index.html 수정<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ httpd 재실행<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ 그림 [Linux Packages] 확인<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ 제로보드 (https://www.xpressengine.com) 설치<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ /var/www/html/xe에 툴 설치<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ #chmod 707 xe<br>
&nbsp;&nbsp;&nbsp;&nbsp;→ 닉네임 아이디 administrator <br>

### ==라우터 설정 (pkt)==<br>
Router>en<br>
Router#conf t<br>
Router(config)#no ip domain lookup<br>
Router(config)#line co 0<br>
Router(config-line)#exec-t 0 0<br>
Router(config-line)#logging synchronous <br>
Router(config-line)#exit<br>
Router(config)#int fa0/0<br>
Router(config-if)#ip add 192.168.55.254 255.255.255.0<br>
Router(config-if)#no sh<br>
Router(config-if)#exit<br>
Router(config)#int fa1/0<br>
Router(config-if)#ip add 10.10.10.1 255.255.255.252<br>
Router(config-if)#no sh<br>
Router(config-if)#exit<br>
Router(config)#router rip<br>
Router(config-router)#network 192.168.55.0<br>
Router(config-router)#ver 2<br>
