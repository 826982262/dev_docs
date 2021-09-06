## 本地调试 TOMCAT 应用

#### 下载 tomcat:9
[apache-tomcat-9.0.52-windows-x64.zip](https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.52/bin/apache-tomcat-9.0.52-windows-x64.zip)

#### 准备应用配置文件`config/config.properties`
```
├── bin
│   ├── setenv.sh
├── conf
├── config
│   ├── config.properties
├── lib
├── logs
├── temp
├── webapps
│   └── ROOT.war
├── work
└── README
```

#### 在`bin`目录下增加环境配置文件`setenv.sh`
> 与`idea intellij` 的调试端口设置为`5005`
```
$ cat bin/setenv.sh
#!/bin/sh
#dir=$(cd `dirname $0`; pwd)
dir=$(dirname $(readlink -f $0))
config=$(readlink -f $dir/../config/config.properties)

export JAVA_OPTS="$JAVA_OPTS -Djfeat.config.properties=$config"
#export CATALINA_OPTS=" -agentlib:jdwp=transport=dt_socket,address=8000,server=y,suspend=n"
export CATALINA_OPTS="-Xdebug -Xrunjdwp:transport=dt_socket,server=y,address=5005,suspend=n"
```

#### 把目标调试`.war` 更名为 `webapps/ROOT.war`
> 清除 `webapps`下的示例文件（或保留 `host-manager`, `manager`）


#### 在本地启动`catalina.sh`
```
cd bin
./catalina.sh run
```

#### 用 `idea` 打开`war`项目源代码
> 设置调试端口为`5005`
- [idea 远程调试war包](https://www.jianshu.com/p/8b8bae237315)