## HAProxy
- 下载

		wget http://fossies.org/linux/misc/haproxy-1.6.9.tar.gz
- 解压

		tar -zxvf haproxy-1.6.9.tar.gz
		cd haproxy-1.6.9
- 安装

		make TARGET=linux2628 ARCH=x86_64 PREFIX=/usr/local/haproxy
		make install PREFIX=/usr/local/haproxy

		// 参数说明

		TARGET=linux26 #内核版本，使用uname -r查看内核，如：2.6.18-371.el5，此时该参数就为linux26；kernel 大于2.6.28的用：TARGET=linux2628
		ARCH=x86_64 #系统位数
		PREFIX=/usr/local/haprpxy # /usr/local/haprpxy为haprpxy安装路径

- 配置文件haproxy.cfg

		global
				daemon
				maxconn 65535
		defaults
				mode http
				timeout connect 5000ms
				timeout client 5000ms
				timeout server 5000ms
		frontend http-in
				bind *:80
				default_backend servers
		backend servers
				server server1 192.168.1.2:80 cookie ser1 weight 10 check inter 2000 rise 2 fall 3
				server server2 192.168.1.3:80 cookie ser2 weight 10 check inter 2000 rise 2 fall 3
				server server3 192.168.1.4:80 cookie ser3 weight 10 check inter 2000 rise 2 fall 3
- 启动

		/usr/local/haproxy/sbin/haproxy -f /usr/local/haproxy/haproxy.cfg 