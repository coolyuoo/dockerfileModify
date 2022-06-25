#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

#套件還原
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src #等同於 Linux語法 CD src
COPY ["WebApplication2.csproj", ""]
RUN dotnet restore "WebApplication2.csproj"

#編譯專案
COPY . .
RUN dotnet build "WebApplication2.csproj" -c Release -o /app/build

#部屬專案
FROM build AS publish
RUN dotnet publish "WebApplication2.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app #等同於 Linux語法 CD app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplication2.dll"]