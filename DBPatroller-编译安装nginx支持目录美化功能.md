# Nginx浏览目录配置及美化

在项目中有一个功能需要在浏览器页面中浏览服务器的目录。服务器使用Nginx，而Nginx提供了相应的[ngx_http_autoindex_module](http://nginx.org/en/docs/http/ngx_http_autoindex_module.html) 模块，该模块提供了我们想要的功能。

## Nginx-Fancyindex-Theme

这是从一个项目Fork过来，做了部分改动，并修复了少量bug后的完整的可用项目，需要的可以参考：[Nginx-Fancyindex-Theme](https://github.com/lanffy/Nginx-Fancyindex-Theme)

## Nginx ngx_http_autoindex_module 模块

### 该模块有以下几个命令：

| 命令                   | 默认值                    | 值域                                                                                | 作用域                    | EG                                                                  |
| -------------------- | ---------------------- | --------------------------------------------------------------------------------- | ---------------------- | ------------------------------------------------------------------- |
| autoindex            | off                    | on：开启目录浏览；                                                                        |                        |                                                                     |
| off：关闭目录浏览           | http, server, location | `autoindex on;`打开目录浏览功能                                                           |                        |                                                                     |
| autoindex_format     | html                   | html、xml、json、jsonp 分别用这几个风格展示目录                                                  | http, server, location | `autoindex_format html;` 以网页的风格展示目录内容。该属性在1.7.9及以上适用                |
| autoindex_exact_size | on                     | on：展示文件字节数；                                                                       |                        |                                                                     |
| off：以可读的方式显示文件大小     | http, server, location | `autoindex_exact_size off;` 以可读的方式显示文件大小，单位为 KB、MB 或者 GB，autoindex_format为html时有效 |                        |                                                                     |
| autoindex_localtime  | off                    | on、off：是否以服务器的文件时间作为显示的时间                                                         | http, server, location | `autoindex_localtime on;` 以服务器的文件时间作为显示的时间,autoindex_format为html时有效 |


## 目录浏览美化

我们使用开源的Fancy Index来美化页面，Github[看这里](https://github.com/aperezdc/ngx-fancyindex)

在美化之前，需要安装Nginx FancyIndex模块。安装模块步骤如下。

### 查看Nginx当前编译了哪些模块

要查看Nginx编译了哪些模块，执行以下命令：`2>&1 nginx -V | tr ' ' '\n'|grep module`，如下：
```bash
nginx version: nginx/1.13.8 built by clang 9.0.0 (clang-900.0.39.2) built with OpenSSL 1.1.0f 25 May 2017 TLS SNI support enabled configure arguments: --prefix=/usr/local/nginx --with-http_ssl_module --with-pcre --sbin-path=/usr/local/nginx/bin/nginx --with-cc-opt='-I/usr/local/opt/pcre/include -I/usr/local/opt/openssl@1.1/include' --with-ld-opt='-L/usr/local/opt/pcre/lib -L/usr/local/opt/openssl@1.1/lib' --conf-path=/usr/local/etc/nginx/nginx.conf --pid-path=/usr/local/var/run/nginx.pid --lock-path=/usr/local/var/run/nginx.lock --http-client-body-temp-path=/usr/local/var/run/nginx/client_body_temp --http-proxy-temp-path=/usr/local/var/run/nginx/proxy_temp --http-fastcgi-temp-path=/usr/local/var/run/nginx/fastcgi_temp --http-uwsgi-temp-path=/usr/local/var/run/nginx/uwsgi_temp --http-scgi-temp-path=/usr/local/var/run/nginx/scgi_temp --http-log-path=/usr/local/var/log/nginx/access.log --error-log-path=/usr/local/var/log/nginx/error.log --with-http_gzip_static_module --with-http_v2_module
```

### 动态编译添加Nginx模块

1. 在GitHub下载最新源码：[ngx-fancyindex](https://github.com/aperezdc/ngx-fancyindex/releases)
2. 源码下载下来后，解压，放到nginx源码目录(/usr/local/nginx)中,执行下面的代码，编译：

 `./configure --prefix=/usr/local/nginx --with-http_ssl_module --with-pcre --sbin-path=/usr/local/nginx/bin/nginx --with-cc-opt='-I/usr/local/opt/pcre/include -I/usr/local/opt/openssl@1.1/include' --with-ld-opt='-L/usr/local/opt/pcre/lib -L/usr/local/opt/openssl@1.1/lib' --conf-path=/usr/local/etc/nginx/nginx.conf --pid-path=/usr/local/var/run/nginx.pid --lock-path=/usr/local/var/run/nginx.lock --http-client-body-temp-path=/usr/local/var/run/nginx/client_body_temp --http-proxy-temp-path=/usr/local/var/run/nginx/proxy_temp --http-fastcgi-temp-path=/usr/local/var/run/nginx/fastcgi_temp --http-uwsgi-temp-path=/usr/local/var/run/nginx/uwsgi_temp --http-scgi-temp-path=/usr/local/var/run/nginx/scgi_temp --http-log-path=/usr/local/var/log/nginx/access.log --error-log-path=/usr/local/var/log/nginx/error.log --with-http_gzip_static_module --with-http_v2_module --add-module=ngx-fancyindex-0.4.2`

3. `make` **这里不要make install！！！**
4. 进入nginx源码目录下的`objs`目录，执行`2>&1 ./nginx -V | tr ' ' '\n'|grep fan`
5. 用`objs`目录下的nginx文件替换/usr/bin下面的nginx即可

### 选择Fancy Index主题

在Github里面找到了三个开源的主题，分别是:

- [https://github.com/Naereen/Nginx-Fancyindex-Theme](https://github.com/Naereen/Nginx-Fancyindex-Theme)
- [https://github.com/TheInsomniac/Nginx-Fancyindex-Theme](https://github.com/TheInsomniac/Nginx-Fancyindex-Theme)
- [https://github.com/lanffy/Nginx-Fancyindex-Theme](https://github.com/lanffy/Nginx-Fancyindex-Theme)

> 根据自已的喜好，选择任意主题均可，个人比较喜欢第三个主题。



