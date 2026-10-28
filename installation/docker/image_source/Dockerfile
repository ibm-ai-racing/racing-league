FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive
ENV DISPLAY=:0

# 1. Install build tools, libraries, Xvfb, window manager, VNC stack, and unzip
RUN apt-get update && apt-get install -y \
    git \
    build-essential \
    pkg-config \
    libgl1-mesa-dev \
    libglu1-mesa-dev \
    libplib-dev \
    libopenal-dev \
    libalut-dev \
    libvorbis-dev \
    libxxf86vm-dev \
    libxi-dev \
    libxmu-dev \
    libxrender-dev \
    libxrandr-dev \
    libpng-dev \
    zlib1g-dev \
    freeglut3-dev \
    libglib2.0-dev \
    unzip \
    xvfb \
    x11vnc \
    novnc \
    websockify \
    fluxbox \
    supervisor \
    && rm -rf /var/lib/apt/lists/*

# 2. Build TORCS from source (fmirus repository with SCR patch)
WORKDIR /opt
RUN git clone https://github.com/fmirus/torcs-1.3.7.git torcs-src

WORKDIR /opt/torcs-src
RUN ./configure --prefix=/usr/local/torcs && \
    make && \
    make install && \
    make datainstall

ENV TORCS_HOME=/usr/local/torcs
ENV PATH="$TORCS_HOME/bin:$PATH"
ENV LD_LIBRARY_PATH="/usr/local/torcs/lib:${LD_LIBRARY_PATH}"

# Register TORCS shared libraries
RUN echo "/usr/local/torcs/lib" > /etc/ld.so.conf.d/torcs.conf && ldconfig

# 3. Copy and extract the SCR server plugin
COPY scr_server.zip /tmp/scr_server.zip
RUN mkdir -p /usr/local/torcs/share/games/torcs/drivers/ && \
    unzip -o /tmp/scr_server.zip -d /usr/local/torcs/share/games/torcs/drivers/ && \
    rm -rf /usr/local/torcs/share/games/torcs/drivers/__MACOSX && \
    find /usr/local/torcs/share/games/torcs/drivers/ -name ".DS_Store" -delete && \
    rm -f /tmp/scr_server.zip

# 4. Copy Supervisord configuration
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# 5. Expose ports (8080 for web viewing, 3001 for Python client connection)
EXPOSE 8080 3001

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]