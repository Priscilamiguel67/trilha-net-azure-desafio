# Etapa 1: Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copia o arquivo de projeto e restaura dependências
COPY *.csproj ./
RUN dotnet restore

# Copia o restante do código e faz o build
COPY . ./
RUN dotnet publish -c Release -o /app/publish

# Etapa 2: Runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish .

# Garante que o arquivo do banco SQLite exista
RUN touch /app/funcionarios.db

EXPOSE 8080
ENTRYPOINT ["dotnet", "TrilhaNetAzureDesafio.dll"]
