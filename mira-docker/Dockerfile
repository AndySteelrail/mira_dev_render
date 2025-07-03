FROM nginx:alpine

RUN apk add --no-cache libstdc++ postgresql-client icu-libs dotnet-runtime8.0

COPY mira-docker/frontend/dist /usr/share/nginx/html

COPY mira-docker/backend /app/backend
WORKDIR /app/backend

COPY mira-docker/nginx/nginx.conf /etc/nginx/conf.d/default.conf

RUN sed -i "s/listen 80;/listen \$PORT;/g" /etc/nginx/conf.d/default.conf

RUN echo $'#!/bin/sh\n\
dotnet Mira.dll &\n\
nginx -g "daemon off;"' > /start.sh && chmod +x /start.sh

CMD ["/bin/sh", "/start.sh"]