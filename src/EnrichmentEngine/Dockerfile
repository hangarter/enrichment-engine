# Use the .NET 7 SDK image to build the app
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /app

# Copy the project file and restore any dependencies (via NuGet)
COPY *.csproj .
RUN dotnet restore

# Copy the rest of the app
COPY . .

# Publish the app to the /app/out directory
RUN dotnet publish -c Release -o out

# Use the .NET 7 runtime image to run the app
FROM mcr.microsoft.com/dotnet/runtime:7.0 AS runtime
WORKDIR /app
COPY --from=build /app/out ./

# Run the app
ENTRYPOINT ["dotnet", "EnrichmentEngine.dll"]
