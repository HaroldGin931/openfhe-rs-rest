FROM --platform=linux/amd64 ubuntu:22.04

# Set environment variables
ENV CARGO_TERM_COLOR always

# Install necessary dependencies
RUN apt-get update && apt-get install -y \
    cmake \
    git \
    curl \
    build-essential \
    libssl-dev \
    pkg-config \
    sudo \
    gdb \
    lldb \
    libgmp-dev \
    libomp-dev

# Clone OpenFHE, build and install
RUN git clone https://github.com/openfheorg/openfhe-development.git && \
    cd openfhe-development && \
    git checkout v1.2.0 && \
    mkdir build && \
    cd build && \
    cmake -DBUILD_SHARED=ON .. && \
    make -j$(nproc) && \
    make install && \
    ldconfig

# Install Rust and debugging tools
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y --default-toolchain stable
ENV PATH="/root/.cargo/bin:${PATH}"

# Clone OpenFHE-rs and build
RUN git clone https://github.com/fairmath/openfhe-rs.git && \
    cd openfhe-rs && \
    cargo build

# Set working directory
WORKDIR /workspace

# Add alias commands
RUN echo 'alias check-rust="rustc --version && cargo --version"' >> ~/.bashrc && \
    echo 'alias check-openfhe="make -C /openfhe-development/build/ testall"' >> ~/.bashrc && \
    echo 'alias check-openfhe-rs="cargo test --manifest-path /openfhe-rs/Cargo.toml -- --test-threads=1"' >> ~/.bashrc

# Make aliases effective immediately
RUN . ~/.bashrc

CMD ["bash"]