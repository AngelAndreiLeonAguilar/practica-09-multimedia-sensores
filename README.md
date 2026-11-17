# Práctica 9 — Cámara, multimedia y sensores de movimiento

## Objetivo

Integrar captura de imágenes y lectura de sensores (acelerómetro y giroscopio) para crear interacción con el hardware del dispositivo, y desarrollar una **bitácora de inspección** que guarde foto, fecha/hora y valores de los sensores en una tarjeta de evidencia.

## Funciones

| Pantalla | Descripción |
|---|---|
| Ejemplo guiado | Ejemplo del manual: botón de cámara, vista previa de la foto y lecturas X/Y/Z del acelerómetro, más la ampliación con giroscopio. |
| Bitácora de inspección | Panel en vivo con acelerómetro y giroscopio. Al pulsar **Nueva evidencia** se toma una foto y se crea una tarjeta con la imagen, la fecha/hora y los valores de ambos sensores en ese instante. |

Manejo de casos:

- **Cancelación de cámara:** si el usuario cierra la cámara sin tomar foto, se muestra un aviso y no se crea ninguna tarjeta.
- **Permiso denegado:** se captura la `PlatformException` de `image_picker` y se pide habilitar el permiso en Ajustes.
- **Sensor no disponible:** si el dispositivo no tiene giroscopio o acelerómetro, el panel muestra "No disponible" y la app sigue funcionando.
- **Sin bloquear la interfaz:** los sensores se leen por streams con `SensorInterval.uiInterval`. Las lecturas en vivo usan `ValueNotifier`, así que solo se redibuja el panel y no la lista de tarjetas. Las suscripciones se cancelan en `dispose()`.

## Estructura

```
lib/
  main.dart                     Menú principal
  models/registro_inspeccion.dart
  services/camara_service.dart  Captura + cancelación/permisos
  services/sensores_service.dart Streams de sensores (inyectables)
  pages/sensores_page.dart      Ejemplo guiado
  pages/bitacora_page.dart      Ejercicio evaluable
  widgets/tarjeta_evidencia.dart
test/widget_test.dart
docs/evidencias/practica-09/
```

## Requisitos

- Flutter 3.x (SDK de Dart ≥ 3.0)
- Dispositivo físico Android o iOS con cámara, acelerómetro y giroscopio
- Paquetes: `image_picker`, `sensors_plus`, `intl`

## Permisos

| Plataforma | Configuración |
|---|---|
| Android | `AndroidManifest.xml`: `uses-feature` de cámara, acelerómetro y giroscopio (`required="false"`). `image_picker` abre la cámara del sistema mediante un intent, así que no hace falta declarar `CAMERA`. |
| iOS | `Info.plist`: `NSCameraUsageDescription`, `NSPhotoLibraryUsageDescription`, `NSMotionUsageDescription`. |

## Instalación y ejecución

```bash
git clone <url-del-repositorio>
cd <carpeta>
flutter pub get
flutter run        # con el teléfono conectado y depuración USB activa
```

## Pruebas

```bash
dart format .
flutter analyze
flutter test
```

Las pruebas automáticas usan streams y cámara simulados. Cubren las lecturas en vivo, la creación de la tarjeta con valores congelados, la cancelación, el permiso denegado y el sensor no disponible.

Casos manuales (en dispositivo físico):

1. Inclinar el teléfono y comprobar que cambian X, Y y Z del acelerómetro.
2. Girar el teléfono y comprobar que cambia el giroscopio.
3. Tomar una foto y verificar que se crea la tarjeta con fecha/hora y valores.
4. Abrir la cámara y cancelar: debe aparecer "Captura cancelada".
5. Denegar el permiso de cámara (iOS) o revocarlo en Ajustes: debe aparecer el aviso de permiso.

## Evidencias

Ver `docs/evidencias/practica-09/`.

## Uso de IA

Este proyecto se desarrolló con apoyo de un asistente de IA (Claude) para generar y revisar el código. El equipo lo revisó, lo ejecutó en un dispositivo físico y es responsable de su contenido.

## Participantes

- _Nombre completo — matrícula_
