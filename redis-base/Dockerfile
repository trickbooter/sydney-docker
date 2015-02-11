FROM        ubuntu:latest
MAINTAINER  trickbooter <paul@trickbooter.com>

# Install.
RUN \
  apt-get update && \
  apt-get install -y build-essential tar wget

# Get Redis.
RUN cd /tmp && \
  wget http://download.redis.io/redis-stable.tar.gz && \
  tar xvzf redis-stable.tar.gz

# Make Redis
RUN cd /tmp/redis-stable && \
  make && \
  make install

# Grab the built Redis executables and move them to usr/local/bin
# Move the Redis conf files into /etc/redis
RUN \
  cd /tmp/redis-stable && \
  cp -f src/redis-sentinel /usr/local/bin && \
  cp -f src/redis-cli /usr/local/bin && \
  mkdir -p /etc/redis && \
  cp -f *.conf /etc/redis


# Tidy Up
RUN rm -rf /tmp/redis-stable*
