#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/services/NerdStore.Carrinho.Api/NerdStore.Carrinho.Api.csproj", "src/services/NerdStore.Carrinho.Api/"]
RUN dotnet restore "src/services/NerdStore.Carrinho.Api/NerdStore.Carrinho.Api.csproj"
COPY . .
WORKDIR "/src/src/services/NerdStore.Carrinho.Api"
RUN dotnet build "NerdStore.Carrinho.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "NerdStore.Carrinho.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "NerdStore.Carrinho.Api.dll"]