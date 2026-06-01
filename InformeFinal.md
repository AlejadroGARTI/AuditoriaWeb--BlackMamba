# Informe de Auditoría de Seguridad

---

## Cliente

- **Cliente:** Black Mamba  
- **Fecha de emisión:** 21/05/2026  
- **Auditor Jefe:** Alejandro Gutiérrez Alañón 
- **Clasificación del Documento:** CONFIDENCIAL  

---

## Resumen Ejecutivo

Este informe presenta los resultados de la auditoría de seguridad realizada sobre la infraestructura de Black Mamba. El objetivo principal ha sido identificar vulnerabilidades, evaluar riesgos y determinar el nivel de exposición de los sistemas críticos.

En términos generales, la postura de seguridad de la organización se considera: **[Crítica / Deficiente / Aceptable]**.

Durante el análisis se han identificado y evaluado **[X] hallazgos de seguridad**, de los cuales **[X] han sido clasificados como críticos o de alta severidad**.

Desde el punto de vista del impacto en el negocio, la persistencia de los riesgos críticos podría derivar en consecuencias significativas a nivel financiero, legal y reputacional. Esto incluye posibles pérdidas económicas por interrupción del servicio, sanciones regulatorias por incumplimiento normativo y daño a la confianza de clientes y socios estratégicos.

---

## Alcance y Metodología

### Sistemas evaluados
- Servidor: [Especificar servidor auditado]
- Base de datos: [Especificar base de datos]
- Aplicación: [Especificar aplicación auditada]

### Marcos normativos aplicados
- Metodología MAGERIT v3
- Controles del Esquema Nacional de Seguridad (ENS)

### Herramientas utilizadas
- [Ejemplo: Nmap]
- [Ejemplo: Nessus / OpenVAS]
- [Ejemplo: Burp Suite]
- [Ejemplo: Wireshark]
- [Ejemplo: herramientas de análisis forense y enumeración]

Estas herramientas han sido utilizadas para la recolección de evidencias técnicas, análisis de vulnerabilidades y validación de hallazgos.

---

## Top 3 Hallazgos Críticos

### Hallazgo 1

- **Nombre del Hallazgo:** 
- **Nivel de Riesgo:**  
- **Condición (Lo que es):** 
- **Criterio (Lo que debería ser):**   
- **Causa:** 
- **Consecuencia e Impacto:** 
- **Plan de Acción (Recomendación):** 

---

### Hallazgo 2

- **Nombre del Hallazgo:** 
- **Nivel de Riesgo:**  
- **Condición (Lo que es):** 
- **Criterio (Lo que debería ser):**   
- **Causa:** 
- **Consecuencia e Impacto:** 
- **Plan de Acción (Recomendación):** 

---

### Hallazgo 3

- **Nombre del Hallazgo:** 
- **Nivel de Riesgo:**  
- **Condición (Lo que es):** 
- **Criterio (Lo que debería ser):**   
- **Causa:** 
- **Consecuencia e Impacto:** 
- **Plan de Acción (Recomendación):** 

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
| AM-01 | Versión obsoleta de PHP (7.0.33-0ubuntu0.16.04.16)        | SW-2          | S.21         | Al ser una versión obsoleta del 2018 que ya no recibe parches de seguridad , se expone tanto al servidor, como a la página web a recibir ataques críticos, en donde desctacan vulnerabilidades como la inyección de Comando (CVE-2018-19518) en donde un fallo crítico en la función imap_open, permite a un atacante remoto ejecutar comandos arbitrarios en el servidor enviando un nombre de servidor IMAP manipulado. |
| AM-02 | Actualización de WordPress (7.0)        | SW-1          | S.21         | La versión actual de WordPress (6.5.8) posee múltiples vulnerabilidades, entre las que destacan una vulnerabilidad de tipo SSRF (Server-Side Request Forgery) que permite que un atacante obligue al servidor a hacer peticiones internas o externa o también una vulnerabilidad de tipo XSS (Cross-Site Scripting) que permite el secuestro de cuentas y el robo de cookies o sesiones.|
| AM-03 | Eliminación de temas inactivos          | SW-1          | S.24         | [ Ver 3.1 ]  |
| AM-04 | Módulos recomendados faltantes          | SW-1          | S.22         | [ Ver 3.1 ]  |
| AM-05 | Servidor SQL obsoleto                   | SW-2          | S.21         | [ Ver 3.1 ]  |
| AM-06 | Falta de caché de página                | SW-2          | A.11        | El servidor no cachea contenido, por lo que ante picos de tráfico deberá procesar cada petición desde cero, lo que puede agotar recursos y provocar caída del servicio. |

En donde los códigos de las amenazas están dados por: 
- **[S.21] Vulnerabilidades de los programas:** Uso de software obsoleto, sin actualizar o que ya no recibe parches de seguridad de sus creadores.
- **[S.22] Errores de configuración / Faltas funcionales:** Ausencia de componentes, librerías o módulos necesarios para que el sistema funcione correctamente y de forma segura.
- **[S.24] Deficiencias de mantenimiento:** Dejar instalados componentes, plugins o temas que no se usan. Esto aumenta la "superficie de ataque".
- **[A.11] Degradación del servicio:** Fallos o configuraciones pobres que hacen que el sistema vaya muy lento o pueda colapsar si recibe muchas visitas de golpe.
#### 🔴 Evaluación de Riesgos

#### 🔴 Selección de Salvaguardas

### Evidencias Visuales



---
