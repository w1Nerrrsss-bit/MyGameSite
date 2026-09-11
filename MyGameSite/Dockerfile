FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Копируем всё содержимое и ищем проект
COPY . .

# Собираем проект без явного указания имени .csproj
RUN dotnet restore
RUN dotnet publish -c Release -o /app/out

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/out .
EXPOSE 8080
ENV ASPNETCORE_URLS=http://+:8080

# Запуск приложения
ENTRYPOINT ["dotnet", "SkyNet RP.dll"]