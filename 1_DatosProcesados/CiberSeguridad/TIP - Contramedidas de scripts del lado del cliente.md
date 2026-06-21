---
version: 1.0
estado: activo
idioma: inglés (traducido)
---

# Contramedidas de scripts del lado del cliente

> [!summary] Resumen
> Técnica de defensa contra scrapers que consiste en incrustar WebAssembly pesado o JavaScript ofuscado con multi-hilo en el código fuente. Los scrapers que compilan y ejecutan código web a ciegas acaban lanzando tareas de cálculo intensivas localmente, sobrecargando su propio hardware.

Mecanismo: Se incrustan instrucciones pesadas de WebAssembly o JavaScript ofuscado con multi-hilo directamente en los módulos del código fuente objetivo.

Por qué funciona: Los scrapers automatizados que compilan y ejecutan código web a ciegas acaban lanzando tareas de cálculo intensivas en recursos localmente, sobrecargando su propia infraestructura de hardware.

Cómo mantenerse seguro: Asegúrate de que todos los entornos de análisis automatizado tengan restricciones de sandbox que deshabiliten explícitamente los ciclos de ejecución del navegador en línea sin procesar.

---

«Un bot scraper intenta robar código de tu sitio web... pero tú sigues a cyberzest y obligas a su propia CPU a minar cripto para ti»
