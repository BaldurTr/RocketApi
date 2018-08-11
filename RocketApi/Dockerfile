FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 52383
EXPOSE 44395

FROM microsoft/dotnet:2.1-sdk-nanoserver-1709 AS build
WORKDIR /src
COPY RocketApi/RocketApi.csproj RocketApi/
RUN dotnet restore RocketApi/RocketApi.csproj
COPY . .
WORKDIR /src/RocketApi
RUN dotnet build RocketApi.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish RocketApi.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "RocketApi.dll"]
