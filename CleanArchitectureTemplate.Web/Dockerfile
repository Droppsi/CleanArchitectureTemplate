FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["CleanArchitectureTemplate.Web/CleanArchitectureTemplate.Web.csproj", "CleanArchitectureTemplate.Web/"]
RUN dotnet restore "CleanArchitectureTemplate.Web/CleanArchitectureTemplate.Web.csproj"
COPY . .
WORKDIR "/src/CleanArchitectureTemplate.Web"
RUN dotnet build "CleanArchitectureTemplate.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CleanArchitectureTemplate.Web.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CleanArchitectureTemplate.Web.dll"]
