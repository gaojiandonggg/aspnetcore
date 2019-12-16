FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY ["aspnetcore2.0/aspnetcore2.0.csproj", "aspnetcore2.0/"]
RUN dotnet restore "aspnetcore2.0/aspnetcore2.0.csproj"
COPY . .
WORKDIR "/src/aspnetcore2.0"
RUN dotnet build "aspnetcore2.0.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "aspnetcore2.0.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "aspnetcore2.0.dll"]