[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/BlackShell256/ReflectUnhook/blob/main/LICENSE)
[![Telegram](https://badgen.net/badge/icon/telegram?icon=telegram&label)](https://t.me/MalwareBit)
[![LinkedIn](https://img.shields.io/static/v1.svg?label=LinkedIn&message=@anibal&logo=linkedin&style=flat&color=blue)](https://www.linkedin.com/in/anibal-5a3870278/)
[![YouTube](https://img.shields.io/badge/YouTube-%23FF0000.svg?logo=YouTube&logoColor=white)](https://www.youtube.com/@MalwarebitTeam)

| Español | [English](https://github.com/BlackShell256/ReflectUnhook?tab=readme-ov-file)  |
| --- | --- |

# ReflectUnhook
ReflectUnhook es una herramienta avanzada escrita en PowerShell que utiliza Reflection para acceder a la API de Windows y funciones de bajo nivel. Esta herramienta se enfoca en limpiar los hooks presentes en el módulo ntdll.dll de la memoria, restaurando su estado original mediante la lectura de ntdll.dll directamente desde el disco.

---

## ¿Qué son los hooks?

Las herramientas de detección y respuesta en endpoints (EDR) emplean una técnica llamada hooking para supervisar funciones críticas del sistema en las DLL de los procesos que están en ejecución. El hooking consiste en modificar dinámicamente las DLL del sistema en memoria, lo que permite a los EDR interceptar y analizar el flujo de ejecución de un programa para evaluar si su comportamiento es legítimo o malicioso.

El proceso funciona de la siguiente manera: los EDR alteran las instrucciones iniciales de ciertas funciones dentro de las DLL. Cuando estas funciones son llamadas, el flujo de ejecución del programa es desviado hacia el código del EDR, que generalmente reside en una DLL propia cargada en el proceso. Una vez redirigido, el EDR examina los parámetros de las funciones interceptadas para determinar si están siendo utilizadas de manera segura o potencialmente peligrosa. Si se considera que la operación es legítima, el EDR permite que el programa retome su flujo normal de ejecución y la función se completa sin interrupciones.

Para evadir la detección de un EDR, los atacantes pueden recurrir a una técnica conocida como unhooking. Este método restaura el contenido de la sección de código (.text) de la DLL afectada a su estado original, eliminando cualquier modificación realizada por el EDR. Con esto, el malware puede ejecutar sus funciones sin ser interceptado ni analizado.
<br><br><ins>Funcion hookeada</ins><br><br>
![image](https://github.com/user-attachments/assets/eed6af23-3e04-430c-962d-5474edc3a739)
<br><br><ins>Funcion limpia luego de ejecutar ReflectUnhook</ins><br><br>
![image](https://github.com/user-attachments/assets/6da4d13f-489f-4736-b9f4-d0ad18e79eb8)

---

## Características principales

- **Reflection**: Permite acceder a funciones de bajo nivel de la API de Windows sin necesidad de tocar el disco usando el comando (Cmdlet) "Add-Type".
- **Eliminación de hooks**: Limpia los hooks en `ntdll.dll` utilizados por soluciones AV/EDR.
- **Lectura desde el disco**: Recupera el estado original del módulo directamente desde su archivo en el sistema.

---

## Uso
Para utilizar ReflectUnhook, ejecute los siguientes comandos:

Con este comando ejecutaremos ReflectUnhook en memoria 
```
iex (iwr -UseBasicParsing https://raw.githubusercontent.com/BlackShell256/ReflectUnhook/refs/heads/main/ReflectUnhook.ps1)
```
Para ejecutar
```
Invoke-ReflectUnhook
```
Para obtener información detallada sobre la herramienta
```
Invoke-ReflectUnhook -v
```

### Ejemplo de uso
![image](https://github.com/user-attachments/assets/8a69184a-08ab-4115-9ac7-0d19ea4c56d1)

---

Recomiendo usar ReflectUnhook + bypass de amsi para una evasion mas completa, puede usar [Null-AMSI](https://github.com/BlackShell256/Null-AMSI) (Mi herramienta personalizada de AMSI Bypass) o alguna de su preferencia

---

## Créditos

* Parte del código de Reflection lo aprendí de Matt Graeber. [X/Twitter](https://x.com/mattifestation)

* Gran parte del código es de la herramienta Invoke-ReflectivePEInjection de PowerSploit. [Github](https://github.com/PowerShellMafia/PowerSploit/blob/master/CodeExecution/Invoke-ReflectivePEInjection.ps1)
