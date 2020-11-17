FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster As build
WORKDIR /src
COPY ["ContosoUniversity/ContosoUniversity.csproj", "ContosoUniversity/"]
RUN dotnet restore "ContosoUniversity/ContosoUniversity.csproj"
COPY . .
WORKDIR "/src/ContosoUniversity"
RUN dotnet build "ContosoUniversity.csproj" -c Release -o /app/build
FROM build As publish
RUN dotnet publish "ContosoUniversity.csproj" -c Release -o /app/publish

FROM base As final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ContosoUniversity.dll"]