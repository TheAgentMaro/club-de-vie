# Étape de build
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app

# Copier les fichiers csproj et restaurer les dépendances
COPY backend/*.sln .
COPY backend/ClubDeVie.Api/*.csproj ./ClubDeVie.Api/
COPY backend/ClubDeVie.Domain/*.csproj ./ClubDeVie.Domain/
COPY backend/ClubDeVie.Infrastructure/*.csproj ./ClubDeVie.Infrastructure/
RUN dotnet restore

# Copier le reste des fichiers et construire le projet
COPY backend/. ./backend/
WORKDIR /app/backend/ClubDeVie.Api
RUN dotnet publish -c Release -o out

# Étape de runtime
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS runtime
WORKDIR /app
COPY --from=build /app/backend/ClubDeVie.Api/out ./
ENTRYPOINT ["dotnet", "ClubDeVie.Api.dll"]
