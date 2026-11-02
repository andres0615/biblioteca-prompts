---
name: simple-syntax
description: Escribe código con sintaxis sencilla, legible y fácil de entender. Úsala cuando generes código nuevo o refactorices código existente para priorizar claridad sobre brevedad, reducir anidamiento y evitar construcciones complejas, ingeniosas o inline.
license: MIT
metadata:
  audience: developers
  workflow: coding
---

## Qué hago

Escribo y modifico código priorizando la **claridad**, la **legibilidad** y la **facilidad de mantenimiento** por encima de la brevedad o la "elegancia" excesiva. El objetivo es que cualquier desarrollador (humano o agente) pueda entender el código sin esfuerzo.

## Cuándo usarme

Úsame cuando:

- Generes código nuevo desde cero.
- Refactorices o modifiques código existente.
- El código funcione pero sea difícil de leer, mantener o extender.
- Detectes lógica demasiado anidada, nombres poco descriptivos, construcciones complejas o código inline difícil de seguir.

No me uses para:

- Micro-optimizaciones de rendimiento que sacrifiquen legibilidad.
- Cambiar el comportamiento observable del código (a menos que se pida explícitamente).
- Reescrituras masivas fuera del alcance de la tarea actual.

## Principios

### 1. Claridad sobre brevedad

El código explícito y legible es preferible al código compacto o "clever". Evita:

- One-liners densos que hacen varias cosas a la vez.
- Ternarios anidados o encadenados.
- Expresiones comprimidas que obligan a detenerse a descifrarlas.

### 2. Reduce el anidamiento

- Prefiere **early returns** (cláusulas de guarda) en lugar de bloques `if` profundamente anidados.
- Extrae condiciones complejas a variables con nombres descriptivos.
- Si un bloque supera 3 niveles de indentación, considera extraerlo a una función auxiliar.

### 3. Funciones pequeñas y con un solo propósito

- Mantén las funciones cortas y enfocadas en una sola responsabilidad.
- Si una función hace más de una cosa, divídela.
- El nombre de la función debe describir exactamente lo que hace.

### 4. Nombres descriptivos y explícitos

- Usa nombres que revelen la intención: `userList` en lugar de `ul`, `calculateTotal` en lugar de `calc`.
- Evita abreviaturas ambiguas y nombres de una sola letra (salvo contadores de bucle muy locales, como `i`, `j`).
- Los nombres deben poder leerse en voz alta y entenderse sin contexto adicional.

### 5. Estructuras de control simples

- Usa `if/else` claros antes que estructuras anidadas o combinaciones de operadores ternarios.
- Prefiere `switch` o `match` cuando haya múltiples ramas mutuamente excluyentes.
- Evita bucles con lógica compleja dentro; extrae el cuerpo del bucle a una función si es necesario.

### 6. Evita construcciones "ingeniosas"

- No uses trucos de lenguaje que ahorren líneas a costa de claridad.
- No encadenes múltiples operaciones en una sola línea si eso oculta el flujo de datos.
- No uses destructuring excesivo si hace perder el contexto de los objetos.

### 7. Comentarios solo cuando aporten valor

- No comentes lo obvio.
- Comenta solo bloques no evidentes, decisiones de diseño o "porqués" que el código no puede expresar por sí solo.

### 8. Evita el código inline complejo

No escribas expresiones inline que combinen varias operaciones, llamadas o condiciones en una sola línea si eso dificulta la lectura. En su lugar, **descompón en pasos explícitos** asignando resultados intermedios a variables con nombres claros.

**Evita específicamente:**

- ❌ Llamadas a funciones anidadas en línea: `foo(bar(baz(x)))`
- ❌ Cadenas largas de métodos sin separación visual: `arr.filter(...).map(...).reduce(...).sort(...)`
- ❌ Condiciones inline con múltiples operadores lógicos y llamadas: `if (a && b(x) || c?.d && e(f))`
- ❌ Ternarios inline dentro de argumentos o retornos complejos: `return x ? y ? a : b : c`
- ❌ Callbacks inline extensos pasados como argumento a `map`, `filter`, `reduce`, `forEach`, etc.
- ❌ Objetos o arrays inline con lógica embebida: `{ total: items.filter(i => i.ok).reduce((a, b) => a + b.price, 0) }`
- ❌ Asignaciones inline con operadores encadenados: `const v = (a || b) && (c ?? d) ? e : f`
- ❌ Composición de funciones inline: `compose(f, g, h)(x)` sin contexto claro


**Prefiere:**

- ✅ Asignar resultados intermedios a variables descriptivas:

  ```js
  // ❌ Inline complejo
  const names = users.filter(u => u.active && u.age >= 18).map(u => u.name).sort();

  // ✅ Pasos explícitos
  const activeUsers = users.filter((user) => user.active);
  const adultUsers = activeUsers.filter((user) => user.age >= 18);
  const adultNames = adultUsers.map((user) => user.name);
  const sortedNames = adultNames.sort();
  ```

- ✅ Extraer callbacks a funciones nombradas:

  ```js
  // ❌ Callback inline extenso
  items.forEach(item => {
    if (item.valid) { process(item); log(item); }
  });

  // ✅ Callback extraído
  function handleItem(item) {
    if (!item.valid) return;
    process(item);
    log(item);
  }
  items.forEach(handleItem);
  ```

- ✅ Extraer condiciones complejas a variables booleanas:

  ```js
  // ❌ Condición inline compleja
  if (user && user.role === 'admin' && (user.active || user.pending) && !user.banned) { ... }

  // ✅ Condición descompuesta
  const isAdmin = user?.role === 'admin';
  const isAllowedState = user?.active || user?.pending;
  const isNotBanned = !user?.banned;
  if (isAdmin && isAllowedState && isNotBanned) { ... }
  ```

- ✅ Separar la construcción de objetos/arrays con lógica embebida en pasos previos.

**Regla práctica:** si una línea necesita más de ~2 operaciones encadenadas o requiere desplazamiento horizontal para leerse, descomponla.

## Guardrails (lo que NO debo hacer)

- ❌ No dejar expresiones inline complejas (llamadas anidadas, cadenas largas de métodos, ternarios anidados, callbacks extensos, condiciones con múltiples operadores) sin descomponer en pasos legibles.

## Proceso

Cuando escribas:

1. **Lee el contexto**: entiende qué hace el código existente y qué se espera del cambio.
2. **Identifica la complejidad innecesaria**: anidamiento profundo, nombres pobres, one-liners, lógica redundante y **expresiones inline complejas**.
3. **Descompón el código inline complejo** en pasos explícitos con variables intermedias o funciones auxiliares antes de aplicar otras simplificaciones.
4. **Simplifica con pasos pequeños**: aplica los principios anteriores de forma incremental.
5. **Verifica que el comportamiento no cambió**: si hay tests, ejecútalos; si no, revisa mentalmente los caminos de ejecución.

## Formato de salida esperado

- Código limpio, explícito y fácil de leer, sin expresiones inline complejas.