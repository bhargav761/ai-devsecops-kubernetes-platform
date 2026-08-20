FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build

WORKDIR /src

COPY ["Instagram.Services.User/Instagram.Services.User.csproj", "Instagram.Services.User/"]
COPY ["Instagram.Common/Instagram.Common.csproj", "Instagram.Common/"]

RUN dotnet restore "Instagram.Services.User/Instagram.Services.User.csproj"

COPY . .

WORKDIR /src/Instagram.Services.User
RUN dotnet publish "Instagram.Services.User.csproj" \
    -c Release \
    -o /app/publish \
    --no-restore

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-alpine

WORKDIR /app

COPY --from=build /app/publish .

ENV ASPNETCORE_URLS=http://*:9000
ENV ASPNETCORE_ENVIRONMENT=Production

ENTRYPOINT ["dotnet", "Instagram.Services.User.dll"]