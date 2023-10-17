# Configuración de OWASP ZAP y FoxyProxy en un Contenedor Docker

Este repositorio contiene instrucciones sobre cómo configurar OWASP ZAP en un contenedor Docker y usar FoxyProxy para capturar el tráfico de aplicaciones web. Además, se describe cómo exportar la sesión desde el contenedor para su posterior análisis en una instalación local de OWASP ZAP.

## 1. Crear una imagen Docker personalizada de OWASP ZAP

Puedes utilizar un Dockerfile personalizado para crear una imagen de OWASP ZAP que cumpla con tus requisitos. A continuación, se muestra un ejemplo de un Dockerfile simple:

```Dockerfile
# Usa una imagen base
FROM debian:bullseye

# Actualiza el sistema y agrega dependencias
RUN apt-get update && apt-get install -y \
   openjdk-11-jre-headless \
   wget

# Descarga e instala OWASP ZAP
RUN wget -q -O - https://github.com/zaproxy/zaproxy/releases/download/v2.11.0/ZAP_2.11.0_Linux.tar.gz | tar xz -C /opt

# Configura el puerto para la interfaz web de ZAP
EXPOSE 8080

# Inicia ZAP en modo demonio
CMD ["/opt/ZAP_2.11.0/zap.sh", "-daemon", "-host", "0.0.0.0", "-port", "8080"]

