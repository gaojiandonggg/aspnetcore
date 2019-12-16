FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["aspnetcore2.0/aspnetcore2.0.csproj", "aspnetcore2.0/"]
RUN dotnet restore "aspnetcore2.0/aspnetcore2.0.csproj"
COPY . .
WORKDIR "/src/aspnetcore2.0"
RUN dotnet build "aspnetcore2.0.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "aspnetcore2.0.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "aspnetcore2.0.dll"]