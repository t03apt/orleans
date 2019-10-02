FROM mcr.microsoft.com/dotnet/core/runtime:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 2222
EXPOSE 4000

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY . .
WORKDIR "/src/src/OneBoxDeployment.OrleansHost"
RUN dotnet restore
RUN dotnet build -c Release -o /app --no-restore

FROM build AS publish
RUN dotnet publish -c Release -o /app --no-restore

FROM base AS final
ENV ASPNETCORE_ENVIRONMENT Production
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "OneBoxDeployment.OrleansHost.dll"]