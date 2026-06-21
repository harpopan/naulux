---
version: 1.0
estado: activo
idioma: inglés (traducido)
---

# Explicación de CORS (Cross-Origin Resource Sharing)

> [!summary] Resumen
> Explicación didáctica de CORS usando una analogía de un edificio de apartamentos con guardia de seguridad. Cubre la Política de Mismo Origen, la petición preflight (OPTIONS), la cabecera Access-Control-Allow-Origin y cómo configurar correctamente el backend, incluyendo la respuesta ideal para una entrevista técnica.

ENTREVISTADOR:
«Tu frontend se ejecuta en localhost:3000 y tu backend en localhost:8000. Cuando intentas obtener datos, recibes un error de CORS. ¿Por qué ocurre esto y cómo lo solucionas?»

## Explicación para principiantes

Imagina que vives en un Edificio de Apartamentos Estricto (El Navegador).

- Tú (El Frontend en :3000) quieres pedir azúcar a un vecino en un Edificio Diferente (El Backend en :8000).
- El guardia de seguridad (El Navegador) te detiene y dice: «¡Espera! No sé si ese vecino confía en ti. No te dejaré llevarte nada a menos que me diga explícitamente que estás autorizado.»

Este «Guardia de Seguridad» es la Política de Mismo Origen (Same-Origin Policy). Evita que sitios web maliciosos roben datos de otros sitios.

## Desglose técnico

**CORS (Cross-Origin Resource Sharing):**
Es una característica de seguridad implementada por los navegadores. Un «Origen» se define por Protocolo + Dominio + Puerto. Como tus puertos son diferentes (:3000 vs :8000), el navegador los considera «Origen Cruzado».

**El flujo:**
1. **Petición Preflight (OPTIONS):** Antes de la petición real, el navegador envía una llamada «OPTIONS» al backend para preguntar: «Oye, ¿está bien que :3000 hable contigo?»
2. **La Respuesta:** Si el backend no devuelve la cabecera correcta (`Access-Control-Allow-Origin`), el navegador bloquea la petición y lanza el error de CORS.

**Cómo solucionarlo:**
Debes configurar tu backend (Node.js, Spring Boot, Python, etc.) para permitir peticiones desde tu puerto de frontend.

Ejemplo (Express.js):
```js
app.use(cors({ origin: 'http://localhost:3000' }));
```

## Respuesta ideal para entrevista

«CORS no es un "bug"; es un mecanismo de seguridad del lado del navegador basado en la Política de Mismo Origen. Para resolverlo, debemos configurar el backend para que incluya la cabecera `Access-Control-Allow-Origin` en su respuesta. En producción, nunca debemos usar `origin: '*'` ya que abre vulnerabilidades de seguridad; siempre debemos incluir en lista blanca solo los dominios específicos que necesitan acceso a nuestra API.»
