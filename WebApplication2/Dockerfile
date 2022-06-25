#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

#套件還原
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
#等同於 Linux語法 CD src
WORKDIR /src 
#把本機專案的所有檔案複製到容器裡的 src資料夾
COPY . . 
RUN dotnet restore "WebApplication2.csproj"
RUN apt-get install & apt-get update -y 
RUN apt-get install npm -y

#編譯專案
RUN dotnet build "WebApplication2.csproj" -c Release -o /app/build

#部屬專案
FROM build AS publish
RUN dotnet publish "WebApplication2.csproj" -c Release -o /app/publish

FROM base AS final
#等同於 Linux語法 CD app
WORKDIR /app 
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplication2.dll"]