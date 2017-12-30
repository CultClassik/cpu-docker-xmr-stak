FROM library/alpine:3.6

LABEL "maintainer"="Chris Diehl <cultclassik@gmail.com>"

ENV WORKER="myminer"
ENV POOL_USER="447vxA7StEu5Ht9p8MiWNmhLo48dYnfwPGUYtxUAArxKD6DkSthnQiVL843NKEC1oGTS6Gmu3XaoK3uBcQ118zXaFPjLdxz"
ENV POOL_PASS="x"
ENV POOL_URL="mine.moneropool.com:3333"
ENV CURRENCY="monero"

RUN apk --no-cache upgrade &&\
    apk --no-cache add \
        cmake \
        automake \
        autoconf \
        openssl-dev \
        git \
        build-base

WORKDIR /tmp

RUN git clone https://github.com/fireice-uk/xmr-stak.git &&\
         cd xmr-stak &&\
         cmake . \
                 -DCUDA_ENABLE=OFF \
                 -DOpenCL_ENABLE=OFF \
                 -DHWLOC_ENABLE=OFF \
                 -DMICROHTTPD_ENABLE=OFF \
         && make \
         && cd - \
         && mv /tmp/xmr-stak/bin/* /usr/local/bin/ \
         && rm -rf /tmp/xmr-stak \
         && apk del \
                 automake \
                 autoconf \
                 build-base \
                 git


WORKDIR /

CMD [ "xmr-stak", "--currency", "${CURRENCY}", "--url", "${POOL_URL}", "--user", "${POOL_USER}", "--pass", "${POOL_PASS}" ]