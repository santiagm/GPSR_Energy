
## Evaluación del impacto de potencia de transmisión en GPSR (OMNeT++/INET) con Métricas de Energía


## Resumen del proyecto

Este repositorio reproduce y extiende el escenario `manetrouting/gpsr` de INET para evaluar el impacto de parámetros físicos (especialmente potencia de transmisión) sobre el desempeño de GPSR en una red MANET.  
Además, se instrumenta y analiza el **consumo energético** usando el modelo de energía de INET (`SimpleEpEnergyStorage` + consumidor de energía de radio). 

---

## Requisitos

- **OMNeT++** (IDE + toolchain de compilación)
- **INET Framework** (ej. 4.x)
- Escenario base: `inet4.5/examples/manetrouting/gpsr` (o equivalente en tu versión)

---

## Estructura del escenario (referencia)

Archivos típicos del ejemplo:
- `GPSRNetwork.ned`
- `omnetpp.ini`
- `scenario.xml`

## Métrica 1: Energía residual vs tiempo (vector)

**Nombre (en Result Analysis):** `Residual energy capacity`

**Qué mide:** la energía restante (J) en el módulo `SimpleEpEnergyStorage` de cada nodo a lo largo del tiempo.  
En el análisis, esta curva debe verse **descendente** (consumo progresivo), y permite comparar **pendientes** entre nodos para inferir cuáles actúan más como *forwarders*. 

**Interpretación rápida:**
- Pendiente más pronunciada ⇒ mayor actividad (TX/RX + procesamiento).
- Nodos de tránsito consumen más que un emisor “ligero”. 

---

## Métrica 2: Consumo total por nodo al final de la simulación (escalar)

A partir de `Residual energy capacity`, se reporta un resumen por nodo:

\[
E_{\text{consumo}} = E_{\text{inicial}} - E_{\text{final}}
\]

En el reporte se muestra un ejemplo tras **360 s**:

| Nodo   | Energía Inicial (J) | Energía Final (J) | Consumo Total (J) |
|--------|----------------------|-------------------|-------------------|
| Host 0 | 50.0000              | 48.7565           | 1.2435            |
| Host 10| 50.0000              | 47.9116           | 2.0884            |

**Lectura clave:** `Host 10` consume más porque actúa como nodo de reenvío central (forwarder), manejando más tráfico y beacons que el emisor. 

