FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["ConsoleApp10/ConsoleApp10.csproj", "ConsoleApp10/"]
RUN dotnet restore "ConsoleApp10/ConsoleApp10.csproj"
COPY . .
WORKDIR "/src/ConsoleApp10"
RUN dotnet build "ConsoleApp10.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ConsoleApp10.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ConsoleApp10.dll"]
