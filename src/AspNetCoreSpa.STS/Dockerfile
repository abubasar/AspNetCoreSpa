FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app

EXPOSE 5005

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["src/AspNetCoreSpa.STS/AspNetCoreSpa.STS.csproj", "src/AspNetCoreSpa.STS/"]
RUN dotnet restore "src/AspNetCoreSpa.STS/AspNetCoreSpa.STS.csproj"
COPY . .
WORKDIR "/src/src/AspNetCoreSpa.STS"
RUN dotnet build "AspNetCoreSpa.STS.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AspNetCoreSpa.STS.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AspNetCoreSpa.STS.dll"]