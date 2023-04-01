FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["UI/Parties.Server/Parties.Server.csproj", "UI/Parties.Server/"]
RUN dotnet restore "UI/Parties.Server/Parties.Server.csproj"
COPY . .
WORKDIR "/src/UI/Parties.Server"
RUN dotnet build "Parties.Server.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Parties.Server.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Parties.Server.dll"]
