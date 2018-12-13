#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see http://aka.ms/containercompat 

##FROM microsoft/aspnetcore:2.0-nanoserver-1803 AS base
#from microsoft/aspnetcore-build:2.0 AS base
#WORKDIR /app
#EXPOSE 80
#
#FROM microsoft/aspnetcore-build:2.0-nanoserver-1803 AS build
#WORKDIR /src
#COPY ConferenceApp/ConferenceApp.csproj ConferenceApp/
#RUN dotnet restore ConferenceApp/ConferenceApp.csproj
#COPY . .
#WORKDIR /src/ConferenceApp
#RUN dotnet build ConferenceApp.csproj -c Release -o /app
#
#FROM build AS publish
#RUN dotnet publish ConferenceApp.csproj -c Release -o /app
#
##FROM base AS final
#FROM microsoft/aspnetcore:2.0
#WORKDIR /app
#COPY --from=publish /app .
#ENTRYPOINT ["dotnet", "ConferenceApp.dll"]
#



FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /build
COPY ConferenceApp/ConferenceApp.csproj ConferenceApp/
RUN dotnet restore ConferenceApp/ConferenceApp.csproj
COPY . .
WORKDIR /build/ConferenceApp
#RUN dotnet restore
RUN dotnet build ConferenceApp.csproj -c Release -o output
RUN dotnet publish ConferenceApp.csproj -c Release -o output

FROM microsoft/aspnetcore:2.0
WORKDIR /app
COPY --from=build /build/output . 
ENTRYPOINT ["dotnet", "ConferenceApp.dll"]