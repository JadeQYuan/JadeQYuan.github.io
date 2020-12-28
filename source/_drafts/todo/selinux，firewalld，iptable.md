selinux  ( /etc/selinux/config)
	安全增强型 Linux（Security-Enhanced Linux）简称 SELinux，它是一个 Linux 内核模块，也是 Linux 的一个安全子系统。
	SELinux 主要由美国国家安全局开发。2.6 及以上版本的 Linux 内核都已经集成了 SELinux 模块。
	SELinux 主要作用就是最大限度地减小系统中服务进程可访问的资源（最小权限原则）。

firewalld
	firewall能够允许哪些服务可用，那些端口可用.... 属于更高一层的防火墙。
	firewall的底层是使用iptables进行数据过滤，建立在iptables之上。
	firewall是动态防火墙，使用了D-BUS方式，修改配置不会破坏已有的数据链接。

iptables
	iptables用于过滤数据包，属于网络层防火墙.
	在设置iptables后需要重启iptables，会重新加载防火墙模块，而模块的装载将会破坏状态防火墙和确立的连接。会破坏已经对外提供数据链接的程序。可能需要重启程序。
