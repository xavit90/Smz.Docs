**Guía Estándar: Verificación y Preparación del Entorno para Aplicaciones ASP.NET Core 3.1 en IIS**

---

## 1. Requisitos Previos

Antes de comenzar, asegúrese de contar con:

* Sistema operativo Windows Server o Windows 10/11
* Internet para descargas necesarias
* Acceso como administrador
* IIS instalado y habilitado

---

## 2. Instalación del Hosting Bundle de .NET Core 3.1

### 2.1 Descargar el Hosting Bundle

1. Visite el sitio oficial de .NET:
   [https://dotnet.microsoft.com/en-us/download/dotnet/3.1](https://dotnet.microsoft.com/en-us/download/dotnet/3.1)

2. Busque la sección correspondiente a **.NET Core 3.1 Runtime** y descargue el **Hosting Bundle** (ejemplo: `dotnet-hosting-3.1.32-win.exe`).

### 2.2 Ejecutar el instalador

* Ejecute el archivo descargado como administrador.
* Asegúrese de que estén seleccionadas las opciones para instalar el runtime y el módulo de IIS.
* Finalice la instalación.

### 2.3 Reiniciar IIS

Abra una terminal con privilegios de administrador y ejecute:

```powershell
iisreset
```

---

## 3. Verificación del Entorno

### 3.1 Verificar runtimes instalados

Ejecute en consola:

```powershell
dotnet --list-runtimes
```

Verifique que estén instalados:

* `Microsoft.AspNetCore.App 3.1.x`
* `Microsoft.NETCore.App 3.1.x`

### 3.2 Verificar el Hosting Bundle en el registro

```powershell
Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\AspNetCore\HostingBundle"
```

Salida esperada:

```
Version    : 3.1.32
InstallPath: C:\Program Files\dotnet\
```

### 3.3 Verificar el módulo AspNetCoreModuleV2 en IIS

```powershell
Get-WebGlobalModule -Name "AspNetCoreModuleV2"
```

Salida esperada:

```
Name  : AspNetCoreModuleV2
Image : C:\Program Files\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll
```

### 3.4 Verificar el archivo DLL del módulo (opcional)

```powershell
Test-Path "C:\Program Files\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll"
```

Resultado esperado:

```
True
```

---

## 4. Recomendaciones para Despliegue en IIS

* Utilizar `dotnet publish` para generar los archivos publicados:

  ```bash
  dotnet publish -c Release -o C:\inetpub\misitio
  ```
* Asegurar permisos adecuados para el usuario `IIS_IUSRS` sobre la carpeta publicada.

### 4.1 Crear un sitio en IIS desde PowerShell

Ejemplo de script:

```powershell
Import-Module WebAdministration

$siteName = "MiSitioNetCore"
$sitePath = "C:\inetpub\misitio"
$port = 8080
$appPool = "MiSitioAppPool"

# Crear Application Pool sin código administrado
New-WebAppPool -Name $appPool
Set-ItemProperty IIS:\AppPools\$appPool -Name managedRuntimeVersion -Value ""
Set-ItemProperty IIS:\AppPools\$appPool -Name processModel.identityType -Value "ApplicationPoolIdentity"

# Crear el sitio
New-Website -Name $siteName -Port $port -PhysicalPath $sitePath -ApplicationPool $appPool
```

Este script crea un sitio web en IIS configurado para aplicaciones ASP.NET Core, en el puerto 8080, con un Application Pool dedicado sin código administrado.

---

## 5. Recursos

* Documentación oficial de hosting en IIS:
  [https://docs.microsoft.com/en-us/aspnet/core/host-and-deploy/iis/](https://docs.microsoft.com/en-us/aspnet/core/host-and-deploy/iis/)

* Descarga directa del Hosting Bundle 3.1.32:
  [https://download.visualstudio.microsoft.com/download/pr/4e98ff35-69ce-434c-a8fc-c3e9cc83a39e/68b8e8b324c729e9999f88a6214079d7/dotnet-hosting-3.1.32-win.exe](https://download.visualstudio.microsoft.com/download/pr/4e98ff35-69ce-434c-a8fc-c3e9cc83a39e/68b8e8b324c729e9999f88a6214079d7/dotnet-hosting-3.1.32-win.exe)

---

**Fin del documento**
