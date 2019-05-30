FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["BeanTest/BeanTest.csproj", "BeanTest/"]
RUN dotnet restore "BeanTest/BeanTest.csproj"
COPY . .
WORKDIR "/src/BeanTest"
RUN dotnet build "BeanTest.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "BeanTest.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "BeanTest.dll"]