FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["DeskBookingSystem.WebApp/DeskBookingSystem.WebApp.csproj", "DeskBookingSystem.WebApp/"]
RUN dotnet restore "DeskBookingSystem.WebApp/DeskBookingSystem.WebApp.csproj"
COPY . .
WORKDIR "/src/DeskBookingSystem.WebApp"
RUN dotnet build "DeskBookingSystem.WebApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DeskBookingSystem.WebApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DeskBookingSystem.WebApp.dll"]
