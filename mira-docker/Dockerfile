FROM nginx:alpine

RUN apk add --no-cache libstdc++ postgresql-client icu-libs
COPY ../frontend/dist /usr/share/nginx/html

COPY ../backend /app/backend
WORKDIR /app/backend

COPY ../nginx/nginx.conf /etc/nginx/conf.d/default.conf
CMD (dotnet Mira.dll &) && nginx -g 'daemon off;'