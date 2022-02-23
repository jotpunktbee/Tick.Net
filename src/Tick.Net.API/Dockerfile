FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Tick.Net.API/Tick.Net.API.csproj", "Tick.Net.API/"]
RUN dotnet restore "Tick.Net.API/Tick.Net.API.csproj"
COPY . .
WORKDIR "/src/Tick.Net.API"
RUN dotnet build "Tick.Net.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Tick.Net.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Tick.Net.API.dll"]
