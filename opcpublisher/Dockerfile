
FROM mcr.microsoft.com/dotnet/core/sdk:3.1-nanoserver-1809 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY opcpublisher/*.csproj ./opcpublisher/
WORKDIR /app/opcpublisher
RUN dotnet restore

# copy and publish app
WORKDIR /app
COPY opcpublisher/. ./opcpublisher/
WORKDIR /app/opcpublisher
RUN dotnet publish -c Release -o out

# start it up
FROM mcr.microsoft.com/dotnet/core/runtime:3.1-nanoserver-1809 AS runtime
WORKDIR /app
COPY --from=build /app/opcpublisher/out ./
WORKDIR /appdata
ENTRYPOINT ["dotnet", "/app/opcpublisher.dll"]