FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["SimpleApiGateway/SimpleApiGateway.csproj", "SimpleApiGateway/"]
RUN dotnet restore "SimpleApiGateway/SimpleApiGateway.csproj"
COPY . .
WORKDIR "/src/SimpleApiGateway"
RUN dotnet build "SimpleApiGateway.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SimpleApiGateway.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SimpleApiGateway.dll"]
