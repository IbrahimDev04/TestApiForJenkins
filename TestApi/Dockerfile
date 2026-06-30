# Build mərhələsi
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Layihə faylını kopyala
COPY *.csproj ./

# Paketləri bərpa et
RUN dotnet restore

# Bütün layihəni kopyala
COPY . .

# Publish et
RUN dotnet publish \
    -c Release \
    -o /app/publish

# Runtime mərhələsi
FROM mcr.microsoft.com/dotnet/aspnet:8.0

WORKDIR /app

COPY --from=build /app/publish .

EXPOSE 80
EXPOSE 443

ENTRYPOINT ["dotnet", "TestApi.dll"]