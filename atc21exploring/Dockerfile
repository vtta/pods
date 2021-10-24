FROM ubuntu:bionic
RUN apt-get update && apt-get install -y linux-source-5.3 linux-headers-5.3.0-76-generic
RUN apt-get install -y git build-essential kernel-package fakeroot libncurses5-dev libssl-dev ccache bison flex libelf-dev dwarves6
RUN apt-get install -y rpm neovim rsync
RUN git clone https://github.com/csl-ajou/AutoTiering
RUN cd AutoTiering/linux-5.3.0-autotiering \
    && cp /usr/src/linux-headers-5.3.0-76-generic/.config . \
    && echo $'CONFIG_PAGE_BALANCING=y\nCONFIG_PAGE_BALANCING_DEBUG=y\nCONFIG_PAGE_FAULT_PROFILE=y' >> .config
RUN make olddefconfig \
    && make -j$(nproc) binrpm-pkg bindeb-pkg \
    && cp ../*.deb ~/rpmbuild/RPMS/x86_64/
CMD [ "cmd" ]