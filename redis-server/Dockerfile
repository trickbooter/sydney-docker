FROM        trickbooter/redis-base:latest
MAINTAINER  trickbooter <paul@trickbooter.com>

# Expose ports.
EXPOSE      6379

# Define mountable directories.
VOLUME ["/data"]

# Configure Redis Server
RUN \
  sed -i 's/^\(bind .*\)$/# \1/' /etc/redis/redis.conf && \
  sed -i 's/^\(daemonize .*\)$/# \1/' /etc/redis/redis.conf && \
  sed -i 's/^\(dir .*\)$/# \1\ndir \/data/' /etc/redis/redis.conf && \
  sed -i 's/^\(logfile .*\)$/# \1/' /etc/redis/redis.conf && \
  sed -i 's/^\(loglevel .*\)$/# \1\nloglevel Verbose/' /etc/redis/redis.conf

# Fire-up Redis and pass in our config file
CMD ["redis-server", "/etc/redis/redis.conf"]
