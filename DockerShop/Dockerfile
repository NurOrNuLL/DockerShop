FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app

EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DockerShop/DockerShop.csproj", "DockerShop/"]
RUN dotnet restore "DockerShop/DockerShop.csproj"
COPY . .
WORKDIR "/src/DockerShop"
RUN dotnet build "DockerShop.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DockerShop.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DockerShop.dll"]
