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
FROM rust:1.53.0

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
    apt-get install -y curl apt-utils protobuf-compiler

RUN rustc --version

RUN rustup component add clippy
RUN rustup component add rustfmt
RUN cargo install sccache
RUN cargo install cargo-audit
RUN cargo install wasm-pack

# Add fixed 1.47
RUN rustup toolchain install 1.47.0
RUN rustup component add rustfmt --toolchain 1.47.0
RUN rustup component add clippy --toolchain 1.47.0
RUN cargo +1.47.0 install sccache
RUN cargo +1.47.0 install cargo-audit
RUN cargo +1.47.0 install wasm-pack
RUN cargo +1.47.0 install cargo-tree

# Add fixed 1.49
RUN rustup toolchain install 1.49.0
RUN rustup component add rustfmt --toolchain 1.49.0
RUN rustup component add clippy --toolchain 1.49.0
RUN cargo +1.49.0 install sccache
RUN cargo +1.49.0 install cargo-audit
RUN cargo +1.49.0 install wasm-pack
RUN cargo +1.49.0 install cargo-tree

# Install latest node
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get -y install nodejs
RUN npm install -g yarn

RUN node -v
RUN yarn --version
RUN yarn global add n
RUN n latest -q

ENV RUSTC_WRAPPER sccache
ENV SCCACHE_CACHE_SIZE 1G
