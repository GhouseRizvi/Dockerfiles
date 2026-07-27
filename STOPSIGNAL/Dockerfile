FROM nginx:alpine

# Set custom stop signal
STOPSIGNAL SIGTERM

# Copy application files
COPY ./html /usr/share/nginx/html

# Expose port
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]