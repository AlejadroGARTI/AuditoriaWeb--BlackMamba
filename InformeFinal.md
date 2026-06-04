# Informe de Auditoría de Seguridad

---

## Cliente

- **Cliente:** Black Mamba  
- **Fecha de emisión:** 04/06/2026  
- **Auditor Jefe:** Alejandro Gutiérrez Alañón 
- **Clasificación del Documento:** CONFIDENCIAL  

---

## Resumen Ejecutivo

Tras realizar la auditoría basada en la metodología MAGERIT y el cumplimiento del ENS, se concluye que la postura de seguridad de la infraestructura actual de Black Mamba es crítica ya que se han identificado y evaluado un total de 6 hallazgos, de los cuales tres presentan un nivel de riesgo crítico, por lo que la organización está expuesta a ciberataques con una probabilidad muy elevada en el corto plazo de que estos problemas afecten los activos de la empresa.

El principal problema reside en el uso de software obsoleto y sin parches de seguridad, lo que convierte los sistemas críticos de la empresa en un blanco fácil para atacantes. Aunque existen problemas de configuración y mantenimiento como los temas inactivos o la falta de caché, la amenaza más inmediata y grave es técnica, ya que los componentes centrales del negocio están desactualizados, facilitando de esta forma la ejecución remota de comandos, robo de datos o caída de servicios.

En cuanto al impacto directo en el negocio, si Black Mamba no soluciona estos riesgos críticos de forma inmediata, las consecuencias podrían significar la perdida completa del negocio ya que a nivel financiero, un ataque exitoso podría paralizar el negocio durante días, con la consiguiente pérdida de ingresos, costes de recuperación forense y posibles multas regulatorias, o incluso, perder los datos para siempre.

---

## Alcance y Metodología

### Sistemas evaluados
Se ha auditado el servidor principal con sistema operativo Ubuntu 16.04, el middleware (PHP 7.0.33) que actúa como capa de integración, la aplicación web (WordPress 6.5.8) y la base de datos SQL que almacena los datos de negocio. También se han revisado las comunicaciones internas y externas del entorno.

### Marcos normativos aplicados
- Metodología MAGERIT v3
- Controles del Esquema Nacional de Seguridad (ENS)

### Herramientas utilizadas
- Inspección manual de configuración de WordPress (temas activos/inactivos, plugins recomendados).
- Análisis de cabeceras HTTP y respuesta del servidor para detectar ausencia de caché


Estas herramientas han sido utilizadas para la recolección de evidencias técnicas, análisis de vulnerabilidades y validación de hallazgos.

---

## Top 3 Hallazgos Críticos

### Hallazgo 1

- **Nombre del Hallazgo:** Versión obsoleta de PHP en el Middleware
- **Nivel de Riesgo:** Muy Alto / Crítico (Riesgo Potencial 81.0)
- **Condición (Lo que es):** El servidor ejecuta PHP 7.0.33-0ubuntu0.16.04.16, una versión lanzada en 2018 que ya no recibe parches de seguridad.
- **Criterio (Lo que debería ser):**  Todo software en producción debe mantenerse en versiones soportadas por el fabricante y con parches de seguridad aplicados periódicamente. 
- **Causa:** Falta de un plan de actualización y mantenimiento del software base; probablemente se priorizó la estabilidad funcional sobre la seguridad.
- **Consecuencia e Impacto:**  Un atacante remoto puede explotar vulnerabilidades críticas conocidas (ej. CVE-2018-19518, inyección de comandos en imap_open) para ejecutar comandos arbitrarios, tomar control del servidor, robar o destruir datos de negocio.
- **Plan de Acción (Recomendación):** Actualizar PHP a una versión soportada (8.x) y aplicar parches de seguridad mensualmente bajo un plan de gestión de vulnerabilidades [op.exp.8].

---

### Hallazgo 2

