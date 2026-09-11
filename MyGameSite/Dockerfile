FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Копируем все файлы проекта
COPY . .

# Автоматически находим .csproj и собираем его
RUN dotnet restore $(ls *.csproj 2>/dev/null || ls */*.csproj 2>/dev/null)
RUN dotnet publish $(ls *.csproj 2>/dev/null || ls */*.csproj 2>/dev/null) -c Release -o /app/out

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/out .
EXPOSE 8080
ENV ASPNETCORE_URLS=http://+:8080

# Возвращаем исходное имя сборки MyGameSite.dll
ENTRYPOINT ["dotnet", "MyGameSite.dll"]