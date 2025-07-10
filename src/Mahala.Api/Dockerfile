FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["src/Mahala.Api/Mahala.Api.csproj", "Mahala.Api/"]
RUN dotnet restore "Mahala.Api/Mahala.Api.csproj"
COPY . .
WORKDIR "/src/Mahala.Api"
RUN dotnet build "Mahala.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Mahala.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Mahala.Api.dll"]
