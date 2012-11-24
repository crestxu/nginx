nginx
=====

debian .deb nginx with push_stream_module instead of HTTP_Push_Module
nginx version "nginx-1.2.5 stable"

1. apt-get install build-essential dpkg-dev debhelper autotools-dev libgeoip-dev libssl-dev libpcre3-dev zlib1g-dev
2. wget http://nginx.org/download/nginx-1.x.x.tar.gz
3. tar xvzf nginx-1.x.x.tar.gz
4. apt-get source nginx (you get a directory with latest nginx source (ex: 1.y.y))
5. cp -r nginx-1.y.y/debian/ nginx-1.x.x
6. rm nginx-1.x.x/debian/patches/*
7. nano (or alternative) nginx-1.x.x/debian/changelog, prepend: 
\* nginx (1.x.x-1) unstable; urgency=low

  * added stream push module
  * removed http push module

 -- kivlara   Sat, 25 Nov 2012 13:00:00 +0200
8. cd nginx-1.x.x/debian/modules/
9. git clone https://github.com/wandenberg/nginx-push-stream-module.git
10. edit nginx-1.x.x/debian/rules
11. add --add-module=$(CURDIR)/modules/nginx-push-stream-module \
12. cd nginx-1.x.x
13. dpkg-buildpackage -b (build)
14. dpkg -i nginx_1.x.x-1_amd64.deb (install)