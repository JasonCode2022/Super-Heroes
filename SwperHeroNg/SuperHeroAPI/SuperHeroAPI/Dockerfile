FROM docker.io/library/build:latest

# Build stage
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build-env
WORKDIR /SuperHeroAPI

# Copy csproj and restore as distinct layers
COPY *.csproj .
RUN dotnet restore

# Copy everything else and build
COPY . .
RUN dotnet publish -c Release -o out

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /SuperHeroAPI

# Copy the built API and EF files from the build stage
COPY --from=build-env /SuperHeroAPI/out .

# Expose ports 5000 for the API and 1433 for EF
EXPOSE 5000
EXPOSE 1433


# Set environment variables
ENV ASPNETCORE_ENVIRONMENT=Production
ENV ConnectionStrings__DefaultConnection=Server=JASONPC\\SQLEXP_2K19_2022;Database=SuperHeroDb;User=sa;Password=Sa_Password;PersistSecurityInfo=True;trustServerCertificate=true;

# Install MySQL client library
RUN apt-get update && apt-get install -y default-mysql-client

# Copy initialization script
# COPY init.sql /docker-entrypoint-initdb.d/
#COPY ./sql/init.sql /docker-entrypoint-initdb.d/

# Copy initialization script for Entity Framework
#COPY ./SuperHeroAPI/init.sql /init.sql

# Start the application
ENTRYPOINT ["dotnet", "SuperHeroAPI.dll"]

#To Set Names For The Images In Docker
LABEL maintainer="Jason Ishak"
LABEL description="My API and Entity Framework App"

# Set a custom name for the image
LABEL org.opencontainers.image.title="my-api-ef-super-hero-images-app"

# Set a custom name for the container
LABEL org.opencontainers.container.title="my-api-ef-super-hero-container"

