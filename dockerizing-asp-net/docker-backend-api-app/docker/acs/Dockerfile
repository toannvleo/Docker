FROM toannvleo/aspnet-backend:4.6.2

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# Copy oracle client file conection
COPY tnsnames.ora c:/oracle/network/admin/


# Set working directory
WORKDIR c:/app/backend/acs

# Remove default web server and create a new web server
RUN Remove-Website -Name 'Default Web Site'; \
    New-Website -Name 'acs' -Port 80 -PhysicalPath "C:\app\backend\acs"  -ApplicationPool '.NET v4.5';  \
    New-WebApplication -Name 'acs' -Site 'acs' -PhysicalPath "C:\app\backend\acs"