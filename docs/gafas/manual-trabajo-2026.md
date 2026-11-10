# 🧰 Manual de trabajo con las gafas · 2026 *Una cuenta del centro, modo desarrollador y ADB* { .card }

!!! info "OBJETIVOS"
    Este manual fija **cómo se trabaja con las 6 gafas Meta Quest 2** del aula ATECA (`Q2-01` … `Q2-06`) durante el curso 2026-27:

    - Todas las gafas usan **una única cuenta Meta del centro**.
    - Las aplicaciones se instalan como **APK** con **ADB** (las 6 gafas a la vez) o con **SideQuest**.
    - También se usan **experiencias web (WebXR)** desde el navegador de las gafas.

    Para el uso diario de las gafas (montaje, Guardián, carga) consulta el [Manual Quest 2](meta-quest-2.md).

!!! info "RECURSOS"
    - Las 6 gafas **Meta Quest 2** cargadas y con la **cuenta Meta del centro**.
    - La app **Meta Horizon** en el móvil del profesorado.
    - Un PC con **ADB** (Android Platform Tools) y, opcionalmente, **SideQuest**.
    - Un **hub USB** con alimentación y 6 cables **USB-C** de datos, o wifi en la misma red que el PC.

## **Decisiones del curso 2026-27** { .seccion }

### 1. Por qué una sola cuenta

| Opción | Resultado |
|---|---|
| **HMS + MDM** (gestión centralizada de Meta) | ❌ No sirve: Meta solo da HMS a Quest 3 y 3S, y desde 2025 ningún MDM puede gestionar gafas Quest sin HMS |
| **Una cuenta por gafa** | ⚠️ Posible, pero 6 cuentas que verificar y mantener, y las apps de pago se compran 6 veces |
| **Una cuenta del centro + APK y WebXR** | ✅ Opción elegida: sencilla, gratuita y las APK funcionan en las 6 gafas a la vez |

!!! warning "Límite de la cuenta única"
    Una misma cuenta **no puede abrir la misma app de la tienda de Meta en varias gafas a la vez** (pasa también con muchas apps gratuitas). Las **APK** instaladas a mano y las **experiencias web** normalmente no tienen esa comprobación.

    Si una app imprescindible de la tienda se bloquea, la solución es crear cuentas separadas solo para esa actividad.

### 2. Qué se puede usar en clase

| Tipo de contenido | Origen | ¿Las 6 gafas a la vez? |
|---|---|---|
| **APK** | itch.io, GitHub, web del desarrollador, SideQuest | ✅ Normalmente sí |
| **WebXR** | Navegador de las gafas (Meta Quest Browser) | ✅ Sí, sin instalar nada |
| **Vídeos 360°** | Copiados a las gafas con ADB | ✅ Sí |
| **Apps de la tienda de Meta** | Meta Horizon Store | ❌ Solo en una gafa a la vez |

## **Preparación (una sola vez)** { .seccion }

### 3. Cuenta de desarrollador del centro

Para activar el modo desarrollador, la cuenta Meta del centro tiene que pertenecer a una **organización de desarrollador verificada**. Se hace una sola vez:

