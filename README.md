# CENFONET: Proyecto de red WAN
---

<img width="284" height="78" alt="Imagen para markdown" src="https://github.com/user-attachments/assets/66e32529-6cec-4cac-823d-dbd5145a9152" />
<img width="286" height="99" alt="Imagen Cisco para markdown" src="https://github.com/user-attachments/assets/0e4fa8a1-34e5-44de-92df-4a3ae18ff419" />
<img width="249" height="46" alt="Imagen MIT markdown" src="https://github.com/user-attachments/assets/ffed0d9f-1048-44b8-89ad-5b480ea479aa" />

# Descripción del Proyecto
CENFONET es un proyecto académico de diseño e implementación de una red WAN (Wide Area Network) empresarial desarrollado como parte del curso de Fundamentos de Redes en UCENFOTEC.
El proyecto simula la infraestructura de red que podria utilizar la universidad Cenfotec para brindar todos sus servicios, que requiere interconectar 4 sedes ubicadas en diferentes pisos de un edificio corporativo mediante enlaces de fibra óptica.

# ¿Qué es CENFONET?
CENFONET es el nombre que elegimos para este proyecto de red, haciendo referencia a:

- CENFO: Abreviatura de UCENFOTEC

- NET: Network (Red)

El nombre representa la conexión entre el conocimiento adquirido en la institución educativa y su aplicación práctica en el diseño de redes empresariales.

---

# Objetivos del Proyecto
## Objetivos Académicos
Como proyecto del curso de Fundamentos de Redes, este trabajo busca demostrar:

- ✅ Comprensión de subnetting y VLSM (Variable Length Subnet Masking)
- ✅ Configuración de rutas estáticas en routers Cisco
- ✅ Diseño de topologías WAN con redundancia física
- ✅ Implementación de enlaces de fibra óptica
- ✅ Uso de Cisco Packet Tracer para simulación de redes
- ✅ Documentación técnica profesional
- ✅ Análisis de costos de implementación

## Objetivos Técnicos

- Interconectar 4 LANs mediante una red WAN
- Garantizar conectividad completa entre todas las sedes
-  Optimizar el uso de direcciones IP mediante VLSM
-  Implementar redundancia física en la topología
-  Configurar seguridad básica (SSH, contraseñas encriptadas)
-  Proporcionar escalabilidad para crecimiento futuro

---

# Topología de Red

<img width="1329" height="840" alt="Screenshot 2025-11-25 194352" src="https://github.com/user-attachments/assets/29bfcd1f-2491-4d7e-8c99-41aa724deeff" />

## ¿Por qué topología en anillo?
Elegimos esta topología por las siguientes razones:

Ventajas

- Redundancia física: Existen al menos 2 rutas entre cualquier par de routers
- No hay punto único de falla: Ningún router es crítico para la conectividad general
- Balance costo/beneficio: Solo 4 enlaces de fibra vs 6 en topología de malla completa (ahorro del 33%)
- Escalabilidad: Fácil agregar nuevos sitios sin rediseñar toda la red
- Distribución de carga: El tráfico puede usar múltiples caminos

Consideraciones

- Con rutas estáticas básicas, no hay failover automático
- Requiere intervención manual del administrador si un enlace falla
- La redundancia es física pero no automática en esta implementación

---

# Características Técnicas
Tecnologías Implementadas

- Simulador: Cisco Packet Tracer
- Routers: Cisco 1941 (4 unidades)
- Switches: Cisco Catalyst 2960-24TT (4 unidades)
- Medio WAN: Fibra óptica
- Medio LAN: Cable de cobre (Ethernet)
- Protocolo de enrutamiento: Rutas estáticas
- Esquema de direccionamiento: IPv4 con VLSM
- Seguridad: SSH, contraseñas encriptadas, banners

### Plan de Direccionamiento IP

Red Base: 172.16.0.0/16 (Red Privada Clase B)

--- 

# Asignación de Puertos

### RT_TercerPiso

- G0/0: LAN (Switch Labz)
- G0/1/0: WAN hacia RT_Auditorio
- G0/0/0: WAN hacia RT_SegundoPiso

### RT_Auditorio_MakerSpace

- G0/0: LAN (Switch Auditorio)
- G0/1/0: WAN hacia RT_TercerPiso
- G0/0/0: WAN hacia RT_PrimerPiso

### RT_PrimerPiso

- G0/0: LAN (Switch Laboratorio)
- G0/1/0: WAN hacia RT_Auditorio
- G0/0/0: WAN hacia RT_SegundoPiso

### RT_SegundoPiso

- G0/0: LAN (Switch Administración)
- G0/1/0: WAN hacia RT_TercerPiso
- G0/0/0: WAN hacia RT_PrimerPiso

# Scripts de configuración y subneteo

Esta información se encuentra en la carpeta /docs. Ahi se puede encontrar el trabajo escrito que se realizó para lograr el proyecto como toda la parte del subneteo realizado, oferta económica de la solución, scripts de configuración y datos importantes para tomar en cuenta.

---

