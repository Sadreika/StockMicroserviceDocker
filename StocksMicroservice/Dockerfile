FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["StocksMicroservice/StocksMicroservice.csproj", "StocksMicroservice/"]
COPY ["Domain/Domain.csproj", "Domain/"]
COPY ["Repositories/Repositories.csproj", "Repositories/"]
RUN dotnet restore "StocksMicroservice/StocksMicroservice.csproj"
COPY . .
WORKDIR "/src/StocksMicroservice"
RUN dotnet build "StocksMicroservice.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "StocksMicroservice.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "StocksMicroservice.dll"]