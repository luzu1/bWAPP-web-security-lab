# bWAPP – Laboratorio de Seguridad Web

Este repositorio documenta prácticas hands-on realizadas con **bWAPP (Buggy Web Application)** como parte del programa de **Ciberseguridad de 4Geeks Academy**.

El objetivo del laboratorio es identificar, explotar y comprender vulnerabilidades web comunes en un entorno controlado, analizando su impacto y las causas de su existencia.

---

## Entorno de Trabajo

- Aplicación: bWAPP (bee-box)
- Sistema Operativo: Linux
- Servidor Web: Apache
- Base de Datos: MySQL
- Nivel de seguridad: Bajo (entorno educativo)

---

## Vulnerabilidades Analizadas

### 1. Insecure Direct Object Reference (IDOR)

La aplicación permite modificar información sensible de otros usuarios sin verificar la propiedad del recurso.

**Pasos realizados:**
1. Acceso a la funcionalidad *Change Secret*
2. Manipulación del identificador del usuario
3. Cambio exitoso del secreto de otra cuenta

![IDOR](screenshots/idor-change-secret.png)

---

### 2. Broken Authentication

El sistema de autenticación presenta controles débiles que permiten el acceso con credenciales triviales.

**Pasos realizados:**
1. Identificación del formulario de login inseguro
2. Uso de credenciales conocidas
3. Acceso exitoso sin protecciones adicionales

![Broken Authentication](screenshots/broken-auth-login.png)

---

### 3. SQL Injection (GET / Search)

La funcionalidad de búsqueda es vulnerable a inyección SQL mediante parámetros GET.

#### Enumeración de tablas
1. Prueba de inyección básica
2. Uso de `UNION SELECT`
3. Enumeración de tablas del sistema

![SQLi Tablas](screenshots/sqli-enumeracion-tablas.png)

#### Enumeración de columnas
1. Identificación de columnas relevantes
2. Uso de `information_schema`

![SQLi Columnas](screenshots/sqli-enumeracion-columnas.png)

#### Extracción de datos
1. Selección de columnas sensibles
2. Obtención de usuarios, emails y hashes

![SQLi Datos](screenshots/sqli-extraccion-datos.png)

---

### 4. Cross-Site Scripting (XSS)

#### XSS Reflejado (GET)
1. Inyección de código JavaScript vía URL
2. Ejecución del payload en el navegador

![XSS GET](screenshots/xss-reflected-get.png)

#### XSS Reflejado (POST)
1. Envío del payload mediante POST
2. Ejecución directa del script

![XSS POST](screenshots/xss-reflected-post.png)

#### XSS Almacenado (Stored)
1. Inserción del payload en el blog
2. Persistencia del código malicioso
3. Ejecución para cualquier usuario que acceda

![XSS Stored](screenshots/xss-stored-blog.png)

---

### 5. Local & Remote File Inclusion (LFI / RFI)

#### Lectura de archivos locales
1. Manipulación del parámetro `language`
2. Acceso a `/etc/hostname`
3. Acceso a configuraciones de Apache

![LFI Hostname](screenshots/lfi-hostname.png)
![LFI Apache](screenshots/lfi-apache-config.png)

#### Inclusión remota
1. Inclusión de recurso externo
2. Ejecución de código remoto

![RFI](screenshots/rfi-alert.png)

---

### 6. Evidencia en Logs del Servidor

Las inyecciones SQL quedan reflejadas en los logs del servidor web, demostrando trazabilidad del ataque.

**Pasos realizados:**
1. Acceso al archivo `access.log`
2. Identificación de payloads SQL
3. Correlación ataque → registro

![Access Log](screenshots/access-log-sqli.png)

---

## Conclusiones

- La falta de validación de entradas permite múltiples vectores de ataque
- Los controles de acceso son críticos para proteger recursos
- Vulnerabilidades clásicas siguen teniendo alto impacto
- La trazabilidad en logs es clave para detección y respuesta

---

## Aviso Legal

Todas las pruebas se realizaron en un **entorno controlado con fines educativos**.  
No se atacaron sistemas reales ni sin autorización.
