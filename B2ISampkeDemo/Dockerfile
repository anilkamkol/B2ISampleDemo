#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["B2ISampkeDemo/B2ISampkeDemo.csproj", "B2ISampkeDemo/"]
RUN dotnet restore "B2ISampkeDemo/B2ISampkeDemo.csproj"
COPY . .
WORKDIR "/src/B2ISampkeDemo"
RUN dotnet build "B2ISampkeDemo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "B2ISampkeDemo.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "B2ISampkeDemo.dll"]