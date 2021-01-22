FROM alpine:3.7

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
&& apk update && apk upgrade \
&& apk add gcc g++ make libffi-dev openssl-dev