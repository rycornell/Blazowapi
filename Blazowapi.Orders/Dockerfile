FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["Blazowapi.Orders/Blazowapi.Orders.csproj", "Blazowapi.Orders/"]
RUN dotnet restore "Blazowapi.Orders/Blazowapi.Orders.csproj"
COPY . .
WORKDIR "/src/Blazowapi.Orders"
RUN dotnet build "Blazowapi.Orders.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Blazowapi.Orders.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Blazowapi.Orders.dll"]