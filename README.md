# Práctica 9 – Cámara, multimedia y sensores de movimiento

App en Flutter para registrar una **bitácora de inspección**: captura fotografías con la cámara del dispositivo, lee en tiempo real el acelerómetro y el giroscopio, y guarda cada foto con su fecha/hora y los valores de los sensores en una tarjeta de evidencia.

## Objetivo

Integrar captura de imágenes y lectura de sensores para crear interacción con hardware del dispositivo.

## Funciones

- **Cámara y sensores (ejemplo guiado):** toma una fotografía con `image_picker`, la muestra en pantalla y lee los ejes X, Y y Z del acelerómetro. Como ampliación agrega la lectura del giroscopio.
- **Manejo de cámara y permisos:** distingue captura correcta, cancelación por el usuario, permiso denegado y errores, sin cierres inesperados.
- **Bitácora de inspección (ejercicio evaluable):**
  - Panel de lectura en vivo del acelerómetro (m/s²) y del giroscopio (rad/s).
  - Botón "Nueva evidencia" para capturar una fotografía.
  - Tarjeta de evidencia con la foto, la fecha/hora y los valores de ambos sensores en el momento de la captura.
  - Lista numerada con la evidencia más reciente primero.
  - Aviso cuando se cancela la cámara o falta el permiso, y "No disponible" si el dispositivo no tiene alguno de los sensores.
- **Sensores sin bloquear la interfaz:** streams con `SensorInterval.uiInterval`. Los valores en vivo van en `ValueNotifier`, así que solo se redibuja el panel. Las suscripciones se cancelan en `dispose()`.

## Requisitos

- Flutter 3.x (probado con Flutter 3.47 / Dart 3.13)
- Android Studio o Xcode
- Dispositivo físico con cámara, acelerómetro y giroscopio, o emulador con cámara y sensores virtuales

Paquetes: `image_picker`, `sensors_plus`, `intl`.

## Instalación

```bash
git clone <url-del-repositorio>
cd <carpeta-del-proyecto>
git checkout practica-09-multimedia-sensores
flutter pub get
```

## Ejecución

```bash
flutter run
```

En el emulador de Android los valores de los sensores se pueden cambiar desde *Extended controls → Virtual sensors*, y la cámara usa la escena virtual del emulador.

## Permisos configurados

| Plataforma | Archivo | Permisos |
|---|---|---|
| Android | `android/app/src/main/AndroidManifest.xml` | `uses-feature` de `camera`, `sensor.accelerometer` y `sensor.gyroscope` (`required="false"`). `image_picker` abre la cámara del sistema mediante un intent, por lo que no requiere `CAMERA` en tiempo de ejecución |
| iOS | `ios/Runner/Info.plist` | `NSCameraUsageDescription`, `NSPhotoLibraryUsageDescription`, `NSMotionUsageDescription` |

## Estructura

```
lib/
  main.dart                          Menú y navegación entre pantallas
  models/registro_inspeccion.dart    Modelo del registro y lecturas de ejes
  services/camara_service.dart       Captura, cancelación y permisos
  services/sensores_service.dart     Streams de acelerómetro y giroscopio
  pages/sensores_page.dart           Ejemplo guiado
  pages/bitacora_page.dart           Bitácora de inspección
  widgets/tarjeta_evidencia.dart     Tarjeta con foto, fecha/hora y sensores
test/widget_test.dart                Pruebas unitarias y de widgets
docs/evidencias/practica-09/         Capturas y resultados de pruebas
```

## Pruebas

```bash
dart format .
flutter analyze
flutter test
```

Resultados en [`docs/evidencias/practica-09/pruebas.md`](docs/evidencias/practica-09/pruebas.md).

## Vinculación con el proyecto integrador

La captura de fotos y la lectura de sensores están separadas en `camara_service.dart` y `sensores_service.dart`, así que se pueden reutilizar en el proyecto integrador. Por ejemplo, para adjuntar fotografías de evidencia a un registro, o para guardar la orientación del dispositivo en el momento de una captura. Las dos dependencias se pueden inyectar, por lo que el flujo se prueba sin hardware.

## Uso de IA

En el desarrollo se usó un asistente de IA (Claude) como apoyo para generar y revisar el código.

## Participantes

- Angel Andrei Leon Aguilar
