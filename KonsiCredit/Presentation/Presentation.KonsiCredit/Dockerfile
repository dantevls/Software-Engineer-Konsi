﻿FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
ENV ASPNETCORE_URLS=http://+:5030/
WORKDIR /app
EXPOSE 5030
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Presentation/Presentation.KonsiCredit/Presentation.KonsiCredit.csproj", "Presentation/Presentation.KonsiCredit/"]
COPY ["Application/Application.KonsiCredit/Application.KonsiCredit.csproj", "Application/Application.KonsiCredit/"]
COPY ["Domain/Domain.KonsiCredit/Domain.KonsiCredit.csproj", "Domain/Domain.KonsiCredit/"]
COPY ["Infra/CrossCutting/Infra.CrossCutting.KonsiCredit/Infra.CrossCutting.KonsiCredit.csproj", "Infra/CrossCutting/Infra.CrossCutting.KonsiCredit/"]
COPY ["Infra/Data/Infra.Data.KonsiCredit/Infra.Data.KonsiCredit.csproj", "Infra/Data/Infra.Data.KonsiCredit/"]
COPY ["Services/Services.KonsiCredit/Services.KonsiCredit.csproj", "Services/Services.KonsiCredit/"]
RUN dotnet restore "Presentation/Presentation.KonsiCredit/Presentation.KonsiCredit.csproj"
COPY . .
WORKDIR "/src/Presentation/Presentation.KonsiCredit"
#RUN dotnet build "Presentation.KonsiCredit.csproj" -c Release -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "Presentation.KonsiCredit.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Presentation.KonsiCredit.dll"]