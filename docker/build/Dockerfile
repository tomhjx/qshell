FROM golang:1.17.5-bullseye as builder

RUN mkdir $HOME/src && \
    cd $HOME && \
    git clone --branch v2.6.2 https://github.com/qiniu/qshell.git && \
    cd qshell && \
    go install && \
    echo $PATH && \
    qshell -h && \
    which go qshell

FROM debian:bullseye-slim
COPY --from=builder /go/bin/qshell /usr/local/bin/qshell
