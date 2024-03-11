FROM debian:bookworm-slim

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    ca-certificates \
    lib32gcc-s1 \
    lib32stdc++6 \
    lib32z1 \
    rsync \
    unzip \
    wget \
    locales \
    && sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen \
    && dpkg-reconfigure --frontend=noninteractive locales \
    && rm -rf /var/lib/apt/lists/* \
    && useradd -m vietnam

USER vietnam

RUN mkdir /home/vietnam/Steam && \
    mkdir /home/vietnam/server

WORKDIR /home/vietnam/Steam

RUN wget -qO- https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz | tar zxf - \
    && /home/vietnam/Steam/steamcmd.sh +quit \
    && mkdir -p /home/vietnam/.steam/sdk64 \
    && ln -s /home/vietnam/Steam/linux64/steamclient.so /home/vietnam/.steam/sdk64/steamclient.so

WORKDIR /home/vietnam

COPY server.sh .

CMD [ "/home/vietnam/server.sh" ]