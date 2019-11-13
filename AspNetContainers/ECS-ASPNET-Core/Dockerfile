FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["ECS-ASPNET-Core/ECS-ASPNET-Core.csproj", "ECS-ASPNET-Core/"]
RUN dotnet restore "ECS-ASPNET-Core/ECS-ASPNET-Core.csproj"
COPY . .
WORKDIR "/src/ECS-ASPNET-Core"
RUN dotnet build "ECS-ASPNET-Core.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ECS-ASPNET-Core.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ECS-ASPNET-Core.dll"]