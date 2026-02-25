📚 Audiobook-Stack-RPi: "A Prueba de Madres" 🔊
Este proyecto permite desplegar un ecosistema completo para la descarga, gestión y reproducción de audiolibros en una Raspberry Pi (probado en Debian 13). Está diseñado para que cualquier miembro de la familia pueda descargar libros y escucharlos directamente en una Smart TV LG con el control remoto.

🚀 Características
Descarga Simplificada: Instancia dedicada de Transmission (Puerto 9092) configurada para descargar directamente a la biblioteca.

Reproducción en TV: Jellyfin configurado para servir audiolibros a la app oficial de LG WebOS.

Gestión Avanzada: Audiobookshelf para organizar metadatos, series y unir (merge) libros de múltiples archivos.

Persistencia de lectura: El sistema recuerda exactamente dónde te quedaste en cada libro.

🛠️ Estructura de Carpetas
El proyecto se organiza en /home/raspin/ para separar la configuración de los archivos multimedia:
```text
Plaintext
/home/user/
├── audiobook-stack/          # Este repositorio (Docker Compose)
├── audiolibros/              # Los archivos MP3/M4B finales
├── jellyfin/                 # Configuración de Jellyfin
├── audiobookshelf/           # Configuración de Audiobookshelf
└── transmission_libros/      # Configuración del descargador
```
📦 Instalación
Preparar el sistema:

Bash
mkdir -p /home/raspin/audiolibros /home/raspin/jellyfin/config /home/raspin/audiobookshelf/config /home/raspin/transmission_libros/config
sudo chown -R 1000:1000 /home/raspin/audiolibros /home/raspin/jellyfin /home/raspin/audiobookshelf /home/raspin/transmission_libros
Desplegar con Docker Compose:
Copia el archivo docker-compose.yml en la carpeta audiobook-stack/ y ejecuta:

Bash
cd /home/raspin/audiobook-stack
docker-compose up -d
Puertos configurados:

Transmission (Descargas): http://tu-ip-rpi:9092

Jellyfin (TV/Media): http://tu-ip-rpi:8096

Audiobookshelf (Gestión): http://tu-ip-rpi:13378

📖 Guía de Uso (Flujo de trabajo)
1. Descarga
Entrar a la interfaz de Transmission (puerto 9092), pegar el enlace magnet o subir el archivo .torrent. Los archivos se guardarán automáticamente en la carpeta de la biblioteca.

2. Organización (Opcional pero recomendado)
Si un libro viene en muchas partes (múltiples MP3), entrar a Audiobookshelf (13378) y usar la función "Merge" para convertirlos en un solo archivo .m4b. Esto facilita la navegación en la TV.

3. Reproducción
Abrir la app de Jellyfin en la Smart TV LG. Los libros aparecerán con su carátula y descripción. Seleccionar y dar a Play.

⚠️ Notas Técnicas
Permisos: Si los contenedores no pueden escribir archivos, verificar los permisos con sudo chmod -R 777 /home/raspin/audiolibros.

Firewall: Asegurarse de tener abiertos los puertos 8096, 9092 y 13378 en el sistema (ufw allow).

Jellyfin en LG: Configurar la biblioteca como tipo "Música" y activar la opción de "Reproducción continua" para no perder el progreso.

Hecho con ❤️ para que mamá no deje de leer (ni de escuchar).
¡Gracias totales!
