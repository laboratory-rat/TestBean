FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env
WORKDIR /app
EXPOSE 80

# Copy csproj and restore as distinct layers
COPY *.sln ./
COPY BeanTest/BeanTest.csproj BeanTest/
RUN dotnet restore
COPY . .
  
# Copy everything else and build
WORKDIR BeanTest
RUN dotnet publish -c Release -o ./out 

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
WORKDIR /app
COPY --from=build-env /app/BeanTest/out .
ENTRYPOINT ["dotnet", "BeanTest.dll"]