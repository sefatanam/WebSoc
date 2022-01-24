FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["WebSoc/WebSoc.csproj", "WebSoc/"]
RUN dotnet restore "WebSoc/WebSoc.csproj"
COPY . .
WORKDIR "/src/WebSoc"
RUN dotnet build "WebSoc.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebSoc.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebSoc.dll"]
