
FROM alpine:edge
RUN apk add openssh-client
RUN apk add openmpi --update-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing

RUN apk add build-base
RUN apk add openmpi-dev --update-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing

WORKDIR /local
COPY mpitest.c .
RUN mpicc mpitest.c -o mpitest