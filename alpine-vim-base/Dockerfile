FROM frolvlad/alpine-mono

MAINTAINER dkil1972 <dermot.kilroy@invoko.co.uk>

#setup the home directory - see https://github.com/JAremko/docker-alpine-base
RUN mkdir -p /home/developer/workspace
ENV HOME /home/developer

ADD tidy-viml /util/

RUN apk add --update --virtual build-deps python2 python2-dev python3 python3-dev ctags build-base    \
      make libxpm-dev libx11-dev libxt-dev ncurses-dev git                   && \
    ls -al /usr/lib                                                         && \
    cd /tmp                                                                  && \
    git clone https://github.com/vim/vim                                     && \
    cd /tmp/vim                                                              && \
    ./configure --with-features=huge                                             \
                --enable-multibyte                                              \
                --enable-pythoninterp                                           \
                --with-python-config-dir=/usr/lib/python2.7/config-x86_64-linux-gnu              \
                --enable-python3interp                                           \
                --with-python3-config-dir=/usr/lib/python3.8/config-3.8-x86_64-linux-gnu              \
                --disable-gui                                                   \
                --disable-netbeans                                              \
                --prefix /usr                                                && \
    make install                                                             && \
    apk del build-deps                                                       && \
    apk add libsm libice libxt libx11 ncurses                                && \
    #cleanup
    rm -rf /var/cache/* /var/log/* /var/tmp/*                                && \
    mkdir /var/cache/apk

ENTRYPOINT ["vim"]
