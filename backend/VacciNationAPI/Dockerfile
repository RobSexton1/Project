FROM mcr.microsoft.com/dotnet/aspnet:5.0-focal AS base
WORKDIR /app
FROM mcr.microsoft.com/dotnet/sdk:5.0-focal AS build
WORKDIR /src
COPY ["VacciNationAPI.csproj", "./"]
RUN dotnet restore "./VacciNationAPI.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "VacciNationAPI.csproj" -c Release -o /app/build
FROM build AS publish
RUN dotnet publish "VacciNationAPI.csproj" -c Release -o /app/publish
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "VacciNationAPI.dll"]