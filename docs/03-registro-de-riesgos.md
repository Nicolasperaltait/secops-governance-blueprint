# Registro de Riesgos

> Estado descrito: octubre de 2026. Version publica: solo riesgos **mitigados** o
> **aceptados con motivo**. Los riesgos abiertos se gestionan en privado.

## Metodo

| Paso | Que se hace |
|---|---|
| Identificar | cada incidente, cambio o relevamiento puede abrir un riesgo |
| Evaluar | probabilidad e impacto **sobre todo el sitio**, no sobre el proyecto en curso |
| Tratar | mitigar, aceptar con motivo escrito, o eliminar |
| Verificar | la mitigacion se prueba **haciendo caer lo que mitiga** |
| Revisar | un riesgo que se materializa obliga a revisar como se habia evaluado |

Escala: probabilidad e impacto en **Baja / Media / Alta**.

## Riesgos tratados

| ID | Riesgo | Evaluacion inicial | Evaluacion real | Tratamiento | Estado |
|---|---|---|---|---|---|
| R-01 | Unico resolver DNS para toda la red | Baja / Media | **Alta / Alta**: se materializo al dia siguiente | resolver de respaldo en toda la malla, probado con el primario caido | Mitigado |
| R-02 | Exposicion del borde por acceso remoto | Media / Alta | - | malla sin puertos entrantes, politica por puerto, tailnet lock | Mitigado |
| R-03 | Agente de IA con privilegio excesivo | Media / Alta | - | host de salto unico con interruptor manual; permisos medidos | Mitigado |
| R-04 | Backup que informa exito sobre contenido viejo | Baja / Alta | **Alta / Alta**: casi 4 meses sin detectar | metrica por edad del contenido, con alerta | Mitigado |
| R-05 | Copia externa que falla sin avisar | Baja / Alta | **Media / Alta**: varios dias sin alerta | aviso enganchado a la salida del proceso | Mitigado |
| R-06 | Disco lleno por snapshots olvidados | Media / Media | se dio dos veces | todo snapshot nace con fecha de retiro | Mitigado |
| R-07 | Perder acceso a un host al retirar una credencial | Media / Alta | se dio dos veces | regla: el reemplazo se prueba antes de retirar; el script se niega si no | Mitigado |
| R-08 | Controles que informan exito sin haber actuado | Baja / Alta | **Alta / Alta**: siete casos en una semana | verificar el efecto y lo que tiene que fallar | Mitigado |
| R-09 | Perdida del sitio completo con el codigo adentro | Baja / Alta | - | clones en otra maquina, backup de la VM, estrategia de copia en frio | Mitigado parcialmente |
| R-10 | Dependencia de un unico hipervisor | Baja / Alta | - | aceptado: restauracion documentada y probada; un segundo nodo no se justifica a esta escala | Aceptado |

## Lo que muestra esta tabla

- **La columna mas importante es "Evaluacion real".** Cuatro riesgos estaban
  subestimados y se corrigieron despues de materializarse. Registrarlo es lo que
  vuelve util al registro.
- **Aceptar un riesgo es una decision, no un olvido**: R-10 esta aceptado con
  motivo escrito.
- Ningun riesgo se cierra sin una prueba que demuestre la mitigacion.
