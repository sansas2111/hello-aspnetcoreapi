FROM mcr.microsoft.com/dotnet/aspnet:6.0-focal AS base
WORKDIR /app
EXPOSE 80

ENV ASPNETCORE_URLS=http://+:80

FROM mcr.microsoft.com/dotnet/sdk:6.0-focal AS build
WORKDIR /src
COPY ["HelloASPNetCore.csproj", "./"]
RUN dotnet restore "./HelloASPNetCore.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "HelloASPNetCore.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "HelloASPNetCore.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "HelloASPNetCore.dll"]