- **Nombre del Hallazgo:** Servidor SQL obsoleto
- **Nivel de Riesgo:** Alto (Riesgo Potencial 80.0)
- **Condición (Lo que es):** La base de datos que almacena los datos de negocio ejecuta una versión antigua y sin soporte del motor SQL.
- **Criterio (Lo que debería ser):** Los sistemas que alojan información crítica (confidencialidad alta) deben estar actualizados y recibir parches de seguridad de forma continua.
- **Causa:** Ausencia de procesos de actualización y mantenimiento en la capa de persistencia de datos; probablemente se priorizó la compatibilidad de la aplicación sobre la seguridad.
- **Consecuencia e Impacto:** Un atacante puede explotar vulnerabilidades conocidas en versiones obsoletas del motor SQL para realizar inyecciones SQL, escalar privilegios y extraer información confidencial. Esto expone a Black Mamba a filtraciones de datos, sanciones regulatorias (RGPD), pérdidas económicas y daños reputacionales.
- **Plan de Acción (Recomendación):** Actualizar el motor de base de datos a una versión estable y con soporte activo, realizando pruebas de compatibilidad previas en un entorno de ensayo [op.exp.8].

---

### Hallazgo 3

- **Nombre del Hallazgo:** WordPress desactualizado con vulnerabilidades activas
- **Nivel de Riesgo:** Alto (Riesgo Potencial 72.0)
- **Condición (Lo que es):** El sitio web utiliza WordPress 6.5.8, una versión que presenta vulnerabilidades conocidas de tipo SSRF y XSS.
- **Criterio (Lo que debería ser):** Las aplicaciones web expuestas a Internet deben mantenerse actualizadas a la última versión estable para evitar vectores de ataque conocidos.
- **Causa:** Falta de un proceso de actualización continua del CMS y sus componentes; probablemente se aplican actualizaciones únicamente de forma reactiva.
- **Consecuencia e Impacto:** Un atacante podría explotar la vulnerabilidad SSRF para acceder a recursos internos o servicios restringidos, o aprovechar el XSS para secuestrar sesiones de administradores, robar cookies y tomar el control del sitio web, afectando la disponibilidad y confidencialidad de los datos.
- **Plan de Acción (Recomendación):** Actualizar WordPress a la última versión estable, establecer un calendario de actualizaciones periódicas y habilitar actualizaciones automáticas de seguridad [op.exp.8].

---

## Anexos Técnicos

### Tablas de Auditoría

#### 🔴 Identificación y Valoración de Activos
##### 🟢 Valor propio
###### MAGERIT
| Ref.   | Activo              | C | I | A | Au | T |
|--------|---------------------|---|---|---|----|---|
| INF-1  | Datos de negocio    | 10 | 9 | 8 | 6  | 6 |
| SW-1   | Aplicación Web      | 3 | 8 | 7 | 5  | 4 |
| SW-2   | Middleware          | 4 | 7 | 7 | 4  | 4 |
| COM-1  | Comunicaciones      | 10 | 9 | 6 | 8  | 5 |
| HW-1   | Servidor Ubuntu     | 4 | 7 | 7 | 4  | 5 |
###### ENS
| Ref.  | Activo             | C | I | A | Au | T |
|-------|--------------------|---|---|---|----|---|
| INF-1 | Datos de negocio   | A | A | A | M  | M |
| SW-1  | Aplicación Web     | B | A | M | M  | B |
| SW-2  | Middleware         | B | M | M | B  | B |
| COM-1 | Comunicaciones     | A | A | M | A  | M |
| HW-1  | Servidor Ubuntu    | B | M | M | B  | M |
##### 🟢 Valor acumulado
###### MAGERIT
| Ref.   | Activo              | C | I | A | Au | T |
|--------|---------------------|---|---|---|----|---|
| INF-1  | Datos de negocio    | 10 | 9 | 8 | 6  | 6 |
| SW-1   | Aplicación Web      | 10 | 9 | 8 | 6  | 6 |
| SW-2   | Middleware          | 10 | 9 | 8 | 6  | 6 |
| COM-1  | Comunicaciones      | 10 | 9 | 8 | 8  | 6 |
| HW-1   | Servidor Ubuntu     | 10 | 9 | 8 | 8  | 6 |
###### ENS
| Ref.  | Activo             | C | I | A | Au | T |
|-------|--------------------|---|---|---|----|---|
| INF-1 | Datos de negocio   | A | A | A | M  | M |
| SW-1  | Aplicación Web     | A | A | A | M  | M |
| SW-2  | Middleware         | A | A | A | M  | M |
| COM-1 | Comunicaciones     | A | A | A | A  | M |
| HW-1  | Servidor Ubuntu    | A | A | A | A  | M |
#### 🔴 Identificación de Amenazas
| Ref.  | Hallazgo                                | Activo Afectado | Código Amenaza | Justificación |
|-------|-----------------------------------------|----------------|---------------|--------------|
| AM-01 | Versión obsoleta de PHP (7.0.33-0ubuntu0.16.04.16)        | SW-2 (Middleware)          | S.21         | Al ser una versión obsoleta del 2018 que ya no recibe parches de seguridad , se expone tanto al servidor, como a la página web a recibir ataques críticos, en donde desctacan vulnerabilidades como la inyección de Comando (CVE-2018-19518) en donde un fallo crítico en la función imap_open, permite a un atacante remoto ejecutar comandos arbitrarios en el servidor enviando un nombre de servidor IMAP manipulado. |
| AM-02 | Actualización de WordPress (7.0)        | SW-1 (Aplicación Web)          | S.21         | La versión actual de WordPress (6.5.8) posee múltiples vulnerabilidades, entre las que destacan una vulnerabilidad de tipo SSRF (Server-Side Request Forgery) que permite que un atacante obligue al servidor a hacer peticiones internas o externas o también una vulnerabilidad de tipo XSS (Cross-Site Scripting) que permite el secuestro de cuentas y el robo de cookies o sesiones.|
| AM-03 | Eliminación de temas inactivos          | SW-1 (Aplicación Web)         | S.24         | Los temas inactivos pueden tener vulnerabilidades de seguridad, y al estar fuera de uso, es más probable que no se actualicen y sus versiones presenten graves problemas de seguridad. |
| AM-04 | Módulos recomendados faltantes          | SW-1 (Aplicación Web)         | S.22         | La ausencia de los módulos recomendados, en si no representa un fallo crítico de seguridad, sin embargo, la configuración recomendada y la instalación de estos módulos permite reforzar la seguridad y el funcionamiento del sitio.  |
| AM-05 | Servidor SQL obsoleto                   | INF-1 (Datos de negocio)          | S.21         | Los datos del negocio se podrìan ver gravemente afectados ya que al tener una base de datos obsoleta, se podrían robar todos los datos que contiene.  |
| AM-06 | Falta de caché de página                | HW-1 (Servidor Ubuntu)         | A.11        | El servidor no cachea contenido, por lo que ante picos de tráfico deberá procesar cada petición desde cero, lo que puede agotar recursos y provocar caída del servicio. |

