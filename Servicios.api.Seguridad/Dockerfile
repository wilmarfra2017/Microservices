# Etapa base
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

CMD echo "Ruta: " && ls

# Etapa de construcción
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src

COPY . /src/Servicios.api.Seguridad/
RUN dotnet restore "Servicios.api.Seguridad/Servicios.api.Seguridad.csproj"

RUN dotnet build "Servicios.api.Seguridad/Servicios.api.Seguridad.csproj" -c $BUILD_CONFIGURATION -o /app/build

# Etapa de publicación
FROM build AS publish
RUN dotnet publish "Servicios.api.Seguridad/Servicios.api.Seguridad.csproj" -c $BUILD_CONFIGURATION -o /app/publish

# Etapa final
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Servicios.api.Seguridad.dll"]
