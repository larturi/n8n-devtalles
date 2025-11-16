FROM postgres:16-bullseye

# Instalamos dependencias necesarias para compilar pgvector
RUN apt-get update && apt-get install -y --no-install-recommends \
    wget \
    ca-certificates \
    gnupg \
    git \
    build-essential \
    postgresql-server-dev-16 \
    && \
    wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | gpg --dearmor > /etc/apt/trusted.gpg.d/llvm-snapshot.gpg && \
    echo "deb http://apt.llvm.org/bullseye/ llvm-toolchain-bullseye-14 main" | tee /etc/apt/sources.list.d/llvm.list && \
    apt-get update && apt-get install -y --no-install-recommends \
    llvm-14 \
    clang-14 \
    && rm -rf /var/lib/apt/lists/*

# Clonamos y compilamos pgvector
RUN git clone https://github.com/pgvector/pgvector.git /tmp/pgvector && \
    cd /tmp/pgvector && \
    make CC=clang-14 OPTFLAGS="" && make install && \
    cd / && rm -rf /tmp/pgvector

# Exponemos puerto y lanzamos postgres
EXPOSE 5432
CMD ["postgres"]
