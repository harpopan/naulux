---
version: 1.0
estado: activo
idioma: castellano
---

# Idempotencia

> [!summary] Resumen
> Explicación breve del concepto de idempotencia en desarrollo: la propiedad de una operación que puede repetirse múltiples veces sin alterar el resultado más allá de la primera ejecución. Concepto clave en APIs para evitar duplicados.

Conceptos DEV que escuchas… pero nadie te explica

Hoy: IDEMPOTENCIA

Idempotencia es cuando puedes repetir una operación varias veces y el resultado final no cambia.

- La ejecutas una vez… funciona
- La repites… y no pasa nada extra

Ejemplo típico: Marcar un pedido como enviado
- La primera vez lo cambia
- Las siguientes… simplemente ya estaba hecho

- No duplica
- No vuelve a procesar
- No genera efectos extra
- Todo sigue igual

Esto es clave en APIs para evitar duplicados, especialmente en pagos.
