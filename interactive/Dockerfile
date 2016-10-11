FROM mhart/alpine-node:6

MAINTAINER quidmonkey <quidmonkey@gmail.com>

# Bash function to alias forge command to run in Docker container:
#     forge() {
#         docker run -it \
#             -v $(pwd):/data \
#             -v $HOME/.ssh:/root/.ssh \
#             --name forge \
#             quidmonkey/forge:latest /bin/bash
#     }
# Function should be run in a project directory with forge tasks.

VOLUME /data
WORKDIR /data

RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh ruby python3 && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --upgrade pip setuptools && \
    rm -r /root/.cache

RUN git clone --depth 1 -b Dockerfile https://github.com/quidmonkey/forge.git /.forge && \
    /.forge/install

RUN ln -sf $(which python3) /usr/local/bin/python
ENV PYTHON_PATH="/usr/local/bin/python"
