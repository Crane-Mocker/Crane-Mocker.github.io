# CentOS实用技巧


<!-- vim-markdown-toc GFM -->

* [网络配置](#网络配置)
	* [动态IP](#动态ip)
	* [ftp开放21端口](#ftp开放21端口)

<!-- vim-markdown-toc -->

## 网络配置

### 动态IP

刚安装好centos时需要手动配置网络。

`nmcli connection show [NAME]`查看[指定网卡的]网络配置
`nmcli connection modify NAME connection.autoconnect yes ipv4.method auto`指定网卡自动获取IP
此时ping IP就能ping 通了。
一般来说，此时ping Domain也能ping通了

### ftp开放21端口

```
firewall-cmd --permanent --add-port=21/tcp
firewall-cmd --permanent --add-service=ftp
firewall-cmd --reload
```

