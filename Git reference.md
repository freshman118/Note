# Git异常

**现象**

```shell
OpenSSL SSL_read: Connection was reset, errno 10054
```

**方案**

```shell
# 解除ssl验证
git config --global http.sslVerify "false"
```



# 
