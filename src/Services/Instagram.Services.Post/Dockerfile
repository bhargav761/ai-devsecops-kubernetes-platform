FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build

WORKDIR /src

COPY ["Instagram.Services.Post/Instagram.Services.Post.csproj", "Instagram.Services.Post/"]
COPY ["Instagram.Common/Instagram.Common.csproj", "Instagram.Common/"]

RUN dotnet restore "Instagram.Services.Post/Instagram.Services.Post.csproj"

COPY . .

WORKDIR /src/Instagram.Services.Post
RUN dotnet publish "Instagram.Services.Post.csproj" \
    -c Release \
    -o /app/publish \
    --no-restore

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-alpine

RUN apk add --no-cache ffmpeg libgdiplus

WORKDIR /app

COPY --from=build /app/publish .

ENV ASPNETCORE_URLS=http://*:9001
ENV ASPNETCORE_ENVIRONMENT=Production

ENTRYPOINT ["dotnet", "Instagram.Services.Post.dll"]