#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["CQRS_MediatR/CQRS_MediatR.csproj", "CQRS_MediatR/"]
RUN dotnet restore "CQRS_MediatR/CQRS_MediatR.csproj"
COPY . .
WORKDIR "/src/CQRS_MediatR"
RUN dotnet build "CQRS_MediatR.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CQRS_MediatR.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CQRS_MediatR.dll"]