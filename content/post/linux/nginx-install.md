---
title: "리눅스 Nginx 설치"
date: 2021-05-18T12:36:03+09:00
categories: 
- development
- linux
tags: 
- development
- front-end
- CentOS
- linux
- nginx
- 리눅스
- 서버
- 개발
keywords: 
- development
- front-end
cover: ""
draft: false
thumbnailImage: ""
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---

centos6

vi /etc/yum.repos.d/nginx.repo

\[nginx\]

name=nginx repo

baseurl=http://nginx.org/packages/centos/6/@basearch

gpgcheck=0

enabled=1

위 처럼 저장 후, 

yum install nginx

nginx -v

시작 : nginx

종료 : nginx -s stop

---

NGINX install support tls v1.3 in CentOS 7  
  
  
0\. Prerequisites openssl 1.1.1  
  
OpenSSL 1.1.1a upgrade for CentOS 7  
  
  
  
1\. Install redhat-lsb-core  
  
yum install redhat-lsb-core  
  
yum -y install wget openssl-devel libxml2-devel libxslt-devel gd-devel perl-ExtUtils-Embed GeoIP-devel pcre-devel  
  
2\. User add  
  
useradd builder  
groupadd builder  
  
3\. download  
  
wget [http://nginx.org/packages/mainline/centos/7/SRPMS/nginx-1.15.8-1.el7\_4.ngx.src.rpm](http://nginx.org/packages/mainline/centos/7/SRPMS/nginx-1.15.8-1.el7_4.ngx.src.rpm)  
  
4\. Configuration  
  
rpm -ivh [nginx-1.15.8-1.el7\_4.ngx.src.rpm](http://nginx-1.15.8-1.el7_4.ngx.src.rpm)  
sed -i “s|–with-http\_ssl\_module|–with-http\_ssl\_module –with-openssl=/usr/local/src/openssl-1.1.1a –with-openssl-opt=enable-tls1\_3 |g” /root/rpmbuild/SPECS/nginx.spec  
  
5\. Compile  
  
rpmbuild -ba /root/rpmbuild/SPECS/nginx.spec  
  
6\. Install  
  
rpm -ivh /root/rpmbuild/RPMS/x86\_64/nginx-1.15.8-1.el7\_4.ngx.x86\_64.rpm  
  
7\. Check version  
  
nginx -v  
  
8\. Reference  
  
How to Enable TLS 1.3 in Chrome, Safari and Firefox?