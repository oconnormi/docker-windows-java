# escape=` (backtick)
FROM microsoft/nanoserver
MAINTAINER oconnormi

# ENV JAVA_VERSION_MAJOR=8 `
#     JAVA_VERSION_MINOR=102 `
#     JAVA_VERSION_BUILD=14 `
#     JAVA_PACKAGE=jdk `
#     JAVA_JCE=standard `
#     # JAVA_HOME=/jdk `
#     # PATH=${PATH}:Program Files/Java/jdk/bin \
#     LANG=C.UTF-8

RUN powershell -Command `
    $ErrorActionPreference = 'Stop' ; `
    $progressPreference = 'silentlyContinue' ; `
    Invoke-WebRequest 'http://www.oracle.com/' -UseBasicParsing -UseDefaultCredentials -SessionVariable session ; `
    $secureBackupCookie = New-Object System.Net.Cookie('oraclelicense', 'accept-securebackup-cookie', '/', '.oracle.com') ; `
    $gpwCookie = New-Object System.Net.Cookie('gpw_e24', 'http%3A%2F%2Fwww.oracle.com%2F') ; `
    $session.Cookies.Add('http://www.oracle.com/', $secureBackupCookie) ; `
    $session.Cookies.Add('http://www.oracle.com', $gpwCookie) ; `
    Invoke-WebRequest http://download.oracle.com/otn-pub/java/jdk/8u112-b14/jdk-8u112-windows-x64.exe -UseDefaultCredentials -WebSession $session -OutFile "$env:TEMP\jdk.exe" -UseBasicParsing ; `
    Start-Process -FilePath $env:TEMP\jdk.exe -PassThru -Wait -ArgumentList "/s, ADDLOCAL='ToolsFeature,PublicjreFeature'" ; `
    Remove-Item $env:TEMP\jdk.exe -Force

CMD java --version
