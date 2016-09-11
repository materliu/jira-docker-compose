# 使用说明
利用此docker-compose配置， 迅速的在本地搭建起jira。

有几点是一定要注意的，mysql的配置需要修改， 设置成使用utf-8的编码格式。

docker-compose up

起来之后，访问 localhost:10011

但如果你想让JIRA连上mysql可没那么容易， 启动起来运行    后续操作id处请换成jira container的id

docker exec -it --user root 841d5ab77d41 /bin/bash   

以root用户登陆进去， 执行 chmod 777 -fR atlassian-jira 退出

docker-compose exec jira /bin/bash 以daemon的账户

进到 /opt/atlassian/jira/bin 执行 ./config.sh 来对JIRA进行配置， 这里配置JIRA的数据库连接方式， 退出

docker cp 7b71b9b09e66:/var/atlassian/jira/dbconfig.xml . #把配置文件拷出来

编辑此文件
jdbc:mysql://db:3306/jira?useUnicode=true&amp;characterEncoding=UTF8&amp;sessionVariables=storage_engine=InnoDB

修改为： jdbc:mysql://db:3306/jira?useUnicode=true&amp;characterEncoding=UTF8&amp;useSSL=false

docker cp ./dbconfig.xml 7b71b9b09e66:/var/atlassian/jira/dbconfig.xml #拷贝回去

退出后  docker-compose restart 重启

按照流程一步步走下去即可。





