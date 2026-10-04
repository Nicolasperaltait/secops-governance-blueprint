# Caso de Estudio - El DNS que se Llevo Internet

## Contexto

El DNS interno (Pi-hole) corre en una maquina virtual del servidor y resuelve
para toda la red. El acceso remoto por malla (Tailscale) usa ese mismo DNS para
que los nombres internos funcionen desde afuera.

## Problema

Una noche el servidor se apago por un error del operador. El equipo principal
**se quedo sin internet**, no solo sin acceso a los servicios internos, con el
router y el proveedor funcionando perfecto.

## Por que importaba

El riesgo estaba registrado... como **bajo**, y con impacto "no resuelven los
nombres internos". Se materializo al dia siguiente con impacto real: **sin
internet en el equipo principal**.

## Decision, y el diagnostico que estaba mal

| Paso | Que se creyo | Que paso |
|---|---|---|
| Diagnostico 1 | el adaptador de red tenia un solo DNS | cierto, pero no era la causa |
| Mitigacion 1 | agregar un DNS secundario al adaptador; los dos resolvian | parecia resuelto |
| **Prueba de falla** | bloquear el DNS interno solo para ese equipo y pedir un nombre de internet | **fallo: el secundario nunca se consulto** |
| Causa real | la malla intercepta **todas** las consultas DNS del equipo y las manda a un unico resolver | el respaldo del adaptador era irrelevante mientras la malla corria |
| Mitigacion 2 | un segundo resolver en la configuracion de la malla, publico y sin registro | **funciona**, verificado en tres equipos |

**Por que un solo respaldo, y publico:** encadenar varios resolvers internos
suma un timeout por cada uno caido; estando fuera del sitio con el servidor
apagado, cada consulta esperaria dos timeouts. Un resolver publico funciona
igual adentro y afuera.

## Que salio mal en el camino

- **La primera mitigacion se dio por buena sin probar la falla.** Los dos DNS
  resolvian, pero eso no decia nada sobre que pasaba cuando el primero caia.
- **El riesgo se evaluo desde el proyecto equivocado**: desde el acceso remoto
  era "molesto"; desde la red completa era "sin internet".
- La mitigacion 1 **se conservo igual**: si algun dia se detiene la malla, esa
  lista vuelve a ser la que actua. Defensa en profundidad, no la solucion.

## Validacion

- Con el DNS interno bloqueado, el equipo resuelve nombres de internet.
- La correccion es de toda la malla: notebook y telefono quedaron cubiertos sin
  tocarlos.
- El arranque automatico pone el DNS primero, asi que reiniciar el servidor
  recupera todo solo.

## Resultado

| Antes | Despues |
|---|---|
| Servidor apagado = sin internet | Servidor apagado = sin servicios internos, con internet |
| Riesgo "bajo, impacto medio" | Riesgo reevaluado por impacto real, mitigado y probado |
| Mitigacion "verificada" porque resolvia | Mitigacion verificada **haciendo fallar** el primario |

## Leccion

**Un componente que el proyecto no toco puede ser el riesgo mas grande del
sistema.** Los riesgos se evaluan por su impacto real en todo el sitio, no por
su relacion con el proyecto en curso. Y una mitigacion se prueba haciendo caer
lo que mitiga.
