#*******************************************************************************
#    (c) 2020 Zondax GmbH
#
#   Licensed under the Apache License, Version 2.0 (the "License");
#   you may not use this file except in compliance with the License.
#   You may obtain a copy of the License at
#
#       http://www.apache.org/licenses/LICENSE-2.0
#
#   Unless required by applicable law or agreed to in writing, software
#   distributed under the License is distributed on an "AS IS" BASIS,
#   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#   See the License for the specific language governing permissions and
#   limitations under the License.
#*******************************************************************************
FROM rust:1.57.0

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
    apt-get install -y curl apt-utils protobuf-compiler

RUN rustc --version

RUN rustup toolchain install 1.53.0
RUN rustup component add clippy
RUN rustup component add rustfmt
RUN cargo install sccache
RUN cargo install cargo-audit
RUN cargo install wasm-pack
RUN cargo install cargo-tree

# Install lastest lts node
RUN curl -sL https://deb.nodesource.com/setup_16.x | bash -
RUN apt-get -y install nodejs sudo
RUN npm install -g yarn

RUN node -v
RUN yarn --version
RUN yarn global add n
RUN n lts_latest -q

# Add github user (1001) to sudoers list
RUN adduser --disabled-password --gecos "" -u 1001 github
RUN echo "github ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

ENV RUSTC_WRAPPER sccache
ENV SCCACHE_CACHE_SIZE 1G
