# Stage 1: Build Stage
# Use the official .NET SDK image to build the application
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

# Set the working directory inside the container
WORKDIR /dotnet_build

# Copy all files from the host machine into the container
COPY . .

# Restore dependencies, build the app, and publish it to the 'publish' folder
RUN dotnet restore && \
    dotnet build --configuration Release && \
    dotnet publish --configuration Release --output ./publish

# Stage 2: Runtime Stage
# Use a smaller runtime-only image to reduce final image size and improve performance
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS deploy

# Set the working directory inside the container
WORKDIR /dotnet_artifects

# Copy published output from the build stage to the runtime container
COPY --from=build /dotnet_build/publish .

# Set the entry point for the container to start the application
ENTRYPOINT ["dotnet", "ElearnBackend.dll"]

