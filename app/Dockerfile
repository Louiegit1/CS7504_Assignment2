FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["app/SampleWebApp/SampleWebApp.csproj", "SampleWebApp/"]
RUN dotnet restore "SampleWebApp/SampleWebApp.csproj"
COPY app/SampleWebApp/ SampleWebApp/
WORKDIR "/src/SampleWebApp"
RUN dotnet build "SampleWebApp.csproj" -c Release -o /app/build
RUN dotnet publish "SampleWebApp.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
COPY --from=build /app/publish .
EXPOSE 80
ENTRYPOINT ["dotnet", "SampleWebApp.dll"]
