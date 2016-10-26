# escape=` (backtick)
FROM microsoft/nanoserver
MAINTAINER oconnormi

RUN powershell -Command `
    $ErrorActionPreference = 'Stop' ; `
    $progressPreference = 'silentlyContinue' ; `
    Invoke-WebRequest -UseBasicParsing -UseDefaultCredentials`
      -OutFile "$env:TEMP\\jdk.msi" `
      https://developers.redhat.com/download-manager/file/java-1.8.0-openjdk-1.8.0.111-1.b15.redhat.windows.x86_64.msi ;

RUN powershell -Command `
    $ErrorActionPreference = 'Stop' ; `
    $progressPreference = 'silentlyContinue' ; `
    Start-Process -FilePath $env:TEMP\jdk.msi ; `
    Remove-Item $env:TEMP\jdk.msi ;
