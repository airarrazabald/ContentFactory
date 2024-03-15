# PowerShell - Como obtener información desde Internet information services

Este script de PowerShell es una herramienta valiosa para un ingeniero que necesita obtener información sobre los sitios web y las aplicaciones web alojados en un servidor IIS (Internet Information Services). 

Obtenemos de forma rapida toda la información que se puede necesitar y generar un descubrimiento de las aplicaciones o sitios existente.  Aquí está la explicación del código desde esa perspectiva:

## Script Powershell

El siguiente escript ademas de obtener la información la exporta a un archivo txt separados por pipe "|":

```powershell
    Write-Host "Inicio - Script"
    $Websites = Get-Website
    $Hostname = hostname
    $filename = "apps-"+$Hostname+".txt"

    'Hostname|Type|Site|Webapp_Name|State|PhysicalPath|Bindings|AppPool_Name|AppPool_State|AppPool_ManagedRuntimeVersion' > $filename

    foreach ($Website in $Websites) {

        $AppPool = Get-IISAppPool -Name $Website.ApplicationPool

        $customWeb = [PSCustomObject]@{
            Hostname = $Hostname
            Type = 'Site'
            Site = $Website.Name -join ';'
            Webapp_Name = ''
            State                 = $Website.State -join ';'
            PhysicalPath          = $Website.PhysicalPath
            Bindings              = $Website.Bindings.Collection -join ';'
            AppPool_Name                  = $AppPool.Name -join';'
            AppPool_State                 = $AppPool.State -join ';'
            AppPool_ManagedRuntimeVersion = $AppPool.ManagedRuntimeVersion -join ';'

        }

        $customWeb.Hostname + '|' +$customWeb.Type + '|' + $customWeb.Site + '|' + $customWeb.Webapp_Name + '|' + $customWeb.State + '|' + $customWeb.PhysicalPath + '|' + $customWeb.Bindings + '|' + $customWeb.AppPool_Name + '|' + $customWeb.AppPool_State + '|' + $customWeb.AppPool_ManagedRuntimeVersion >> $filename
    }

    $Webapps = Get-WebApplication

    foreach ($Webapp in $Webapps) {
        $name = ($Webapp.Path).Replace('/','')
        $site = $Webapp.GetParentElement().Attributes['name'].Value
        $AppPool = Get-IISAppPool -Name $Webapp.ApplicationPool

        $customApp = [PSCustomObject]@{
            Hostname = $Hostname
            Type = 'Application'
            Site = $site
            Webapp_Name  = $name
            State = ''
            PhysicalPath = $Webapp.PhysicalPath
            Bindings = ''
            AppPool_Name                  = $AppPool.Name -join';'
            AppPool_State                 = $AppPool.State -join ';'
            AppPool_ManagedRuntimeVersion = $AppPool.ManagedRuntimeVersion -join ';'
        }

        $customApp.Hostname + '|' +$customApp.Type + '|' + $customApp.Site + '|' + $customApp.Webapp_Name + '|' + $customApp.State + '|' + $customApp.PhysicalPath + '|' + $customApp.Bindings + '|' + $customApp.AppPool_Name + '|' + $customApp.AppPool_State + '|' + $customApp.AppPool_ManagedRuntimeVersion >> $filename
    }  
    Write-Host $filename
    Write-Host "Fin - Script"
```

## Explicación de Script

1. `Write-Host "Inicio - Script"`: Este comando indica el inicio del script, lo cual es útil para el seguimiento de la ejecución del script.
2. `$Websites = Get-Website`: Este comando recopila todos los sitios web alojados en el servidor IIS. Esta información es crucial para entender qué sitios están actualmente en funcionamiento.
3. `$Hostname = hostname`: Este comando recupera el nombre del servidor, lo cual es útil para la documentación y el seguimiento.
4. `$filename = "apps-"+$Hostname+".txt"`: Este comando genera un nombre de archivo basado en el nombre del servidor. Este archivo se utilizará para almacenar la información recopilada.
5. ```'Hostname|Type|Site|Webapp_Name|State|PhysicalPath|Bindings|AppPool_Name|AppPool_State|AppPool_ManagedRuntimeVersion' > $filename```: Este comando crea un archivo y escribe en él la cabecera de la tabla. Este archivo servirá como un registro detallado de los sitios y aplicaciones web en el servidor.
6. `foreach ($Website in $Websites) {...}`: Este bucle recorre cada sitio web recopilado anteriormente, recopila información detallada sobre cada uno, incluyendo su estado, ruta física, enlaces, y detalles del pool de aplicaciones, y luego escribe esta información en el archivo.
7. `$Webapps = Get-WebApplication`: Este comando recopila todas las aplicaciones web alojadas en el servidor IIS.
8. `foreach ($Webapp in $Webapps) {...}`: Este bucle recorre cada aplicación web recopilada anteriormente, recopila información detallada sobre cada una, incluyendo su estado, ruta física, y detalles del pool de aplicaciones, y luego escribe esta información en el archivo.
9. `Write-Host $filename`: Este comando imprime el nombre del archivo en la consola. Esto es útil para saber dónde se ha guardado la información recopilada.
10. `Write-Host "Fin - Script"`: Este comando indica el final del script, lo cual es útil para el seguimiento de la ejecución del script.


## Conclusión

En conclusión, este script de PowerShell es una herramienta esencial para cualquier ingeniero que necesite recopilar información detallada sobre los sitios web y las aplicaciones web alojados en un servidor IIS. Proporciona una visión general rápida y eficiente del entorno de IIS, recopilando datos como el estado del sitio, la ruta física, los enlaces y los detalles del pool de aplicaciones. Además, almacena esta información en un archivo de texto para su posterior análisis y seguimiento. Este script es un excelente ejemplo de cómo se pueden utilizar las capacidades de automatización de PowerShell para simplificar y acelerar las tareas de administración del sistema.
