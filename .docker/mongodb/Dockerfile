FROM ubuntu:latest

WORKDIR /root

# change key bind to vi
RUN set -o vi

# install curl
RUN apt -y update && \
    apt -y install gnupg && \
    apt -y install curl

# install mongodb
RUN curl -fsSL https://pgp.mongodb.com/server-6.0.asc | \
   gpg -o /usr/share/keyrings/mongodb-server-6.0.gpg \
   --dearmor

RUN echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-6.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse" | \
    tee /etc/apt/sources.list.d/mongodb-org-6.0.list

RUN apt -y update

RUN apt-get install -y mongodb-org

RUN echo 'mongod is at ' $(which mongod)

RUN echo 'mongosh is at ' $(which mongosh)