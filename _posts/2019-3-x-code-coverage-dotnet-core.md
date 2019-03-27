

TOPDIR=$(pwd) 
rm -rf coverage || true
cd src/SalesImportApi.Tests 
dotnet restore -s $NEXUS_NUGET_URL -s $PUBLIC_NUGET_URL
dotnet test /p:AltCover=true /p:AltCoverXmlreport=".\coverage.xml" /p:AltCoverAssemblyFilter="NUnit|sales-import-api-tests" /p:AltCoverThreshold=60 /p:AltCoverAttributeFilter="ExcludeFromCodeCoverage"
cd $TOPDIR 
reportgenerator -reports:src/SalesImportApi.Tests/coverage.xml -targetdir:./coverage


https://github.com/SteveGilham/altcover/wiki/Usage

AltCover is a NuGet package but it's also available as .NET Core Global Tool which is awesome.

dotnet tool install --global altcover.global
This makes "altcover" a command that's available everywhere without adding it to my project.

That said, I'm going to follow the AltCover Quick Start and see how quickly I can get it set up!

I'll Install into my test project hanselminutes.core.tests

dotnet add package AltCover
and then run

dotnet test /p:AltCover=true
90.1% Line Coverage, 71.4% Branch CoverageCool. My tests run as usual, but now I've got a coverage.xml in my test folder. I could also generate LCov or Cobertura reports if I'd like. At this point my coverage.xml is nearly a half-meg! That's a lot of good information, but how do I see  the results in a human readable format?

This is the OpenCover XML format and I can run ReportGenerator on the coverage file and get a whole bunch of HTML files. Basically an entire coverage mini website!

I downloaded ReportGenerator and put it in its own folder (this would be ideal as a .NET Core global tool).

c:\ReportGenerator\ReportGenerator.exe -reports:coverage.xml -targetdir:./coverage
Make sure you use a decent targetDir otherwise you might end up with dozens of HTML files littered in your project folder. You might also consider .gitignoring the resulting folder and coverage file. Open up index.htm and check out all this great information!