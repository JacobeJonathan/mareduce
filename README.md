## 🗺️ Modelo MapReduce

El modelo **MapReduce** divide el procesamiento de datos en tres fases distribuidas:

> **Nota:** podemos tener varios nodos "canasta" y dentro vienen grupos "chunks" → dentro de los chunks vienen los "frames" con los datos a procesar.

---

### Estructura de entrada
Nodo (canasta)
├── Chunk 1 → [manzana, pera, palta]
├── Chunk 2 → [palta, manzana]
└── Chunk 3 → [pera, manzana, pera]

---

### Fase 1 — Función `Map`
> Cuenta los datos **localmente por nodo**.

| Nodo | manzana | pera | palta |
|------|---------|------|-------|
| Canasta 1 | 4 | 7 | 2 |
| Canasta 2 | 5 | — | — |
| Canasta 3 | 8 | 1 | — |

---

### Fase 2 — Función `Combine`
> Combina los grupos **agrupando por clave**.
> manzana: 4 + 5 + 8
> pera:    7 + 4 + 1
> palta:   2

---

### Fase 3 — Función `Reduce`
> Une todos los nodos → **resultado final global**.

| Clave | Total |
|-------|-------|
| manzana | 18 |
| pera | 15 |
| palta | 2 |

---

### Flujo completo
-> [Nodo 1] ─┐
-> [Nodo 2] ──→ MAP → COMBINE → REDUCE → resultado final
-> [Nodo 3] ─┘
