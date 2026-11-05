# 🌬️ SimulWind en Meta Quest 2 *Instalación y uso del simulador de aerogeneradores* { .card }

!!! info "OBJETIVOS"
    Esta guía explica cómo **instalar y ejecutar el simulador SimulWind**, de mantenimiento de aerogeneradores, en **todas las gafas Meta Quest 2** del centro.

    Antes de empezar, las gafas deben estar montadas y actualizadas siguiendo el [Manual de las Quest 2](meta-quest-2.md).

!!! info "RECURSOS"
    - Gafas **Meta Quest 2** actualizadas y con sus mandos.
    - Cable **USB-C** (USB 3, de al menos 3 m, para Quest Link) o red **Wi-Fi 5/6** en la misma red que el PC (para Air Link).
    - PC con **Windows 10/11** y tarjeta gráfica dedicada.
    - Cuenta Meta del centro.
    - Instalador de **SimulWind** facilitado por el profesorado.

!!! info ""
    **SimulWind** es un simulador de **mantenimiento de aerogeneradores** desarrollado en los proyectos europeos Erasmus+ *SIMULWIND* y *WindEXT*. Permite practicar procedimientos reales, como el **bloqueo del eje rápido**, la **sustitución del acoplamiento del eje rápido** o la del **motorreductor de orientación (yaw)**, con niveles de dificultad fácil, medio y difícil.

    Según sus requisitos oficiales, **es una aplicación para PC VR** (procesador tipo Intel i9-9900K, 16 GB de RAM, NVIDIA RTX 2070 y 3 GB de disco). Por eso, en las Quest 2 se usa **conectando las gafas al PC** mediante **Quest Link** (por cable) o **Air Link** (Wi-Fi). Las gafas muestran la imagen y el PC hace los cálculos.

## **1. Preparar el PC** { .seccion }

**1.1 Descargar SimulWind**: el profesorado facilita el instalador en la carpeta compartida del aula. Si hay que descargarlo de nuevo, se solicita en [simulwind.com](https://www.simulwind.com/) con un correo del centro, aceptando sus condiciones de uso y licencia. Instálalo en `C:\SimulWind` y crea un acceso directo en el escritorio.

**1.2 Instalar la app de escritorio de Meta**: descarga **Meta Quest Link** desde la [página oficial de configuración](https://www.meta.com/quest/setup/) e inicia sesión con la **cuenta Meta del centro**.

**1.3 Configurar la app**: en la app del PC, entra en **Ajustes → General** y:

- Activa **Orígenes desconocidos**. Es necesario para ejecutar aplicaciones que no proceden de la tienda de Meta, como SimulWind o SteamVR.
- En **OpenXR Runtime**, pulsa **Establecer Meta Quest Link como activo**.

**1.4 SteamVR (solo si SimulWind lo pide al arrancar)**: instala **Steam** y, dentro de Steam, **SteamVR**. Se iniciará automáticamente cuando lo necesite el simulador.

## **2. Conectar las gafas al PC** { .seccion }

=== "Quest Link (cable)"

    1. Enciende las gafas y conecta el **cable USB-C** al visor y a un puerto **USB 3** (azul) del PC.
    2. En la app del PC, en **Dispositivos**, añade **Quest 2** y elige **Link (cable)**. Pulsa **Probar conexión**: debe indicar compatibilidad USB 3.
    3. En las gafas, acepta **Habilitar Quest Link** y, si aparece, **Permitir acceso a los datos**.

=== "Air Link (Wi-Fi)"

    1. El PC debe estar conectado **por cable** al router, y las gafas en la **misma red** Wi-Fi 5/6 (5 GHz).
    2. En las gafas: **Ajustes rápidos → Quest Link** → activa **Usar Air Link** y elige el PC de la lista.
    3. Confirma el código de emparejamiento en el PC.

!!! tip "¿Cable o Wi-Fi?"
    En el aula, con varias gafas a la vez, el **cable** es más estable. Air Link solo funciona bien con una buena red de 5 GHz y pocos visores conectados a la vez.

## **3. Ejecutar SimulWind** { .seccion }

1. Dentro del entorno de Quest Link, abre el **Escritorio** desde la barra inferior: verás la pantalla del PC.
2. Ejecuta el acceso directo **SimulWind** del escritorio. Si se abre SteamVR, espera a que termine de cargar.
3. Quítate la pantalla de escritorio (vuelve al entorno VR) y el simulador aparecerá en las gafas.
4. Pulsa **Meta (mantenido)** para **recentrar** la vista y elige el procedimiento y el nivel de dificultad.
5. Al terminar, cierra el simulador desde su menú y desconecta Quest Link.

!!! note "Alternativa: versión APK autónoma"
    Si el centro dispone de una versión **APK** del simulador para Quest (sin PC), se instala **directamente en cada visor**:

    1. Crea una organización en [developers.meta.com](https://developers.meta.com/) con la cuenta del centro.
    2. En la app **Meta Horizon** del móvil: **Dispositivos → Ajustes del visor → Modo desarrollador** → activar.
    3. Conecta el visor al PC por USB y acepta **Permitir depuración USB** dentro de las gafas.
    4. Instala el APK con **Meta Quest Developer Hub**, **SideQuest** o por terminal con `adb`:

        ```powershell
        adb devices                       # debe aparecer el visor como "device"
        adb install -r .\simulwind.apk    # -r reinstala/actualiza si ya existía
        ```

    5. En las gafas, abre **Biblioteca → Orígenes desconocidos** y ejecuta SimulWind.

    Para instalarlo en **toda la caja** a la vez, conecta varias gafas a un hub USB y recórrelas con un bucle:

    ```powershell
    # Instala el APK en todas las gafas conectadas por USB
    adb devices | Select-String "\tdevice$" | ForEach-Object {
        $serie = ($_ -split "\t")[0]
        Write-Host "Instalando en $serie..."
        adb -s $serie install -r .\simulwind.apk
    }
    ```

## **Problemas frecuentes** { .seccion }

| Problema | Solución |
|---|---|
| El PC no detecta las gafas | Usa un puerto **USB 3**, prueba otro cable y acepta los permisos en las gafas |
| Quest Link se corta | Cierra aplicaciones en el PC, actualiza la app de Meta y los drivers de la gráfica |
| SimulWind no aparece en las gafas | Revisa **Orígenes desconocidos** y **OpenXR Runtime** (apartado 1.3) |

!!! example "REFERENCIAS"
    - Simulador SimulWind: [simulwind.com](https://www.simulwind.com/)
    - Proyecto europeo WindEXT: [windext.com](http://www.windext.com)
    - Configuración oficial de Meta Quest: [meta.com/quest/setup](https://www.meta.com/quest/setup/)
