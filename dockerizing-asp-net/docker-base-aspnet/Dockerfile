FROM mcr.microsoft.com/dotnet/framework/aspnet:4.6.2-20220809-windowsservercore-ltsc2016

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

ENV CHOCO_URL=https://chocolatey.org/install.ps1

RUN [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.SecurityProtocolType]::Tls12; \
	Set-ExecutionPolicy Bypass -Scope Process -Force; \
    iex ((New-Object System.Net.WebClient).DownloadString("$env:CHOCO_URL"));

# Install Microsoft Visual C++ Redistributable (used by oracle client) via chocolatey
RUN ["choco", "install", "vcredist2010", "-y", "--allow-empty-checksums"]

# Set working directory
COPY ODAC121024Xcopy_x64.zip c:/install/oracle_client.zip

# Extract oracle client file .zip
RUN "expand-archive -Path 'c:\install\oracle_client.zip' -DestinationPath 'c:\install\oracleInstall'"

# Set working directory
WORKDIR c:/install/oracleInstall

# Install Oracle Client
RUN ".\install.bat odp.net4 c:\oracle odac true;"

# fix - error 0175: The specified store provider cannot be found in the configuration, or is not valid.
WORKDIR c:/Oracle/ODP.NET/bin/4
RUN ./oraprovcfg.exe /action:config /product:odp /frameworkversion:v4.0.30319 /providerpath:C:\Oracle\ODP.NET\bin\4\Oracle.DataAccess.dll

# Set path to oracle client
RUN "[Environment]::SetEnvironmentVariable(\"Path\", $env:Path + \";C:\\oracle\\\", [EnvironmentVariableTarget]::Machine)"

RUN Remove-Item -Recurse C:\install\oracle_client.zip;

WORKDIR c:/