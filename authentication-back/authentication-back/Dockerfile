FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 56772
EXPOSE 44377

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY authentication-back/authentication-back.csproj authentication-back/
RUN dotnet restore authentication-back/authentication-back.csproj
COPY . .
WORKDIR /src/authentication-back
RUN dotnet build authentication-back.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish authentication-back.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "authentication-back.dll"]
