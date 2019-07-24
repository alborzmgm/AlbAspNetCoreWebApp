FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["AlbAspNetCoreWebApp/AlbAspNetCoreWebApp.csproj", "AlbAspNetCoreWebApp/"]
RUN dotnet restore "AlbAspNetCoreWebApp/AlbAspNetCoreWebApp.csproj"
COPY . .
WORKDIR "/src/AlbAspNetCoreWebApp"
RUN dotnet build "AlbAspNetCoreWebApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AlbAspNetCoreWebApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AlbAspNetCoreWebApp.dll"]