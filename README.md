---
title: "Evaluación del impacto de potencia de transmisión en GPSR (OMNeT++/INET) con Métricas de Energía"
author: "Mateo Eduardo Bermeo Pesantez, Santiago Andrés Guillén Malla, Vicente Paul Jiménez Ávila"
output: github_document
---

## Resumen del proyecto

Este repositorio reproduce y extiende el escenario `manetrouting/gpsr` de INET para evaluar el impacto de parámetros físicos (especialmente potencia de transmisión) sobre el desempeño de GPSR en una red MANET.  
Además, se instrumenta y analiza el **consumo energético** usando el modelo de energía de INET (`SimpleEpEnergyStorage` + consumidor de energía de radio). :contentReference[oaicite:1]{index=1}

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

(En el reporte se usa este ejemplo como base). :contentReference[oaicite:2]{index=2}

---

## Ejecución rápida

1. Compila en modo release (recomendado para barridos largos):
   ```bash
   make MODE=release
