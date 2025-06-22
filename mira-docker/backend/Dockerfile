FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app

COPY . .

RUN apt-get update && \
    apt-get install -y postgresql-client && \
    rm -rf /var/lib/apt/lists/*

ENV ASPNETCORE_URLS=http://+:5000
EXPOSE 5000

CMD dotnet Mira.dll