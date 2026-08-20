FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build

WORKDIR /src

COPY ["Instagram.Services.Newsfeed/Instagram.Services.Newsfeed.csproj", "Instagram.Services.Newsfeed/"]
COPY ["Instagram.Common/Instagram.Common.csproj", "Instagram.Common/"]

RUN dotnet restore "Instagram.Services.Newsfeed/Instagram.Services.Newsfeed.csproj"

COPY . .

WORKDIR /src/Instagram.Services.Newsfeed
RUN dotnet publish "Instagram.Services.Newsfeed.csproj" \
    -c Release \
    -o /app/publish \
    --no-restore

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-alpine

WORKDIR /app

COPY --from=build /app/publish .

ENV ASPNETCORE_URLS=http://*:9002
ENV ASPNETCORE_ENVIRONMENT=Production

ENTRYPOINT ["dotnet", "Instagram.Services.Newsfeed.dll"]