FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["PucCoins/PucCoins.csproj", "PucCoins/"]
RUN dotnet restore "PucCoins/PucCoins.csproj"
COPY . .
WORKDIR "/src/PucCoins"
RUN dotnet build "PucCoins.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "PucCoins.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "PucCoins.dll"]