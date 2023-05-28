FROM ubuntu:latest

RUN apt -y update && \
    apt -y install curl

RUN curl https://fastdl.mongodb.org/linux/mongodb-linux-aarch64-ubuntu2204-6.0.6.tgz --output ~/mongodb.tgz

RUN mkdir ~/mongodb

RUN tar xvfz ~/mongodb.tgz -C ~/mongodb/

RUN mv ~/mongodb/mongo* /usr/local/bin/

RUN echo 'mongod is at ' $(which mongod)

RUN echo 'mongos is at ' $(which mongos)