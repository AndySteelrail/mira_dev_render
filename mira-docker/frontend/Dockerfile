FROM node:18
WORKDIR /app
COPY . .
RUN npm install && npm run build
RUN npm install -g serve
EXPOSE $PORT
CMD ["serve", "-s", "dist", "-l", "$PORT"]