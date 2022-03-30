#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 8080
 

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["LCMTLCB1.WebAPI.Solution/LCMTLCB1.WebAPI.Solution.csproj", "LCMTLCB1.WebAPI.Solution/"]
RUN dotnet restore "LCMTLCB1.WebAPI.Solution/LCMTLCB1.WebAPI.Solution.csproj"
COPY . .
WORKDIR "/src/LCMTLCB1.WebAPI.Solution"
RUN dotnet build "LCMTLCB1.WebAPI.Solution.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "LCMTLCB1.WebAPI.Solution.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "LCMTLCB1.WebAPI.Solution.dll"]