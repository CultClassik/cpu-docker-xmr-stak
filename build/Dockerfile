FROM library/alpine:3.6

LABEL "maintainer"="Chris Diehl <cultclassik@gmail.com>"

ENV WALLET_ADDRESS="447vxA7StEu5Ht9p8MiWNmhLo48dYnfwPGUYtxUAArxKD6DkSthnQiVL843NKEC1oGTS6Gmu3XaoK3uBcQ118zXaFPjLdxz"
ENV POOL_ADDRESS="mine.moneropool.com:3333"
ENV CURRENCY="monero"
ENV HTTPD_PORT=3000
ENV HTTP_LOGIN="http_user"
ENV HTTP_PASS="http_pass"

WORKDIR /tmp

RUN apk --no-cache upgrade \
        && apk --no-cache add \
                git \
                cmake \
                automake \
                autoconf \
                build-base \
                openssl-dev \
                libmicrohttpd-dev \
                bash \
        && git clone https://github.com/fireice-uk/xmr-stak.git \
        && cd xmr-stak \
        && printf "#pragma once\nconstexpr double fDevDonationLevel = 0.0 / 100.0;" \
                > ./xmrstak/donate-level.hpp \
        && cmake . \
                -DCUDA_ENABLE=OFF \
                -DOpenCL_ENABLE=OFF \
                -DHWLOC_ENABLE=OFF \
        && make \
        && cd - \
        && mv /tmp/xmr-stak/bin/* /usr/local/bin/ \
        && rm -rf /tmp/* \
        && apk del \
                git \
                automake \
                autoconf \
                build-base

ADD ./script/* /xmr-stak/

WORKDIR /xmr-stak

RUN chmod +x /xmr-stak/*.sh

CMD [ "/xmr-stak/run.sh"]