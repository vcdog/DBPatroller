

# nginx配置代码

```bash

# 支持下载功能
location /download{
    alias /data/batch_db_reports_data/inspection_data_report; 
    fancyindex on;              #启用 fancy 索引
    fancyindex_exact_size off;  #输出人类可读的文件大小
    autoindex on; #开启目录浏览
    autoindex_format html; #以html风格将目录展示在浏览器中
    autoindex_exact_size off; #切换为 off 后，以可读的方式显示文件大小，单位为 KB、MB 或者 GB
    autoindex_localtime on; #以服务器的文件时间作为显示的时间
    charset utf-8,gbk; #展示中文文件名

    #添加同时支持下载和预览文件功能
    if ($request_filename ~* ^.*?\.(html|doc|pdf|zip|docx|txt|conf|gz|xz|rar|sql)$) {
        add_header Content-Disposition attachment;
        add_header Content-Type application/octet-stream;
    }  

    #设置访问密码，按需开启
    auth_basic "数据库巡检报告访问验证";
    auth_basic_user_file /usr/local/nginx/conf/.passwd;  # 自定义一个绝对路径的密码文件
}

# 支持在线预览功能
location /report{
    alias /data/batch_db_reports_data/inspection_data_report; #当前报告路径
    
    # 目录美化配置
    fancyindex on;              #启用 fancy 索引
    fancyindex_exact_size off;  #输出人类可读的文件大小
    autoindex on; #开启目录浏览
    autoindex_format html; #以html风格将目录展示在浏览器中
    autoindex_exact_size off; #切换为 off 后，以可读的方式显示文件大小，单位为 KB、MB 或者 GB
    autoindex_localtime on; #以服务器的文件时间作为显示的时间
    charset utf-8,gbk; #展示中文文件名
    #密码，按需开启
    auth_basic "数据库巡检报告访问验证";
    auth_basic_user_file /usr/local/nginx/conf/.passwd; # 自定义一个绝对路径的密码文件
}

#历史归档报告在线预览功能
location /arch{
    alias /data/batch_db_reports_data/inspection_arch_data_backup; #归档报告路路径
    fancyindex on;              #启用 fancy 索引
    fancyindex_exact_size off;  #输出人类可读的文件大小
    autoindex on;               #开启目录浏览
    autoindex_format html;      #以html风格将目录展示在浏览器中
    autoindex_exact_size off;   #切换为off后，以可读的方式显示文件大小，单位为 KB,MB,GB
    autoindex_localtime on;     #以服务器的文件时间作为显示的时间
    charset utf-8,gbk;          #展示中文文件名
    #密码，按需开启
    auth_basic "数据库巡检报告访问验证";
    auth_basic_user_file /usr/local/nginx/conf/.passwd;# 自定义一个绝对路径的密码文件
}

```