#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:3.1 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["HelloWorldPrj/HelloWorldPrj.csproj", "HelloWorldPrj/"]
RUN dotnet restore "HelloWorldPrj/HelloWorldPrj.csproj"
COPY . .
WORKDIR "/src/HelloWorldPrj"
RUN dotnet build "HelloWorldPrj.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HelloWorldPrj.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HelloWorldPrj.dll"]