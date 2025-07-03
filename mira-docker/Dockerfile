FROM nginx:alpine

RUN apk add --no-cache libstdc++ postgresql-client icu-libs
COPY mira-docker/frontend/dist /usr/share/nginx/html

COPY mira-docker/backend /app/backend
WORKDIR /app/backend

COPY mira-docker/nginx/nginx.conf /etc/nginx/conf.d/default.conf
CMD (dotnet Mira.dll &) && nginx -g 'daemon off;'