# Instalación y Uso
## Opción 1: Cargar el archivo .pkt directamente
1. Clona este repositorio:
```bash
git clone https://github.com/FabianVargasH/CENFONET---Proyecto-de-Red-WAN-Empresarial.git
cd CENFONET
```
2. Abre Cisco Packet Tracer
3. Carga el archivo de topología:
```bash
File → Open → packet-tracer/CENFONET_Topology.pkt
```
4. Listo, ya tiene la red lista para pruebas
---

## Opción 2: Configurar desde cero
Si desea aprender configurando manualmente:
### Paso 1: Crear la topología física

1. Abre Packet Tracer
2. Agrega 4 routers Cisco 1941
3. Agrega 4 switches Cisco 2960-24TT
4. Agrega 8 PCs (2 por cada LAN)

### Paso 2: Conectar los dispositivos

- Conexiones LAN (Cable Copper Straight-Through):

  - Cada router (puerto G0/0) → Switch correspondiente
  - Cada switch → 2 PCs

- Conexiones WAN (Cable Fiber):

  - RT_TercerPiso G0/1/0 ↔ RT_Auditorio G0/1/0
  - RT_TercerPiso G0/0/0 ↔ RT_SegundoPiso G0/1/0
  - RT_Auditorio G0/0/0 ↔ RT_PrimerPiso G0/1/0
  - RT_SegundoPiso G0/0/0 ↔ RT_PrimerPiso G0/0/0

### Paso 3: Configurar los dispositivos

Todo el contenido de los scripts, configuraciones de la IP de las PC, está en la carpeta de /docs

---

# Configuración de Dispositivos

## Credenciales de Acceso

- Routers y Switches:
  - Enable Secret: CLASS12345
  - Console Password: CISCO12345
  - VTY Password: CISCO12345
  - SSH Username: ADMIN
  - SSH Password: ADMIN12345

- Switches (adicional):

  - Username: Admin
  - Password: Admin12345

---

#  Pruebas de Conectividad

### Pruebas Básicas
1. Conectividad local (misma LAN)

```cisco
PC0> ping 172.16.1.129    # Gateway
PC0> ping 172.16.1.179    # Otro host en misma LAN
```
2. Conectividad WAN (entre LANs)
```cisco
PC0> ping 172.16.1.2      # PC en Auditorio
PC0> ping 172.16.1.194    # PC en Primer Piso
PC0> ping 172.16.1.226    # PC en Segundo Piso
```
3. Trazar ruta
```cisco
PC0> tracert 172.16.1.226
```

### Resultados Esperados
#### Todos los pings deben ser exitosos con:

- Reply from [IP]: bytes=32
- Time: <10ms (LAN) o <50ms (WAN)
- TTL: 128 (hosts) o 254-126 (a través de routers)
- Success rate: 100% (5/5)

#### Si hay fallas:

- Verificar configuración de IPs
- Verificar estado de interfaces (show ip interface brief)
- Verificar rutas estáticas (show ip route)
- Revisar cables físicos en Packet Tracer
---

# Documentación Técnica

Como ya fue mencionado, toda la documentación técnica detallada se encuentra en la carpeta docs/:

- Tablas de Subneteo: Direccionamiento completo
- Rutas Estáticas: Todas las rutas configuradas
- Configuración de PCs: IPs de hosts
- Scripts de configuración

# Limitaciones Conocidas

## Limitaciones Técnicas

- No hay failover automático: Con rutas estáticas básicas, si un enlace falla, se requiere intervención manual para activar rutas alternativas.
- Balanceo de carga impredecible: Con múltiples rutas estáticas de igual métrica, el router puede alternar entre ellas de forma no determinística.
- Escalabilidad de configuración: Agregar nuevas sedes requiere actualizar rutas estáticas en TODOS los routers manualmente.
- Sin QoS implementado: No hay priorización de tráfico crítico sobre tráfico de menor importancia.

## Limitaciones del Simulador

- Packet Tracer no simula 100% de funcionalidades: Algunas características avanzadas de IOS no están disponibles.
- Sin tráfico real: La simulación no genera carga de red realista.
- Desempeño limitado: El simulador puede ser lento con topologías muy grandes.

---

# Autores

## Proyecto CENFONET

Curso: Fundamentos de Redes

Institución: UCENFOTEC

Año: 2025

Instructor: Marco Ney Jiménez Quesada

## Desarrollado por:

Fabián Vargas Hidalgo

David Rivera Valladares

Correo: fabianvh2506@gmail.com

GitHub: FabianVargasH

---

# Estado del Proyecto

- [x] Diseño de topología
- [x] Plan de direccionamiento VLSM
- [x] Configuración de routers
- [x] Configuración de switches
- [x] Pruebas de conectividad
- [x] Documentación técnica
- [x] Análisis de costos

Última actualización: Noviembre 2025

---

# Agradecimientos

- UCENFOTEC por proporcionar los recursos educativos y acceso a Cisco Networking Academy
- Cisco Networking Academy por Packet Tracer y materiales de estudio
- Comunidad de redes por la documentación y recursos de aprendizaje
- Compañeros de clase por las sesiones de estudio y colaboración

---

# Licencia

Este proyecto contiene una licencia, favor revisarla y tomarla en cuenta
