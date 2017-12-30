FROM library/alpine:3.6

LABEL "maintainer"="Chris Diehl <cultclassik@gmail.com>"

ENV MINER_URL="https://api.github.com/repos/fireice-uk/xmr-stak/releases/latest"

ENV WORKER="myminer"
ENV POOL_USER="447vxA7StEu5Ht9p8MiWNmhLo48dYnfwPGUYtxUAArxKD6DkSthnQiVL843NKEC1oGTS6Gmu3XaoK3uBcQ118zXaFPjLdxz"
ENV POOL_PASS="x"
ENV POOL_URL="mine.moneropool.com:3333"
ENV CURRENCY="monero"

RUN apk --no-cache upgrade &&\
    apk --no-cache add \
        curl

RUN mkdir /miner

WORKDIR /tmp

RUN curl -O `curl -s ${MINER_URL} | grep -o 'browser_download_url.*xmr-stak-portbin-linux.tar.gz' | sed 's/.*"//'`

RUN tar xzf  -C /miner --strip-components 1

RUN rm xmr-stak-portbin-linux.tar.gz

WORKDIR /miner

CMD [ "/miner/xmr-stak", "--currency", "${CURRENCY}", "--url", "${POOL_URL}", "--user", "${POOL_USER}", "--pass", "${POOL_PASS}" ]