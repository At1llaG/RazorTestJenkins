# Use the official ASP.NET Core runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 6002

# Use the official .NET SDK image for build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy csproj and restore dependencies
COPY ["RazorTest.csproj", "./"]
COPY ["RazorTest.csproj", "./RazorTest"]
RUN dotnet restore "RazorTest.csproj"

# Copy the remaining source code
COPY . .

# Build the application
WORKDIR "/src/RazorTest"
RUN dotnet build "RazorTest.csproj" -c Release -o /app/build

# Publish the application
FROM build AS publish
RUN dotnet publish "RazorTest.csproj" -c Release -o /app/publish

# Final stage/image
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RazorTest.dll"]
