# Evidencias — Práctica 9

Capturas tomadas en el **emulador Android "Medium Phone API 36.1"** (1080×2400, Android 16) con cámara y sensores virtuales. Las lecturas de acelerómetro y giroscopio se fijaron con `adb emu sensor set` para comprobar que la app las refleja.

| Archivo | Contenido |
|---|---|
| `00_inicio.png` | Menú principal: ejemplo guiado y bitácora |
| `01_ejemplo_guiado.png` | Ejemplo guiado con la foto capturada y lecturas de acelerómetro (2.50, 4.10, 8.60) y giroscopio (0.35, -0.12, 0.08) |
| `02_bitacora_vivo.png` | Bitácora sin registros, con panel de lectura en vivo |
| `04_cancelacion.png` | La cámara se abrió y se canceló con Atrás: aviso "Captura cancelada por el usuario" y no se crea tarjeta |
| `03_tarjeta_evidencia.png` | Dos evidencias creadas con lecturas distintas; cada tarjeta conserva fecha/hora y valores del momento de la foto |
| `03b_tarjetas_scroll.png` | Desplazamiento: el panel en vivo cambió (1.10, 8.20, 4.90) y las tarjetas mantienen sus valores |
| `pruebas_automaticas.txt` | Salida de `flutter analyze` (sin problemas) y `flutter test` (8 pruebas pasan) |

## Permisos

- **Android:** `image_picker` abre la cámara del sistema mediante un intent, así que no pide permiso en tiempo de ejecución. El permiso denegado se cubre con una prueba automática.
- **iOS:** `NSCameraUsageDescription`, `NSPhotoLibraryUsageDescription` y `NSMotionUsageDescription` en `Info.plist`. No se probó en un dispositivo iOS.

## Pendiente

- Capturas en un dispositivo físico (modelo y versión: _completar_).
- Video o GIF (opcional): _enlace_.
