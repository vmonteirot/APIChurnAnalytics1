# Usando a imagem .NET SDK como ambiente de build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-env
WORKDIR /app

# Copiando o csproj e restaurando como camada distinta
COPY *.csproj ./
RUN dotnet restore

# Copiando o projeto e dando build na aplicação
COPY . ./
RUN dotnet publish -c Release -o out

# Dando build na imagem runtime
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build-env /app/out .

# Expondo a porta em que o projeto vai rodar
EXPOSE 80

# Setando o entry point para rodar a aplicação
ENTRYPOINT ["dotnet", "ChallengeChurnAnalytics.dll"]
