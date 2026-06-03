# Prompt y Guion del Asistente — ClasesPro


## Descripción
Documentación del prompt diseñado para clasificar mensajes de prospectos 
por WhatsApp usando un LLM (Groq - LLaMA 3.3 70B) y Google Gemini 2.5 Flash.

---

## Prompt del Clasificador
Eres el asistente de ventas por WhatsApp de ClasesPro, servicio de clases
universitarias en Colombia. Lee el mensaje y clasificalo. Respondes SIEMPRE
en JSON valido sin texto adicional.
intencion: una de precio, disponibilidad, listo_compra, queja, saludo, fuera_tema.
nivel_interes: una de frio, tibio, caliente.
Reglas estrictas:

Si intencion es listo_compra entonces nivel_interes es caliente.
Si intencion es queja entonces nivel_interes es frio.
Si intencion es fuera_tema o saludo entonces nivel_interes es frio.
Si intencion es precio o disponibilidad y el cliente muestra urgencia o
dice que ya decidio entonces nivel_interes es caliente, si no es tibio.

Devuelve solo: {"intencion":"<valor>","nivel_interes":"<valor>"}

---

## Métricas de Evaluación

| Métrica | Resultado |
|---|---|
| Accuracy intención | 100% |
| Accuracy nivel de interés | 100% |
| Mensajes de prueba | 20 |
| Modelo evaluado | Gemini 2.5 Flash |

---

## Ejemplos Comentados

### Ejemplo 1 ✅
- **Mensaje:** "Quiero contratar las clases de cálculo, cómo pago?"
- **Esperado:** listo_compra | caliente
- **Predicho:** listo_compra | caliente
- **Análisis:** Mensaje claro de compra inmediata. El cliente ya decidió y 
  pregunta por el método de pago.

### Ejemplo 2 ✅
- **Mensaje:** "Cuánto cuesta una hora de clase de estadística?"
- **Esperado:** precio | tibio
- **Predicho:** precio | tibio
- **Análisis:** Consulta directa de precio. El cliente tiene interés pero 
  aún no decide.

### Ejemplo 3 ✅
- **Mensaje:** "Cuál es la receta de la bandeja paisa?"
- **Esperado:** fuera_tema | frio
- **Predicho:** fuera_tema | frio
- **Análisis:** Mensaje completamente ajeno al servicio. El modelo lo 
  identifica correctamente sin confundirse.

---

## Guion de Bienvenida del Asistente

Cuando un cliente escribe por primera vez, el asistente responde:

> 👋 ¡Hola! Bienvenido a *ClasesPro*, tu servicio de clases universitarias 
> en Colombia. 
>
> Puedo ayudarte con:
> 📚 Información sobre nuestras clases y precios
> 📅 Disponibilidad y horarios
> ❓ Cualquier duda sobre nuestros servicios
>
> ¿En qué te puedo ayudar hoy?

---

## Intenciones Detectadas

| Intención | Descripción | Nivel de interés |
|---|---|---|
| precio | Pregunta por costos o planes | tibio / caliente |
| disponibilidad | Pregunta por horarios o fechas | tibio / caliente |
| listo_compra | Quiere contratar el servicio | caliente |
| queja | Expresa insatisfacción | frio |
| saludo | Saludo sin intención clara | frio |
| fuera_tema | Mensaje no relacionado al servicio | frio |
