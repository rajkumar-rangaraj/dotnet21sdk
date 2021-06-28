#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["netcoreapp21test/netcoreapp21test.csproj", "netcoreapp21test/"]
RUN dotnet restore "netcoreapp21test/netcoreapp21test.csproj"
COPY . .
WORKDIR "/src/netcoreapp21test"
RUN dotnet build "netcoreapp21test.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "netcoreapp21test.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "netcoreapp21test.dll"]