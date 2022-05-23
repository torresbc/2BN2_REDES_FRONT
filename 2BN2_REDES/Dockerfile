#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["2BN2_REDES/2BN2_REDES.csproj", "2BN2_REDES/"]
RUN dotnet restore "2BN2_REDES/2BN2_REDES.csproj"
COPY . .
WORKDIR "/src/2BN2_REDES"
RUN dotnet build "2BN2_REDES.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "2BN2_REDES.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "2BN2_REDES.dll"]