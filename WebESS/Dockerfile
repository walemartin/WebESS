#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["WebESS/WebESS.csproj", "WebESS/"]
RUN dotnet restore "WebESS/WebESS.csproj"
COPY . .
WORKDIR "/src/WebESS"
RUN dotnet build "WebESS.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebESS.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebESS.dll"]