FROM golang:1.17.5-bullseye as builder

RUN mkdir $HOME/src && \
    cd $HOME && \
    git clone --branch v2.8.0 https://github.com/qiniu/qshell.git && \
    cd qshell && \
    go install && \
    echo $PATH && \
    qshell -h && \
    which go qshell

FROM debian:bullseye-slim
RUN apt-get update \
    && apt-get install -y --no-install-recommends ca-certificates \
    && update-ca-certificates
COPY --from=builder /go/bin/qshell /usr/local/bin/qshell
COPY entrypoint.sh /
RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    echo "Asia/Shanghai" > /etc/timezone \
    chmod +x /entrypoint.sh 
ENTRYPOINT ["/entrypoint.sh"]
CMD ["-h"]