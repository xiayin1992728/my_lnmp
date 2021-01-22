FROM mysql:5.7

MAINTAINER goozp "1084581212@qq.com"

# 设置容器时间和宿主机相同
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone