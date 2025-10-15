
# Etapa de build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copia o arquivo .csproj e restaura dependências
COPY *.csproj ./
RUN dotnet restore

# Copia o restante do código e publica
COPY . ./
RUN dotnet publish -c Release -o /app/publish

# Etapa de runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app

# Copia os arquivos publicados do build
COPY --from=build /app/publish .

# Expõe a porta da aplicação
EXPOSE 8080

# Comando para iniciar a API
ENTRYPOINT ["dotnet", "TrilhaNetAzureDesafio.csproj"]
