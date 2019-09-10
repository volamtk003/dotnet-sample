FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["DMSPro.Sample.Web/DMSPro.Sample.Web.csproj", "DMSPro.Sample.Web/"]
RUN dotnet restore "DMSPro.Sample.Web/DMSPro.Sample.Web.csproj"
COPY . .
WORKDIR "/src/DMSPro.Sample.Web"
RUN dotnet build "DMSPro.Sample.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DMSPro.Sample.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DMSPro.Sample.Web.dll"]