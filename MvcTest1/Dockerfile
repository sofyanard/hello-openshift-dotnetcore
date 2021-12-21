#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["MvcTest1/MvcTest1.csproj", "MvcTest1/"]
RUN dotnet restore "MvcTest1/MvcTest1.csproj"
COPY . .
WORKDIR "/src/MvcTest1"
RUN dotnet build "MvcTest1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MvcTest1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MvcTest1.dll"]