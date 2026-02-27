FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 8080

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["CicdDemo.Api/CicdDemo.Api.csproj", "CicdDemo.Api/"]
RUN dotnet restore "CicdDemo.Api/CicdDemo.Api.csproj"
COPY . .
WORKDIR "/src/CicdDemo.Api"
RUN dotnet build "CicdDemo.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CicdDemo.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CicdDemo.Api.dll"]
