# Malwatcher: Análisis de archivos con VirusTotal

Aplicación web full-stack para detectar malware en archivos. El usuario sube un archivo, el sistema lo envía a la API de **VirusTotal** y muestra el resultado de varios motores antivirus. Cada análisis queda guardado en el historial del usuario.

Proyecto final de tercer corte de **Programación II**, tercer semestre de Ingeniería de Sistemas, Universidad El Bosque.

## Funcionalidades

- Registro de usuarios con verificación por código enviado al correo.
- Inicio de sesión.
- Carga de archivos de hasta **200 MB** para analizarlos.
- Reporte del análisis con los resultados de varios motores antivirus.
- Historial de análisis por usuario.
- Cifrado AES del usuario y la contraseña en la base de datos.
- Usuario administrador creado automáticamente al iniciar el backend.

## Tecnologías

- **Frontend:** Angular 17, TypeScript
- **Backend:** Java 21, Spring Boot 3, Spring Data JPA, Maven
- **Base de datos:** MySQL
- **Servicios externos:** API v3 de VirusTotal y Gmail (SMTP) para el envío de correos
- **Documentación de la API:** Springdoc OpenAPI (Swagger)

## Estructura

- `Fronted/malwatcher/`: aplicación Angular.
  - `src/app/`: componentes de inicio, registro, inicio de sesión, análisis e historial.
  - `src/app/service/`: servicios que se comunican con el backend.
- `malwatcher/`: backend Spring Boot.
  - `controller`: endpoints REST de usuarios (`/usuario`) y de VirusTotal (`/api/virustotal`).
  - `model`: entidad `Usuario` y DTO de los análisis.
  - `repository`: acceso a la base de datos con JPA.
  - `service`: lógica de usuarios y conexión con VirusTotal.
  - `util`: cifrado AES y envío de correos.
  - `configuration`: carga inicial del usuario administrador.

## Cómo ejecutarlo

### Requisitos

- JDK 21
- Node.js 18 o superior
- MySQL
- Una API key de VirusTotal (gratis en https://www.virustotal.com)
- Una cuenta de Gmail con contraseña de aplicación

### Configuración

Reemplazar los valores de ejemplo:

| Archivo | Valor |
|---|---|
| `malwatcher/src/main/resources/application.properties` | URL, usuario y contraseña de MySQL (`TU_CONTRASENA_DE_MYSQL`) |
| `service/HttpHandler.java` y `service/VirusTotalService.java` | `TU_API_KEY_DE_VIRUSTOTAL` |
| `util/MailSender.java` y `util/RemitenteCorreo.java` | Correo y `TU_CONTRASENA_DE_APLICACION` |

Crear en MySQL una base de datos llamada `malwatcher`. Las tablas se crean solas al iniciar el backend.

### Backend

```bash
cd malwatcher
./mvnw spring-boot:run
```

El backend queda en http://localhost:8082. La documentación de la API está en http://localhost:8082/swagger-ui.html.

### Frontend

```bash
cd Fronted/malwatcher
npm install
npm start
```

Abrir http://localhost:4200 en el navegador.

## Equipo

- Gabriel Alejandro Ruiz Cruz
- Dylan Mathyus Hospital Herrera
- Germán Octavio Vela Cardozo
- Juan Diego Triana Mejía
