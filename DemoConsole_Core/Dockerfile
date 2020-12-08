#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/runtime:3.1-buster-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["DemoConsole_Core/DemoConsole_Core.csproj", "DemoConsole_Core/"]
RUN dotnet restore "DemoConsole_Core/DemoConsole_Core.csproj"
COPY . .
WORKDIR "/src/DemoConsole_Core"
RUN dotnet build "DemoConsole_Core.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DemoConsole_Core.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DemoConsole_Core.dll"]