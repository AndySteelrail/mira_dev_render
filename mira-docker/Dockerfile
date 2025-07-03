FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base

RUN apt-get update && \
    apt-get install -y nginx postgresql-client && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY mira-docker/backend ./

RUN mkdir -p /var/www/html
COPY mira-docker/frontend/dist /var/www/html
COPY mira-docker/nginx/nginx.conf /etc/nginx/sites-available/default

RUN sed -i "s/listen 80/listen \$PORT/g" /etc/nginx/sites-available/default

RUN nginx -t

RUN echo $'#!/bin/bash\n\
service nginx start\n\
dotnet Mira.dll' > /start.sh && chmod +x /start.sh

EXPOSE 5000
CMD ["/bin/bash", "/start.sh"]