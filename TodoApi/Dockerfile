# PHASE 1 : Image de base pour l'exécution
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
# Utilise l'image officielle .NET 8.0 ASP.NET Runtime

USER app
# Définit l'utilisateur non-root 'app' pour plus de sécurité

WORKDIR /app
# Définit le répertoire de travail dans le conteneur

EXPOSE 8080
EXPOSE 8081
# Expose les ports pour l'application web et HTTPS

# PHASE 2 : Construction de l'application
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
# Utilise l'image SDK .NET 8.0 pour la compilation

ARG BUILD_CONFIGURATION=Release
# Définit une variable pour la configuration de build (Debug/Release)

WORKDIR /src
# Crée et se positionne dans le répertoire source

COPY ["TodoApi/TodoApi.csproj", "TodoApi/"]
# Copie uniquement le fichier projet d'abord (pour optimiser le cache Docker)

RUN dotnet restore "./TodoApi/TodoApi.csproj"
# Restaure les dépendances NuGet

COPY . .
# Copie tout le reste du code source

WORKDIR "/src/TodoApi"
# Se positionne dans le répertoire du projet

RUN dotnet build "./TodoApi.csproj" -c $BUILD_CONFIGURATION -o /app/build
# Compile l'application

# PHASE 3 : Publication
FROM build AS publish
ARG BUILD_CONFIGURATION=Release
# Hérite de l'étape build et configure la publication

RUN dotnet publish "./TodoApi.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false
# Publie l'application en mode Release

# PHASE 4 : Image finale
FROM base AS final
# Repart de l'image de base légère

WORKDIR /app
# Définit le répertoire de travail

COPY --from=publish /app/publish .
# Copie les fichiers publiés depuis l'étape de publication

ENTRYPOINT ["dotnet", "TodoApi.dll"]
# Définit la commande de démarrage de l'application