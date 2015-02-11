FROM        ubuntu:latest
MAINTAINER  trickbooter <paul@trickbooter.com>

# RUN         apt-get update && apt-get install -y redis-server

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

# Configure Redis Server
RUN \
  cd /tmp/redis-stable && \
  sed -i 's/^\(bind .*\)$/# \1/' /etc/redis/redis.conf && \
  sed -i 's/^\(daemonize .*\)$/# \1/' /etc/redis/redis.conf && \
  sed -i 's/^\(dir .*\)$/# \1\ndir \/data/' /etc/redis/redis.conf && \
  sed -i 's/^\(logfile .*\)$/# \1/' /etc/redis/redis.conf && \
  sed -i 's/^\(loglevel .*\)$/# \1\nloglevel Verbose/' /etc/redis/redis.conf

# Tidy Up
RUN rm -rf /tmp/redis-stable*

# Add our entrypoint helper
ADD ep /ep
RUN chmod +x /ep

# Expose ports.
EXPOSE      6379

# Define mountable directories.
VOLUME ["/data"]

# Send us to the entrypoint
ENTRYPOINT ["/ep"]
