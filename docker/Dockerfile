FROM litaio/ruby:latest
MAINTAINER Jimmy Cuadra <jimmy@jimmycuadra.com>

ENV HOME /home/lita
ENV GEM_HOME /home/lita/.gems
ENV PATH /home/lita/.gems/bin:$PATH
ENV PS1 '\u@lita-dev \w \$ '

RUN apt-get -qq update &&\
  apt-get -qy install socat sudo &&\
  sed -i.bkp -e\
    's/%sudo\s\+ALL=(ALL\(:ALL\)\?)\s\+ALL/%sudo ALL=NOPASSWD:ALL/g'\
    /etc/sudoers &&\
  useradd -m -g sudo lita
USER lita
WORKDIR /home/lita/workspace

RUN gem install lita

CMD exec socat tcp-listen:6379,fork tcp-connect:$REDIS_PORT_TCP_6379_ADDR:$REDIS_PORT_TCP_6379_PORT
