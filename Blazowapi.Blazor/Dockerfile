FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["Blazowapi.Blazor/Blazowapi.Blazor.csproj", "Blazowapi.Blazor/"]
RUN dotnet restore "Blazowapi.Blazor/Blazowapi.Blazor.csproj"
COPY . .
WORKDIR "/src/Blazowapi.Blazor"
RUN dotnet build "Blazowapi.Blazor.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Blazowapi.Blazor.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Blazowapi.Blazor.dll"]