1. Entra en [developers.meta.com](https://developers.meta.com/){target="_blank"} con la **cuenta del centro**.
2. **Crea una organización** (por ejemplo, `CIFP Villa de Agüimes - ATECA`).
3. **Verifica la cuenta** con un **móvil (SMS)** o una **tarjeta de pago** (PayPal no sirve).

!!! tip "Evita usar un número personal"
    Si hay que verificar de nuevo, usa preferiblemente un medio del centro. No borres el método de verificación: si se elimina, el modo desarrollador puede desactivarse.

### 4. Activar el modo desarrollador en cada gafa

Repite con cada gafa:

1. Enciende la gafa y abre la app **Meta Horizon** en el móvil (con la cuenta del centro).
2. Toca el **icono de las gafas** → elige la gafa → **Ajustes del visor** → **Modo desarrollador** → **Activar**.
3. **Reinicia** la gafa.
4. Conéctala al PC por USB y, dentro de la gafa, acepta **Permitir depuración USB** marcando **Permitir siempre desde este ordenador**.

!!! success "Comprobación"
    Con las 6 gafas conectadas, este comando debe mostrar **6 líneas** terminadas en `device`:

    ```powershell
    adb devices
    ```

    Si alguna aparece como `unauthorized`, ponte esa gafa y acepta la depuración USB.

### 5. Instalar ADB en el PC

1. Descarga **Android SDK Platform-Tools** de la web oficial de Android.
2. Descomprime la carpeta, por ejemplo en `C:\platform-tools`.
3. Añade esa carpeta al **PATH** de Windows.
4. Abre **PowerShell** y comprueba con `adb version`.

## **Trabajo diario** { .seccion }

### 6. Instalar una APK en las 6 gafas a la vez

Guarda este script como `C:\APK\instalar-apk.ps1`:

```powershell
# Instala una APK en todas las gafas conectadas por ADB
param([Parameter(Mandatory=$true)][string]$Apk)

$gafas = adb devices | Select-String "`tdevice$" | ForEach-Object { ($_ -split "`t")[0] }
Write-Host "Gafas detectadas: $($gafas.Count)"

foreach ($id in $gafas) {
    Write-Host "Instalando en $id..."
    adb -s $id install -r -g $Apk
}
```

Uso:

```powershell
cd C:\APK
.\instalar-apk.ps1 -Apk ".\mi-app.apk"
```

| Opción | Significado |
|---|---|
| `-r` | Reinstala o actualiza si la app ya existe |
| `-g` | Concede los permisos de la app al instalar |

!!! note "Si PowerShell bloquea el script"
    Ejecuta una vez `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`.

**Dónde encontrar la app en la gafa:** *Biblioteca* → filtro **Orígenes desconocidos**.

### 7. Comandos útiles de ADB

| Tarea | Comando |
|---|---|
| Ver gafas conectadas | `adb devices` |
| Listar apps instaladas por el centro | `adb -s ID shell pm list packages -3` |
| Desinstalar una app | `adb -s ID uninstall nombre.del.paquete` |
| Copiar un vídeo 360° | `adb -s ID push video.mp4 /sdcard/Movies/` |
| Ver la batería | `adb -s ID shell dumpsys battery` |
| Reiniciar la gafa | `adb -s ID reboot` |

Sustituye `ID` por el identificador que aparece en `adb devices`.

### 8. ADB sin cables (opcional)

Útil para actualizar las gafas sin moverlas de la estantería de carga.

1. Con la gafa conectada por USB: `adb -s ID tcpip 5555`
2. Mira la IP de la gafa en *Ajustes → Wi-Fi → red conectada*.
3. Desconecta el cable y ejecuta: `adb connect IP_DE_LA_GAFA:5555`
4. Al reiniciar la gafa hay que repetir el paso 1.

!!! warning "Misma red"
    El PC y las gafas deben estar en la **misma red wifi** y la red del centro debe permitir la conexión entre equipos.

### 9. SideQuest (alternativa gráfica)

**SideQuest** es un programa para PC que instala APK arrastrándolas a su ventana, gafa por gafa. Es cómodo para probar una app; para las 6 gafas es más rápido el script del apartado 6.

### 10. Experiencias web (WebXR)

1. Abre el **navegador** de las gafas.
2. Escribe la dirección de la experiencia o ábrela desde un marcador.
3. Pulsa **Entrar en realidad virtual**.

!!! tip "Marcadores compartidos"
    Prepara una página con los enlaces de la clase (por ejemplo, en esta web) para que el alumnado no tenga que escribir direcciones largas.

## **Normas y control** { .seccion }

### 11. Antes y después de cada clase

| Antes de clase | Después de clase |
|---|---|
| Gafas cargadas (LED verde) | Gafas **en la caja o boca abajo**, nunca al sol |
| `adb devices` muestra las 6 gafas | Cerrar las apps abiertas |
| App de la sesión instalada en todas | Limpiar lentes e interfaz facial |
| Wifi conectada | Poner a cargar |
| Probar la app en una gafa | Anotar incidencias en el inventario |

### 12. Normas para las APK

- Descarga **solo de fuentes fiables** (web del desarrollador, itch.io, GitHub).
- Revisa la **licencia**: que una app sea gratuita no siempre permite usarla en varias gafas de un centro.
- Guarda las APK aprobadas en una carpeta del centro, por ejemplo `APK/nombre-app/version.apk`.
- Las APK **no se actualizan solas**: cuando salga una versión nueva, vuelve a ejecutar el script.
- Las gafas no tienen servicios de Google Play: las APK de móvil que dependen de ellos no funcionan.

### 13. Inventario

| Etiqueta | N.º de serie | Modo desarrollador | ID ADB | Apps instaladas | Incidencias |
|---|---|:---:|---|---|---|
| Q2-01 | | ☐ | | | |
| Q2-02 | | ☐ | | | |
| Q2-03 | | ☐ | | | |
| Q2-04 | | ☐ | | | |
| Q2-05 | | ☐ | | | |
| Q2-06 | | ☐ | | | |

### 14. Problemas frecuentes

??? question "No aparece la opción Modo desarrollador en la app Meta Horizon"
    La cuenta no está en una organización de desarrollador o no está verificada. Revísalo en developers.meta.com.

??? question "La gafa aparece como unauthorized en adb devices"
    Ponte la gafa y acepta **Permitir depuración USB**. Si no aparece el aviso, desconecta y vuelve a conectar el cable.

??? question "La gafa no aparece en adb devices"
    Usa un cable USB-C **de datos** (no solo de carga), prueba otro puerto del hub y comprueba que el modo desarrollador sigue activo.

??? question "La app dice que no puede usarse en varios dispositivos a la vez"
    Es una app de la tienda de Meta con la misma cuenta en varias gafas. Usa una APK o una alternativa web, o una cuenta separada para esa actividad.

??? question "La APK se instala pero se cierra al abrirla"
    Puede depender de Google Play, no ser compatible con Quest 2 o ser antigua. Prueba la última versión del desarrollador.

??? question "El modo desarrollador se ha desactivado solo"
    Suele ocurrir si se borra el método de verificación de la cuenta. Vuelve a verificarla y actívalo de nuevo.

## **Vídeos en español** { .seccion }

<div class="video-row">
<figure>
<iframe src="https://www.youtube-nocookie.com/embed/unkC1ZcUFnM" title="Aprende a usar las Meta Quest" loading="lazy" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<figcaption>Aprende a usar las Meta Quest (primeros pasos)</figcaption>
</figure>
<figure>
<iframe src="https://www.youtube-nocookie.com/embed/wMUlDf8puUk" title="Activar el modo desarrollador en Meta Quest" loading="lazy" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<figcaption>Activar el modo desarrollador (2026)</figcaption>
</figure>
<figure>
<iframe src="https://www.youtube-nocookie.com/embed/I12NHiOdNXs" title="Cómo instalar SideQuest en Meta Quest" loading="lazy" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<figcaption>Cómo instalar SideQuest (El Rincón del Friki)</figcaption>
</figure>
</div>

## **Fuentes** { .seccion }

- [Meta Developers – Activar el modo desarrollador](https://developers.meta.com/horizon/documentation/android-apps/enable-developer-mode/){target="_blank"}
- [Meta Developers – Configuración de dispositivos Quest](https://developers.meta.com/vr/documentation/native/android/mobile-device-setup-quest/){target="_blank"}
- [Android Developers – Android Debug Bridge (ADB)](https://developer.android.com/tools/adb){target="_blank"}
- [ManageXR – Integración con HMS (MDM solo mediante HMS)](https://help.managexr.com/en/articles/10518345-quick-start-integrating-managexr-with-meta-horizon-managed-services){target="_blank"}
- [Meta for Work](https://www.meta.com/es/meta-for-work/){target="_blank"}
