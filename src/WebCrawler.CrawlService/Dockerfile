FROM mcr.microsoft.com/dotnet/sdk:5.0 AS base
WORKDIR /app

# should be a comma-delimited list
ENV CLUSTER_SEEDS "[]"
ENV CLUSTER_IP ""
ENV CLUSTER_PORT "5213"

#Akka.Remote inbound listening endpoint
EXPOSE 5213 

COPY ./bin/Release/net5/publish/ /app

# Install Petabridge.Cmd client
RUN dotnet tool install --global pbm 

FROM mcr.microsoft.com/dotnet/runtime:5.0 AS app
WORKDIR /app

COPY --from=base /app /app

# copy .NET Core global tool
COPY --from=base /root/.dotnet /root/.dotnet/

# Needed because https://stackoverflow.com/questions/51977474/install-dotnet-core-tool-dockerfile
ENV PATH="${PATH}:/root/.dotnet/tools"

# RUN pbm help

CMD ["dotnet", "WebCrawler.CrawlService.dll"]
