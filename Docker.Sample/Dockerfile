FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 53407
EXPOSE 44365

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY Docker.Sample/Docker.Sample.csproj Docker.Sample/
RUN dotnet restore Docker.Sample/Docker.Sample.csproj
COPY . .
WORKDIR /src/Docker.Sample
RUN dotnet build Docker.Sample.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Docker.Sample.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Docker.Sample.dll"]