En donde los códigos de las amenazas están dados por: 
- **[S.21] Vulnerabilidades de los programas:** Uso de software obsoleto, sin actualizar o que ya no recibe parches de seguridad de sus creadores.
- **[S.22] Errores de configuración / Faltas funcionales:** Ausencia de componentes, librerías o módulos necesarios para que el sistema funcione correctamente y de forma segura.
- **[S.24] Deficiencias de mantenimiento:** Dejar instalados componentes, plugins o temas que no se usan. Esto aumenta la "superficie de ataque".
- **[A.11] Degradación del servicio:** Fallos o configuraciones pobres que hacen que el sistema vaya muy lento o pueda colapsar si recibe muchas visitas de golpe.
#### 🔴 Evaluación de Riesgos
##### 🟢 Cálculo de Probabilidad
| Ref.  | Atracción | Facilidad | Accesibilidad | Probabilidad | P. Cualitativa |
|--------|-----------|------------|---------------|--------------|----------------|
| AM-01 | 8 | 9 | 10 | 9,0 | Crítica |
| AM-02 | 9 | 8 | 10 | 9,0 | Crítica |
| AM-03 | 6 | 7 | 8  | 7,0 | Alta |
| AM-04 | 2 | 2 | 5  | 3,0 | Baja |
| AM-05 | 9 | 8 | 7  | 8,0 | Crítica |
| AM-06 | 5 | 8 | 10 | 7,7 | Alta |
##### 🟢 Cálculo de Impacto
| Ref.  | Activo Afectado | Dimensión Principal Afectada | Valor Acumulado | Degradación | Impacto |
|--------|----------------|------------------------------|-----------------|-------------|---------|
| AM-01 | SW-2 (Middleware) | I | 9 | 100% | 9.0 |
| AM-02 | SW-1 (Aplicación Web) | C | 10 | 80%  | 8.0 |
| AM-03 | SW-1 (Aplicación Web) | I | 9 | 50%  | 4.5 |
| AM-04 | SW-1 (Aplicación Web) | I | 9 | 20%  | 1.8 |
| AM-05 | INF-1 (Datos de negocio) | C | 10 | 100% | 10.0 |
| AM-06 | HW-1 (Servidor Ubuntu) | A | 8 | 70%  | 5.6 | 

