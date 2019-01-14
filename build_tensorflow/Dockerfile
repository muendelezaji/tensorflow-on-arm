FROM debian:stretch

RUN dpkg --add-architecture armhf && dpkg --add-architecture arm64 \
    && apt-get update && apt-get install -y \
        openjdk-8-jdk automake autoconf \
        curl zip unzip libtool swig zlib1g-dev pkg-config git g++ wget xz-utils \
        python-numpy python-pip python-mock \
        python3-numpy python3-pip python3-mock \
        libpython-dev libpython-all-dev libpython3-dev libpython3-all-dev \
        libpython-dev:armhf libpython-all-dev:armhf libpython3-dev:armhf libpython3-all-dev:armhf \
        libpython-dev:arm64 libpython-all-dev:arm64 libpython3-dev:arm64 libpython3-all-dev:arm64

RUN echo "deb http://httpredir.debian.org/debian/ jessie main contrib non-free" > /etc/apt/sources.list.d/jessie.list \
    && apt-get update && apt-get install -y libpng12-dev bash-completion \
    && rm -f /etc/apt/sources.list.d/jessie.list \
    && rm -rf /var/lib/apt/lists/*

RUN pip install -U --user keras_applications==1.0.6 --no-deps \
    && pip install -U --user keras_preprocessing==1.0.5 --no-deps \
    && pip3 install -U --user keras_applications==1.0.6 --no-deps \
    && pip3 install -U --user keras_preprocessing==1.0.5 --no-deps \
    && ldconfig

ARG BAZEL_VERSION=0.18.0
RUN wget -q --no-check-certificate https://github.com/bazelbuild/bazel/releases/download/${BAZEL_VERSION}/bazel_${BAZEL_VERSION}-linux-x86_64.deb -P /tmp/ \
    && dpkg -i /tmp/bazel_${BAZEL_VERSION}-linux-x86_64.deb \
    && rm -f /tmp/bazel_${BAZEL_VERSION}-linux-x86_64.deb

WORKDIR /root
RUN git clone https://github.com/muendelezaji/tensorflow-on-arm/

WORKDIR /root/tensorflow-on-arm/build_tensorflow/
RUN git checkout v1.12.0
CMD ["/bin/bash"]
