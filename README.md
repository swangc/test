# Sunallies-counter
光合联萌后台服务


## 模块说明
### cgweb -> api调用（提供前台访问调用）
### fe_agent -> 优化后api调用（提供前台访问调用）
### async_trans -> 处理支付响应后逻辑
### paynotify -> 响应第三方回调
### monkey_kk -> 自动化脚本
### pm -> api调用（提供中台管理使用）
### bigtail -> 后台清算



# 1 服务器分布
## 1. production
### 1. 10.174.139.190/139.196.14.184（GHLM-TA-PRO-01）
#### 1. servers/tomcat8_ta1/ -> async_trans/cgweb/fe_agent
#### 2. servers/tomcat8_ta2/ -> async_trans/cgweb/fe_agent
#### 3. servers/tomcat8_monkey/ -> monkey_kk
#### 4. servers/tomcat8_paynotify/ -> paynotify

### 2. 10.46.25.86/139.196.108.253（GHLM-TA-PRO-02）
#### 1. servers/tomcat8_paynotify1/ -> paynotify
#### 2. servers/tomcat8_paynotify2/ -> paynotify
#### 3. servers/tomcat8_ta/ -> async_trans/cgweb/fe_agent

### 3. 10.46.27.37/139.196.108.39（GHLM测试和生产中台）
### 1. servers/tomcat8_production/ -> bigtail/pm/ps



## 2. stage
#### 1. servers/tomcat8_stage_paynotify/ -> paynotify
#### 3. servers/tomcat8_stage_ta/ -> async_trans/cgweb/fe_agent/monkey_kk/pm



## 3. test
### 1. 10.46.27.37/139.196.108.39（GHLM测试和生产中台）
### 1. servers/tomcat8_test/ -> async_trans/cgweb/fe_agent/monkey_kk/paynotify/pm



# 2 部署步骤
## 1. cp 对应模块到临时目录 
## 2. 关闭需要更新的tomcat服务
## 3. 备份原项目内容
## 4. 拷贝新模块到webapp中
## 5. 开启tomcat服务
## 6. 验证服务是否正确开启

    eg: 已上传新模块 cgweb.war 在 ~/ 中
        cd servers/tomcat8_test/
        ./shutdown.sh
        tar -zf webapp.tar webapp./
        cp ~/cgweb.war ./webapp
        ./startup.sh

