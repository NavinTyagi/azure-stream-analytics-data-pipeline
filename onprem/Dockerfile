FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
RUN apt-get update
RUN apt-get install -y git
RUN git clone --recursive https://github.com/NavinTyagi/azure-stream-analytics-data-pipeline.git  &&  cd azure-stream-analytics-data-pipeline && git fetch && git checkout master
WORKDIR azure-stream-analytics-data-pipeline/onprem/DataLoader
RUN dotnet build -c Release
RUN dotnet publish -f netcoreapp3.1 -c Release


FROM mcr.microsoft.com/dotnet/core/runtime:3.1 AS runtime
WORKDIR DataLoader
COPY --from=build azure-stream-analytics-data-pipeline/onprem/DataLoader/bin/Release/netcoreapp2.0/publish .
ENTRYPOINT ["dotnet" , "taxi.dll"]
