FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY backend/ .  # Копируем только папку backend
RUN dotnet publish -c Release -o /app

FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app .
COPY --from=build /app/Migrations ./Migrations  # Если миграции не копируются автоматически

RUN apt-get update && \
    apt-get install -y postgresql-client && \
    rm -rf /var/lib/apt/lists/*

ENV ASPNETCORE_URLS=http://*:$PORT
EXPOSE $PORT

CMD until pg_isready -h ${DB_HOST} -U ${DB_USER} -d ${DB_NAME}; do sleep 1; done && \
    dotnet Mira.dll