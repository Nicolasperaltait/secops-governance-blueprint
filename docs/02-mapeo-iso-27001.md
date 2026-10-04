# Mapeo ISO/IEC 27001:2022 - Anexo A

> Estado descrito: octubre de 2026.

## Para que sirve este mapeo

Muestra que controles del **Anexo A de ISO/IEC 27001:2022** cubre la operacion
de esta infraestructura, con que, y **como se demuestra**. No es una
certificacion: es el ejercicio de pensar la operacion diaria con el lenguaje de
un sistema de gestion de seguridad de la informacion (SGSI).

Criterio de estado:

| Estado | Significado |
|---|---|
| **Implementado** | el control existe, opera y tiene evidencia |
| **Parcial** | existe, pero falta cobertura o formalizacion |
| **No aplica** | no corresponde a una infraestructura de una sola persona |

## Resumen

| Tema del Anexo A | Controles mapeados | Implementados | Parciales |
|---|---|---|---|
| 5 - Organizacionales | 9 | 6 | 3 |
| 8 - Tecnologicos | 15 | 13 | 2 |
| **Total** | **24** | **19** | **5** |

Los temas 6 (personas) y 7 (fisicos) se omiten: con un solo operador y un
servidor domestico no tienen una lectura honesta.

## 5 - Controles organizacionales

| Control | Como se cubre | Evidencia | Estado |
|---|---|---|---|
| 5.1 Politicas de seguridad | politica de seguridad y secretos, reglas de publicacion y gobernanza por repositorio | documentos versionados y revisados | Implementado |
| 5.9 Inventario de activos | inventario de maquinas, servicios y dependencias | inventario versionado | Implementado |
| 5.15 Control de acceso | deny por defecto en la malla, permisos por puerto | politica como codigo con pruebas propias | Implementado |
| 5.17 Informacion de autenticacion | claves por equipo, gestor de contrasenas autoalojado, credenciales fuera de los repositorios | revision de repos sin secretos | Implementado |
| 5.18 Derechos de acceso | cuentas en desuso retiradas con el orden reemplazo, prueba, retiro | registro de cada retiro | Implementado |
| 5.24 Planificacion de la gestion de incidentes | incidentes documentados con causa raiz, mitigacion y leccion | registro de incidentes | Implementado |
| 5.26 Respuesta a incidentes | runbooks y via de rescate por consola verificada | rescate probado | Parcial |
| 5.29 Seguridad durante una interrupcion | arranque por dependencias y resolucion DNS de respaldo | prueba con el DNS interno caido | Parcial |
| 5.30 Preparacion TIC para la continuidad | backups por dominio, copia externa cifrada, restauracion probada | RTO y RPO medidos en cada prueba | Parcial |

## 8 - Controles tecnologicos

| Control | Como se cubre | Evidencia | Estado |
|---|---|---|---|
| 8.2 Derechos de acceso privilegiado | ningun permiso privilegiado generico; lista medida para los agentes de IA | lector generico e interprete **denegados** | Implementado |
| 8.5 Autenticacion segura | SSH solo por clave; nodos firmantes en la malla | configuracion **efectiva** verificada en cada host | Implementado |
| 8.7 Proteccion contra malware | integridad de archivos y analisis de reputacion desde el SIEM | alertas del SIEM | Implementado |
| 8.8 Gestion de vulnerabilidades tecnicas | deteccion de vulnerabilidades del SIEM y parcheo automatico | metrica de parches pendientes | Parcial |
| 8.9 Gestion de la configuracion | configuracion y gobernanza versionadas en un remoto propio | historial de cambios | Implementado |
| 8.13 Copias de seguridad | backups nocturnos por dominio, copia externa cifrada, estrategia en frio | metrica de edad del **contenido** | Implementado |
| 8.15 Registro de eventos | SIEM con agentes en hosts y estacion de trabajo; auditoria del sistema | eventos consultables | Implementado |
| 8.16 Monitoreo de actividades | metricas, sondas y alertas solo de fallas | canal de alertas con destino verificado | Implementado |
| 8.20 Seguridad de redes | cero puertos entrantes; firewall por host | contadores de descarte por politica | Implementado |
| 8.21 Seguridad de los servicios de red | DNS interno con filtrado y proxy inverso | consultas y bloqueos medidos | Implementado |
| 8.22 Segregacion de redes | zonas por funcion: administracion, servicios, seguridad | flujos entre zonas minimos y documentados | Parcial |
| 8.23 Filtrado web | resolucion con listas de bloqueo para toda la red | porcentaje de consultas bloqueadas | Implementado |
| 8.24 Uso de criptografia | malla cifrada de extremo a extremo; copia externa cifrada | configuracion de cada canal | Implementado |
| 8.25 Ciclo de vida de desarrollo seguro | integracion continua en cada commit; pruebas de lo que tiene que fallar | corridas de CI | Implementado |
| 8.32 Gestion de cambios | cambios con plan, respaldo previo, rollback y validacion | registro de cada cambio sensible | Implementado |

## Como se lee

- **Un control sin evidencia se marca parcial**, aunque la herramienta este
  instalada. Instalar no es controlar.
- Los parciales tienen direccion definida; no se publican los detalles de que
  falta para no entregar un mapa de huecos.
- La evidencia vive en la documentacion privada; aca se publica que existe y
  como se obtiene.

## Relacion con la experiencia laboral

El mismo criterio se aplica en entornos corporativos gestionados bajo ISO 27001:
la diferencia entre "tener el control" y "poder demostrarlo" es la que hace
pasar una auditoria.
