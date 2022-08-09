#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["dung.Ecommerce.API/dung.Ecommerce.API.csproj", "dung.Ecommerce.API/"]
RUN dotnet restore "dung.Ecommerce.API/dung.Ecommerce.API.csproj"
COPY . .
WORKDIR "/src/dung.Ecommerce.API"
RUN dotnet build "dung.Ecommerce.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dung.Ecommerce.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dung.Ecommerce.API.dll"]