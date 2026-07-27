FROM nginx
VOLUME /usr/share/nginx/html
RUN mkdir /myvol
RUN echo "Hello from my volume!" > /myvol/index.html
VOLUME /myvol
