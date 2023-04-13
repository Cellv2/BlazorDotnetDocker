# Watcher tests:
# FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
# WORKDIR /app
# EXPOSE 5253
# EXPOSE 7253

# FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
# WORKDIR /src
# COPY ["PocExternalDockerDotnet.csproj", "PocExternalDockerDotnet/"]
# RUN dotnet restore "PocExternalDockerDotnet/PocExternalDockerDotnet.csproj"


# WORKDIR /src/PocExternalDockerDotnet
# COPY . .
# # RUN dotnet build "PocExternalDockerDotnet.csproj" -c Debug -o /out

# RUN dotnet dev-certs https --trust
# ENTRYPOINT ["dotnet", "watch", "run"]


# do the below if you want to actually run it statically
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["PocExternalDockerDotnet.csproj", "."]
RUN dotnet restore "PocExternalDockerDotnet.csproj"

COPY . .
RUN dotnet build "PocExternalDockerDotnet.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PocExternalDockerDotnet.csproj" -c Release -o /app/publish

# FROM base AS final
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .

ENTRYPOINT ["dotnet", "PocExternalDockerDotnet.dll"]