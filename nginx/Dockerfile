FROM nginx:stable-alpine

LABEL author="purivaro <aun.puri@gmail.com>"
LABEL version="1.0"

ENV TZ=Asia/Bangkok
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone