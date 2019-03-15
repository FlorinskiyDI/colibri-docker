FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 55360
EXPOSE 44350

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY src/Services/Identity/Identity.API/Identity.API.csproj src/Services/Identity/Identity.API/
RUN dotnet restore src/Services/Identity/Identity.API/Identity.API.csproj
COPY . .
WORKDIR /src/src/Services/Identity/Identity.API
RUN dotnet build Identity.API.csproj -c Release -o /app

FROM build as unittest
RUN dotnet test --verbosity=normal --results-directory /TestResults/ --logger "trx;LogFileName=test_results.xml" /src/src/Services/Identity/Identity.UnitTests/Identity.UnitTests.csproj

FROM build AS publish
RUN dotnet publish Identity.API.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Identity.API.dll"]
