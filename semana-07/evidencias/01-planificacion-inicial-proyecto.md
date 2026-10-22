# Planificación Inicial de Proyecto Tecnológico: HospitaLink-Secure
### Simulación de Red Hospitalaria Segmentada con VLANs y Políticas de Seguridad en GNS3

**Universidad de las Fuerzas Armadas – ESPE**  
**Departamento de Ciencias Exactas / Ingeniería en Tecnologías de la Información**  
**Programa de Preparación para Oportunidades CERN 2026 (PREP CERN)**  
**Módulo 7:** Sprint Técnico y Gestión Ágil de Proyectos

---

### Ficha Técnica de la Planificación

| Parámetro Institucional | Especificación Técnica |
| :--- | :--- |
| **Estudiante / Proponente:** | Angeles Julieth Zambrano Bravo |
| **Identificación Digital / GitHub:** | [@ajzambrano12-cloud](https://github.com/ajzambrano12-cloud) |
| **Programa Académico:** | Ingeniería en Tecnologías de la Información (4.° Semestre) — ESPE |
| **Asignatura / Actividad:** | CERN / Evidencia 1 — Planificación Inicial de un Proyecto Tecnológico |
| **Marco Metodológico:** | Metodologías Ágiles de Gestión de Proyectos (*Atlassian Agile Guide / Scrum*) |
| **Período de Planificación:** | Octubre de 2026 (Semana 07) |
| **Sede:** | Sangolquí, Ecuador |

---

> ### Resumen Ejecutivo
> El presente documento detalla la planificación inicial del proyecto tecnológico **HospitaLink-Secure**, enfocado en el diseño, simulación y securización de la infraestructura de red de un centro hospitalario de mediana complejidad mediante el entorno de emulación **GNS3**. El proyecto aborda la vulnerabilidad crítica de los registros médicos y el tráfico asistencial mediante una arquitectura de red jerárquica con segmentación lógica en cuatro VLANs independientes: **Urgencias, Laboratorio, Farmacia y Administración/Servidores de Pacientes**. A través de una metodología ágil iterativa de 6 semanas, se establecen el objetivo, la delimitación de alcance (*In-Scope* vs. *Out-of-Scope*), tres hitos medibles, la distribución de responsabilidades técnicas, la mitigación de riesgos de sobrecarga de CPU y filtrado erróneo de tráfico médico, y un *roadmap* secuencial en cuatro fases.

---

## 1. Nombre del Proyecto

**HospitaLink-Secure: Simulación y Segmentación de Red Hospitalaria con VLANs y Políticas de Seguridad en GNS3**

* **Acrónimo / Identificador:** `HospitaLink-Secure`
* **Tipo de proyecto:** Simulación de Infraestructura de Redes y Ciberseguridad en Salud (*Networking & Healthcare Security*).

---

## 2. Objetivo del Proyecto

### 2.1. Objetivo General
Diseñar y simular en el entorno GNS3 una topología de red modular, jerárquica y de alta disponibilidad para un entorno hospitalario, implementando segmentación lógica mediante VLANs para las áreas de **Urgencias, Laboratorio, Farmacia y Administración**, junto con políticas estrictas de control de acceso (Listas de Control de Acceso - ACLs) que garanticen el aislamiento de tráfico sensible y la protección de los datos de los pacientes conforme a buenas prácticas de seguridad de la información.

### 2.2. Objetivos Específicos
1. **Segmentación departamental:** Diseñar un plan de direccionamiento IPv4 estructurado con máscaras de longitud variable (VLSM) y configurar cuatro VLANs independientes (VLAN 10: Urgencias, VLAN 20: Laboratorio, VLAN 30: Farmacia, VLAN 40: Administración y Servidor de Historias Clínicas) en switches Cisco enlazados mediante troncales 802.1Q.
2. **Control de acceso y seguridad perimetral:** Configurar enrutamiento inter-VLAN seguro y desplegar Listas de Control de Acceso (ACLs extendidas) en el router principal para restringir estrictamente qué dispositivos pueden consultar los registros clínicos de los pacientes, impidiendo accesos cruzados no autorizados.
3. **Servicios de red y validación de tráfico:** Desplegar direccionamiento dinámico por subred mediante un servidor DHCP segmentado y auditar el comportamiento del tráfico mediante capturas de paquetes con Wireshark en GNS3, verificando el bloqueo efectivo de accesos indebidos.

---

## 3. Alcance del Proyecto (Scope Management)

Para asegurar la ejecución exitosa del proyecto dentro de un marco temporal ágil y con recursos computacionales locales, se delimita claramente lo que incluye y excluye el trabajo:

| Componente | Qué INCLUIRÁ el Proyecto (In-Scope) | Qué QUEDARÁ FUERA del Proyecto (Out-of-Scope) |
| :--- | :--- | :--- |
| **Entorno de Red** | Simulación completa en **GNS3** con routers Cisco (IOSv / c7200) y switches de capa 2/3. | Implementación física con cableado estructurado, canaletas o racks en un hospital real. |
| **Segmentación Lógica** | 4 VLANs departamentales: Urgencias (prioritaria), Laboratorio (diagnóstico), Farmacia (stock/recetas) y Administración (gestión y datos clínicos). | Redes inalámbricas complejas de invitados (WiFi de sala de espera con portal cautivo comercial). |
| **Enrutamiento y Servicios** | Enrutamiento inter-VLAN mediante Router-on-a-Stick / switch multicapa, y servidor DHCP modular por subred. | Protocolos de enrutamiento dinámico exterior como BGP o MPLS hacia sucursales remotas. |
| **Políticas de Seguridad** | Listas de Control de Acceso (ACLs estándar y extendidas) para restringir puertos TCP/UDP específicos hacia el servidor de historias clínicas. | Adquisición o licenciamiento de Firewalls de Próxima Generación comerciales de pago (Fortinet/Palo Alto). |
| **Validación y Entrega** | Pruebas de conectividad ICMP (ping, traceroute), auditoría de paquetes con Wireshark y archivo empaquetado `.gns3project`. | Desarrollo o programación de un software de historias clínicas electrónicas (EHR/EMR de producción). |

---

## 4. Hitos Principales del Proyecto (Milestones)

El avance del proyecto se estructura en tres hitos principales que representan logros técnicos entregables:

| Hito | Nombre del Hito | Plazo Estimado | Entregable Clave Verificable | Criterio de Éxito Técnico |
| :---: | :--- | :---: | :--- | :--- |
| **Hito 1** | **Topología Base y Esquema de Direccionamiento** | Semanas 1 – 2 | Diagrama de red en GNS3 y tabla de direccionamiento VLSM documentada. | Topología cargada en GNS3 con switches y routers interconectados y direccionamiento asignado sin solapamientos. |
| **Hito 2** | **Segmentación por VLANs y Servicios DHCP** | Semanas 3 – 4 | Proyecto GNS3 con VLANs 10, 20, 30 y 40 operativas y DHCP activo por subred. | Terminales de cada área obtienen IP automática en su segmento y existe aislamiento de broadcast verificado. |
| **Hito 3** | **Políticas de Seguridad (ACLs), Auditoría y Release** | Semanas 5 – 6 | Configuración de ACLs extendidas, capturas de Wireshark y reporte final. | Bloqueo exitoso de accesos desde Farmacia y Urgencias al servidor de pacientes; comunicación autorizada fluida. |

---

## 5. Asignación de Roles y Responsabilidades

Para simular un equipo ágil de ingeniería de TI, las tareas se distribuyen entre roles técnicos especializados:

### 5.1. Tareas asumidas por Angeles Zambrano (Líder del Proyecto & Especialista en Redes e Infraestructura)
* **Diseño y Dimensionamiento de Red:** Cálculo de subredes IPv4 con VLSM y arquitectura de red jerárquica en GNS3.
* **Configuración de la Capa de Conmutación:** Creación de VLANs en switches Cisco, asignación de puertos de acceso y configuración de enlaces troncales IEEE 802.1Q.
* **Enrutamiento y Servicios Centrales:** Configuración del enrutamiento inter-VLAN (subinterfaces en router) y pools DHCP segmentados.
* **Control de Versiones y Documentación:** Versionado de las configuraciones Cisco (`running-config`) en GitHub y consolidación del informe técnico final.

### 5.2. Tareas asignadas a Colaboradores Técnicos
* **Colaborador 1 — Especialista en Ciberseguridad y Políticas de Acceso:**
  * Definición de la matriz de flujo de tráfico permitido y denegado entre las distintas áreas hospitalarias.
  * Diseño e implementación de Listas de Control de Acceso (ACLs extendidas) en el router para blindar la base de datos de pacientes.
  * Análisis de tráfico y verificación de reglas mediante capturas con Wireshark en los enlaces troncales.
* **Colaborador 2 — Documentador Técnico & Analista de Procesos Hospitalarios:**
  * Levantamiento de los requerimientos de comunicación del personal médico (Urgencias requiriendo resultados de Laboratorio).
  * Elaboración de la memoria técnica de la topología con diagramas descriptivos de direccionamiento y pruebas de estrés.
  * Pruebas de contingencia y verificación del comportamiento de la red ante desconexión de enlaces.

---

## 6. Gestión de Riesgos Técnicos y Mitigación

Se identifican las dos principales dificultades operativas del proyecto y sus respectivas estrategias de mitigación proactiva:

### Riesgo 1: Saturación de Recursos (CPU y RAM) del Computador Anfitrión en GNS3
* **Descripción de la dificultad:** Al emular simultáneamente múltiples routers Cisco IOS y switches virtuales junto con varias máquinas cliente, el simulador GNS3 puede sobrecargar la CPU del host al 100%, ralentizando el sistema o provocando cierres inesperados.
* **Probabilidad:** Alta | **Impacto:** Alto.
* **Estrategia de mitigación:**  
  1. Configurar adecuadamente el valor de **`Idle-PC`** para cada imagen de router Cisco IOS en GNS3 para reducir el uso de CPU al mínimo cuando no haya tráfico activo.
  2. Emplear nodos ligeros como **VPCS (Virtual PC Simulator)** para los clientes de prueba en cada departamento médico, reservando máquinas virtuales más pesadas únicamente para el servidor central de pacientes.
  3. Dimensionar la topología con el número óptimo de switches virtuales sin redundancias innecesarias en la fase de prototipo.

### Riesgo 2: Configuración Errónea de ACLs que Interrumpa el Flujo de Datos Médicos Críticos
* **Descripción de la dificultad:** Al aplicar reglas restrictivas de seguridad mediante ACLs en el router, una regla mal posicionada o la regla implícita `deny all` al final de la lista podría bloquear accidentalmente comunicaciones vitales (por ejemplo, el envío urgente de resultados de hemogramas desde el Laboratorio hacia la estación de Urgencias).
* **Probabilidad:** Media | **Impacto:** Crítico.
* **Estrategia de mitigación:**  
  1. Diseñar y validar previamente una **matriz de control de tráfico (origen-destino-protocolo-puerto)** en hoja de cálculo antes de ingresar comandos en la CLI de Cisco.
  2. Aplicar las ACLs de forma incremental y controlada, utilizando el comando `show access-lists` para monitorear los contadores de coincidencias (*hits*) de cada regla.
  3. Ejecutar pruebas de conectividad bidireccional (ping y telnet/curl a puertos específicos) tras cada modificación de política de seguridad.

---

## 7. Roadmap y Secuencia Temporal de Ejecución

El proyecto se desarrolla a lo largo de un ciclo ágil de 6 semanas, dividido en cuatro fases secuenciales:

| Fase Metodológica | Período | Actividades Principales de la Fase | Hito Vinculado |
| :---: | :---: | :--- | :--- |
| **Fase 1: Planificación y Diseño Lógico** | Semana 1 | • Levantamiento de requerimientos de red hospitalaria.<br>• Diseño del direccionamiento IPv4 con VLSM.<br>• Creación del proyecto en GNS3 e importación de appliances Cisco. | Topología base y plan de direccionamiento aprobado. |
| **Fase 2: Conmutación y Servicios** | Semana 2 | • Creación y etiquetado de VLANs (10, 20, 30, 40).<br>• Configuración de enlaces troncales 802.1Q.<br>• Configuración de servidor DHCP con exclusiones y pools por área. | **Hito 1:** Topología base operativa y direccionamiento funcional. |
| **Fase 3: Enrutamiento y Políticas de Seguridad** | Semanas 3 – 4 | • Enrutamiento inter-VLAN mediante subinterfaces en el router.<br>• Redacción e implementación de ACLs extendidas para protección de pacientes.<br>• Pruebas de aislamiento entre VLAN de Farmacia y Administración. | **Hito 2:** Segmentación por VLANs y control de acceso implementado. |
| **Fase 4: Auditoría, Pruebas y Release** | Semanas 5 – 6 | • Inspección de paquetes con Wireshark ante intentos de intrusión simulada.<br>• Documentación de configuraciones y resolución de incidencias.<br>• Empaquetado del proyecto `.gns3project` y entrega del reporte técnico. | **Hito 3:** Proyecto validado, documentado y listo para despliegue. |

---

## 8. Fundamentación Metodológica y Conexión con el Perfil de TI

1. **Alineación con la Gestión Ágil de Proyectos:**  
   Se utiliza el enfoque de entregas tempranas y frecuentes: en lugar de esperar al final para verificar la seguridad, la red se valida incrementalmente (primero conectividad de capa 2 en el Hito 1, luego enrutamiento en el Hito 2, y finalmente seguridad y auditoría en el Hito 3).
2. **Transferencia Práctica a la Formación Profesional:**  
   Este proyecto pone en práctica las habilidades de soporte técnico, administración de redes locales y fundamentos de ciberseguridad adquiridas en la carrera de Ingeniería en TI y en la pasantía en la Policía Nacional, demostrando la capacidad de estructurar soluciones tecnológicas seguras en sectores críticos como el de la salud.
