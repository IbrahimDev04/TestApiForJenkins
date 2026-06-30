# Build mərhələsi
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Project faylını kopyala və restore et
COPY *.csproj ./
RUN dotnet restore

# Layihənin qalan hissəsini kopyala
COPY . ./

# Publish
RUN dotnet publish -c Release -o /app/publish

# Runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0

WORKDIR /app

# Tətbiqin 8081 portunda dinləməsini təmin et
ENV ASPNETCORE_URLS=http://+:8081

EXPOSE 8081

# Publish olunmuş faylları kopyala
COPY --from=build /app/publish .

# Tətbiqi işə sal
ENTRYPOINT ["dotnet", "TestApi.dll"]