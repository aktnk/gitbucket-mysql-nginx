FROM nginx:1.23.4

ENV TZ Asia/Tokyo
RUN echo "${TZ}" > /etc/timezone \
    && dpkg-reconfigure -f noninteractive tzdata
