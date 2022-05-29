# Weather Walking Skeleton

[Testing an ASP.NET Core Service with xUnit](https://www.jeremywells.io/2020/08/03/weather-walking-skeleton-03.html)

This is a repo for a series of blog posts that walkthroughj building a minimally functional web application using:

- ASP.NET Core
- Angular
- Azure
- (And maybe other technologies along the way).

You can follow this series either on [JeremyWells.io](https://jeremywells.io), [dev.to](https://dev.to/jsheridanwells) or [Medium](https://medium.com/@jsheridanwells_66599)

## SonarCloud Scanning

[Sample SonarCloud Report](https://sonarcloud.io/summary/overall?id=lab18-sonar-scan)

```
brew install openjdk@11
export PATH="/usr/local/opt/openjdk@11/bin:$PATH"
echo 'export PATH="/usr/local/opt/openjdk@11/bin:$PATH"' >> ~/.zshrc
. ~/.zshrc
java --version
dotnet tool install --global dotnet-sonarscanner --version 5.5.3
```

```
export SONAR_TOKEN=<token>
dotnet sonarscanner begin /o:dliu /k:lab18-sonar-scan /d:sonar.host.url=https://sonarcloud.io /v:"1.0" /d:sonar.login=$SONAR_TOKEN /d:sonar.cs.opencover.reportsPaths="**/coverage.opencover.xml" /d:sonar.coverage.exclusions="**Test*.cs" /d:sonar.exclusions="sonar-project.properties, .**/**, **/wwwroot/**, **/TestResults/**, **/obj/**, **/bin/**"
dotnet build --no-incremental
dotnet test /p:CollectCoverage=true /p:CoverletOutputFormat=opencover --collect:"XPlat Code Coverage"
dotnet sonarscanner end /d:sonar.login=$SONAR_TOKEN
```

## Generate Reports

```
dotnet test /p:CollectCoverage=true /p:CoverletOutputFormat=opencover --collect:"XPlat Code Coverage"
dotnet tool install --global dotnet-reportgenerator-globaltool --version 5.1.9
reportgenerator "-reports:./**/coverage.*.xml" -targetdir:"coveragereport" -reporttype:Html
```