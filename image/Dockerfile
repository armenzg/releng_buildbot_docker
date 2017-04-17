FROM           ubuntu:17.04
MAINTAINER     Armen Zambrano G. <armenzg@mozilla.com>

# Besides basic packages we need few more in order to allow installing Python's cryptography package
RUN apt-get -y update && \
    apt-get install -y mercurial python-pip virtualenv wget \
                       build-essential libssl-dev libffi-dev python-dev && \
    apt-get clean
RUN hg clone https://hg.mozilla.org/build/braindump
COPY hgrc /root/.hgrc
CMD ["/bin/bash", "--login"]
