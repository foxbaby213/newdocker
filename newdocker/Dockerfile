FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["newdocker.csproj", "newdocker/"]
RUN dotnet restore "newdocker/newdocker.csproj"
WORKDIR "/src/newdocker"
COPY . .
RUN dotnet build "newdocker.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "newdocker.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "newdocker.dll"]