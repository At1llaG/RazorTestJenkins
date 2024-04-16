# Use the official ASP.NET Core runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

# Use the official .NET SDK image for build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy csproj and restore dependencies
COPY ["RazorTest.csproj", "./"]
COPY ["RazorTest.csproj", "./RazorTest/RazorTest.csproj"]
RUN ls -la
RUN echo "15"
COPY . .
COPY . ./RazorTest
RUN ls -la
RUN echo "18"
RUN dotnet restore "RazorTest/RazorTest.csproj"

# Copy the remaining source code
#COPY . .

# Build the application
WORKDIR "/src/RazorTest"
RUN ls -la
RUN echo "27"
RUN dotnet build "RazorTest.csproj" -c Release -o /app/build
RUN ls -la
RUN echo "30"
# Publish the application
FROM build AS publish
RUN dotnet publish "RazorTest.csproj" -c Release -o /app/publish

# Final stage/image
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RazorTest.dll"]

