FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/PicCard.Recommendation.Api/PicCard.Recommendation.Api.csproj", "src/PicCard.Recommendation.Api/"]
RUN dotnet restore "src/PicCard.Recommendation.Api/PicCard.Recommendation.Api.csproj"
COPY . .
WORKDIR "/src/src/PicCard.Recommendation.Api"
RUN dotnet build "PicCard.Recommendation.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PicCard.Recommendation.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PicCard.Recommendation.Api.dll"]