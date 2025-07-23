FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build

WORKDIR /src

COPY . .

RUN dotnet restore ./backend.api/backend.api.csproj
RUN dotnet publish ./backend.api/backend.api.csproj -c Release -o /app --no-restore

FROM mcr.microsoft.com/dotnet/aspnet:9.0

WORKDIR /app
COPY --from=build /app .

EXPOSE 8080

CMD ["dotnet", "backend.api.dll"]