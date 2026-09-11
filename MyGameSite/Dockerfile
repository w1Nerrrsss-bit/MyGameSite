FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Копируем все файлы
COPY . .

# Собираем файл проекта напрямую (ищем .csproj в любой подпапке)
RUN dotnet restore *.csproj || dotnet restore */*.csproj
RUN dotnet publish *.csproj -c Release -o /app/out || dotnet publish */*.csproj -c Release -o /app/out

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/out .
EXPOSE 8080
ENV ASPNETCORE_URLS=http://+:8080

ENTRYPOINT ["dotnet", "SkyNet RP.dll"]