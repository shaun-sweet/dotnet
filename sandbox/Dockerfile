FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["sandbox/sandbox.csproj", "sandbox/"]
RUN dotnet restore "sandbox/sandbox.csproj"
COPY . .
WORKDIR "/src/sandbox"
RUN dotnet build "sandbox.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "sandbox.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "sandbox.dll"]