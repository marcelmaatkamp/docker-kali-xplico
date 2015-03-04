FROM marcelmaatkamp/docker-alpine-build-base

EXPOSE 9001
ENV VERSION 0.2.5.10

RUN curl https://dist.torproject.org/tor-${VERSION}.tar.gz | tar xz -C /tmp

RUN cd /tmp/tor-${VERSION} && ./configure
RUN cd /tmp/tor-${VERSION} && make
RUN cd /tmp/tor-${VERSION} && make install
RUN cd /tmp/tor-${VERSION} && make clean

ADD ./torrc /etc/torrc
# Allow you to upgrade your relay without having to regenerate keys
VOLUME /.tor

# Generate a random nickname for the relay
RUN echo "Nickname docker$(head -c 16 /dev/urandom  | sha1sum | cut -c1-10)" >> /etc/torrc

CMD /usr/local/bin/tor -f /etc/torrc