##### 🟢 Cálculo de Riesgo
| Prioridad   | Ref.  | Activo Afectado              | Dimensión Principal Afectada | Degradación | Impacto | Probabilidad | Riesgo Potencial | Riesgo Cualitativo |
|-------------|-------|------------------------------|------------------------------|-------------|----------|--------------|------------------|--------------------|
| 1º Mayor    | AM-01 | SW-2 (Middleware)            | I                            | 100%        | 9.0      | 9,0          | 81.0             | Muy Alto / Crítico |
| 2º          | AM-05 | INF-1 (Datos de negocio)     | C                            | 100%        | 10.0     | 8,0          | 80.0             | Alto               |
| 3º          | AM-02 | SW-1 (Aplicación Web)        | C                            | 80%         | 8.0      | 9,0          | 72.0             | Alto               |
| 4º          | AM-06 | HW-1 (Servidor Ubuntu)       | A                            | 70%         | 5.6      | 7,7          | 43.12            | Medio              |
| 5º          | AM-03 | SW-1 (Aplicación Web)        | I                            | 50%         | 4.5      | 7,0          | 31.5             | Medio              |
| 6º          | AM-04 | SW-1 (Aplicación Web)        | I                            | 20%         | 1.8      | 3,0          | 5.4              | Bajo               |
#### 🔴 Selección de Salvaguardas
##### 🟢 Plan de Tratamiento del Riesgo
| Ref. | Hallazgo                          | Código ENS | Acción Técnica Recomendada | ¿Qué reduce? |
|------|----------------------------------|------------|----------------------------|--------------|
| AM-01 | Versión obsoleta de PHP         | [op.exp.8] Gestión de vulnerabilidades y actualizaciones     | Actualizar a versión soportada y aplicar parches de seguridad | Probabilidad |
| AM-05 | Servidor SQL obsoleto           | [op.exp.8] Gestión de vulnerabilidades y actualizaciones      | Actualizar motor de base de datos a versión soportada y parcheada | Probabilidad |
| AM-02 | Actualización de WP disponible  | [op.exp.8] Gestión de vulnerabilidades y actualizaciones      | Actualizar WordPress a la última versión estable | Probabilidad |
| AM-06 | No se ha detectado caché        | [op.pl.1] Arquitectura de seguridad      | Implementar sistema de caché | Impacto |
| AM-03 | Temas inactivos instalados      | [op.exp.2] Configuración de seguridad      | Eliminar temas no utilizados y mantener solo los necesarios | Probabilidad |
| AM-04 | Módulos recomendados faltantes   | [op.pl.1] Arquitectura de seguridad      | Instalar plugins o módulos de seguridad recomendados | Probabilidad |
##### 🟢 Plan de Tratamiento del Riesgo Residual
| Ref. | Hallazgo                          | Acción Técnica Recomendada | Eficacia (e) | Riesgo Residual  | Riesgo Residual Cualitativo |
|------|----------------------------------|----------------------------|--------------|-----------------|-----------------------------|
| AM-01 | Versión obsoleta de PHP         | Actualizar a versión soportada y aplicar parches de seguridad                      | 80%          | 16.2           | Bajo                       |
| AM-05 | Servidor SQL obsoleto           | Actualizar motor de base de datos a versión soportada y parcheada                     | 80%          | 16.0           | Bajo                       |
| AM-02 | Actualización de WP disponible   | Actualizar WordPress a la última versión estable                      | 70%          | 21.6           | Medio                       |
| AM-06 | No se ha detectado caché        | Implementar sistema de caché                      | 50%          | 21.56           | Medio                       |
| AM-03 | Temas inactivos instalados      | Eliminar temas no utilizados y mantener solo los necesarios                      | 90%          | 3.15           | Bajo                      |
| AM-04 | Faltan módulos recomendados     | Instalar plugins o módulos de seguridad recomendados                      | 100%         | 0          | Bajo                      |
### Evidencias Visuales
#### Captura 1
![](Evidencias_Visuales/Evidencia%201.png)

#### Captura 2
![](Evidencias_Visuales/Evidencia%202.png)


---
