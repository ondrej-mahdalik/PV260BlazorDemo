FROM mcr.microsoft.com/dotnet/aspnet:9.0-alpine AS base
USER $APP_UID
WORKDIR /app
EXPOSE 8080

FROM mcr.microsoft.com/dotnet/sdk:9.0-alpine AS build
WORKDIR /src

COPY . .
WORKDIR "/PV260Demo.App"

RUN dotnet restore "PV260Demo.App.csproj"
RUN dotnet build "PV260Demo.App.csproj" -c Release -o /build --no-restore

FROM build AS publish
RUN dotnet publish "PV260Demo.App.csproj" -c Release -o /build --no-build /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /publish .
ENTRYPOINT ["dotnet", "PV260Demo.App.dll"]
