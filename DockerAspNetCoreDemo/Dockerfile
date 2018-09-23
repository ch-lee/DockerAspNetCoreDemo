FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY DockerAspNetCoreDemo/DockerAspNetCoreDemo.csproj DockerAspNetCoreDemo/
RUN dotnet restore DockerAspNetCoreDemo/DockerAspNetCoreDemo.csproj
COPY . .
WORKDIR /src/DockerAspNetCoreDemo
RUN dotnet build DockerAspNetCoreDemo.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish DockerAspNetCoreDemo.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerAspNetCoreDemo.dll"]
