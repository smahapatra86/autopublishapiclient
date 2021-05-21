#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app


FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["SomeServices.csproj", "."]
RUN dotnet restore "./SomeServices.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "SomeServices.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SomeServices.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SomeServices.dll"]