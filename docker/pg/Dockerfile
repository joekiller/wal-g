FROM wal-g/ubuntu:jammy

ENV PGDATA /var/lib/postgresql/14/main
ENV PATH /usr/lib/postgresql/14/bin:$PATH

RUN apt-get update && \
    apt-get install --yes --no-install-recommends --no-install-suggests \
    postgresql-14 \
    postgresql-contrib \
    gnupg \
    gpg-agent \
    time \
    bc \
    jq \
    s3cmd \
    python3.10 \
    python3-setuptools \
    python3-pip \
    lzop \
    pv && \
    python3.10 -m pip install --upgrade pip && \
    python3.10 -m pip install git+https://github.com/wal-e/wal-e.git && \
    python3.10 -m pip install boto

COPY docker/pg/PGP_KEY /tmp/PGP_KEY
COPY docker/pg/SSH_KEY /tmp/SSH_KEY
COPY docker/pg/gpg.conf /var/lib/postgresql/.gnupg/gpg.conf
COPY docker/pg/gpg-agent.conf /var/lib/postgresql/.gnupg/gpg-agent.conf

COPY docker/common/s3cfg /var/lib/postgresql/.s3cfg

COPY docker/pg/walg.json /tmp/walg.json

RUN rm -rf $PGDATA

RUN chmod 777 /var/lib/postgresql/.gnupg
