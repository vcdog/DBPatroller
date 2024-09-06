

## 1.输入如下命令即可可生成数据库检查报告：
   ```sql
   
  # mysql -h 172.17.44.66  -u root  -p'123456' -P 3306 --html -t  -f --silent < ./DBPatroller.sh
  ```

## 2.巡检报告默认保存路径如下：
  ```bash
  # ll /tmp/Sunac_Dbpatroller_Mysql_Report_20240905145631.html
  ```

## 3.下载及查看巡检报告：
  ```bash
  # sz /tmp/Sunac_Dbpatroller_Mysql_Report_20240905145631.html
  ```
## 4.巡检报告的解读可参考：

[数据库巡检报告帮助文档](https://sunac.feishu.cn/docx/XVJtdChvgoW4Szxpm0Jc2KNSn1e)
