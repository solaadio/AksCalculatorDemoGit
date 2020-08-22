FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY *.sln ./
COPY AksCalculator/*.csproj ./AksCalculator/
RUN dotnet restore

# Copy everything else and build
WORKDIR /app/AksCalculator
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /app
COPY --from=build-env ./app/AksCalculator/out .

ENTRYPOINT ["dotnet", "AksCalculator.dll"]