FROM redis:alpine
VOLUME /data
COPY ./redis/redis.conf /etc/redis/redis.conf
CMD ["redis-server", "/etc/redis/redis.conf"]
EXPOSE 6379
