# escape=`
FROM mssql-developer:2017-windowsservercore-ltsc2019

ENV ACCEPT_EULA='Y' `
    sa_password='HASH-epsom-sunset-cost7!' `
    DB_PREFIX='sc' `
    INSTALL_PATH='c:/install/' `
    DATA_PATH='c:/data/'

COPY . ${INSTALL_PATH}

RUN New-Item -Path $env:DATA_PATH -ItemType Directory | Out-Null; `
    & (Join-Path $env:INSTALL_PATH "\\Extract-Databases.ps1") -Path $env:INSTALL_PATH; `
    & (Join-Path $env:INSTALL_PATH "\\Install-Databases.ps1") -InstallPath $env:INSTALL_PATH -DataPath $env:DATA_PATH -DatabasePrefix $env:DB_PREFIX; `
    Copy-Item -Path (Join-Path $env:INSTALL_PATH "\\Boot.ps1") -Destination 'C:\\'; `
    Get-ChildItem -Path $env:INSTALL_PATH -Exclude "*.mdf", "*.ldf" | Remove-Item -Force;

CMD C:/Boot.ps1 -InstallPath $env:INSTALL_PATH -DataPath $env:DATA_PATH