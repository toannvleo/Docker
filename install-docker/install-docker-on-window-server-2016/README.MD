# Hướng dẫn cài đặt `DockerEE` trên Windows Server

## Cài đặt trên win `Windows Server 2016`

- Bước 1: Điều chỉnh giao thức bảo mật `Tls12`

```
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
```
- Bước 2: Cài đặt gói NuGet

```
Install-PackageProvider -Name NuGet
```

- Bước 2: Download và cài đặt docker ee

    ```
    Install-Module DockerMsftProvider -Force
    Install-Package -Name Docker -ProviderName DockerMsftProvider -Force

    Hoặc cài đặt version mong muốn
    (Install-Package -Name Docker -ProviderName DockerMsftProvider -Force -RequiredVersion 17.06.2-ee-5)
    ```

- Check Package

```
Get-PackageProvider -ListAvailable
Get-PackageSource -ProviderName DockerMsftProvider
Get-Package -Name Docker -ProviderName DockerMsftProvider

[Environment]::SetEnvironmentVariable("LCOW_SUPPORTED", "1", "Machine")
[Environment]::SetEnvironmentVariable("LCOW_SUPPORTED", "$null", "Machine")
```

Invoke-WebRequest "https://github.com/docker/compose/releases/download/v2.9.0/docker-compose-Windows-x86_64.exe" -UseBasicParsing -OutFile $Env:ProgramFiles\Docker\docker-compose.exe


```
Docker issue – ERROR: failed during hnsCallRawResponse: hnsCall failed in Win32: The system cannot find the path specified. (0x3)


ocker: Error response from daemon: hcsshim::CreateComputeSystem feaacdf87faf0486cbb7ed256d751c8e416a592092b9c5bde6c70672539d5479: The system cannot find the path specified.
```
Stop-Service docker
Stop-service hns
Start-service hns
Start-Service docker
docker network prune