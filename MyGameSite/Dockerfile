FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Копируем все файлы
COPY . .

# Собираем конкретный файл проекта в кавычках (чтобы пробел не ломал сборку)
RUN dotnet restore "MyGameSite/SkyNet RP.csproj"
RUN dotnet publish "MyGameSite/SkyNet RP.csproj" -c Release -o /app/out

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/out .
EXPOSE 8080
ENV ASPNETCORE_URLS=http://+:8080

ENTRYPOINT ["dotnet", "SkyNet RP.dll"]