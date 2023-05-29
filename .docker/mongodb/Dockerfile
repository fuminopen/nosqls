FROM ubuntu:latest

WORKDIR /root

# change key bind to vi
RUN set -o vi

# install curl
RUN apt -y update && \
    apt -y install curl

# install mongodb
RUN curl https://fastdl.mongodb.org/linux/mongodb-linux-aarch64-ubuntu2204-6.0.6.tgz --output ~/mongodb.tgz

# decompress mongdb tgz file
RUN tar xvfz ~/mongodb.tgz -C ~/

# move mongod and mongs to /usr/local/bin
RUN mv ~/mongo*/bin/mongo* /usr/local/bin/

RUN echo 'mongod is at ' $(which mongod)

RUN echo 'mongos is at ' $(which mongos)