FROM mcr.microsoft.com/dotnet/runtime:3.1 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["api/extensions.csproj", "api/"]
RUN dotnet restore "api\extensions.csproj"
COPY . .
WORKDIR "/src/api"
RUN dotnet build "extensions.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "extensions.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "extensions.dll"]
