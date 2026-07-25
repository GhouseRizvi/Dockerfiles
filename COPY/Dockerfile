FROM almalinux
RUN yum install -y epel-release && \
    yum install -y nginx && \
    rm -rf /usr/share/nginx/html/index.html
COPY 2168_sweet_bakery/* /usr/share/nginx/html/
CMD ["nginx", "-g", "daemon off;"]

