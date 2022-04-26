FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
WORKDIR /app

# Copy everything
COPY . ./
RUN dotnet --info
RUN dotnet restore examples/Greeter/Client
RUN dotnet publish examples/Greeter/Client -c Release -o out
# RUN dotnet publish --no-restore examples/Container/Backend -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "Client.dll"]