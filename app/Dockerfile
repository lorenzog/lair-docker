FROM node:8.9.0

EXPOSE 11014

WORKDIR /root/app
RUN apt-get update
RUN apt-get install -y bsdtar && ln -sf $(which bsdtar) $(which tar)

# from https://github.com/lair-framework/lair-docker/pull/21/commits/b174836f8a882cca57036cdc8bce30854316f24b
RUN curl https://install.meteor.com/?release=1.7.0.5 | sh
RUN curl -SLO "https://github.com/lair-framework/lair/releases/download/v2.5.0/lair-v2.5.0-linux-amd64.tar.gz" \
    && tar -zxf lair-v2.5.0-linux-amd64.tar.gz \
    && cd bundle/programs/server \
    && npm i

COPY ./package.json /root/app/bundle/programs/server/package.json

ENV ROOT_URL=http://0.0.0.0
ENV PORT 11014
ENV MONGO_URL=mongodb://lairdb:27017/lair
ENV MONGO_OPLOG_URL=mongodb://lairdb:27017/local

CMD sleep 4 && cd /root/app/bundle/programs/server && meteor npm start
