#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Pizzeria/Pizzeria.csproj", "Pizzeria/"]
RUN dotnet restore "Pizzeria/Pizzeria.csproj"
COPY . .
WORKDIR "/src/Pizzeria"
RUN dotnet build "Pizzeria.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Pizzeria.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Pizzeria.dll"]