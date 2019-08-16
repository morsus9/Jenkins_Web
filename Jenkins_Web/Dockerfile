FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Jenkins_Web/Jenkins_Web.csproj", "Jenkins_Web/"]
RUN dotnet restore "Jenkins_Web/Jenkins_Web.csproj"
COPY . .
WORKDIR "/src/Jenkins_Web"
RUN dotnet build "Jenkins_Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Jenkins_Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Jenkins_Web.dll"]
