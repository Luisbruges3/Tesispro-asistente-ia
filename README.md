# ClasesPro — Asistente Automático de Ventas por WhatsApp

Proyecto final de Inteligencia Artificial. Asistente automático que recibe 
mensajes de prospectos por WhatsApp, los clasifica con IA y responde 
de forma automática según la intención detectada.

---

## ¿Qué hace el asistente?

- Recibe mensajes de clientes por WhatsApp
- Clasifica la intención: precio, disponibilidad, listo_compra, queja, saludo, fuera_tema
- Califica el nivel de interés: frío, tibio, caliente
- Responde automáticamente según la intención
- Alerta al vendedor por Gmail cuando hay un prospecto caliente o una queja
- Registra cada conversación en Google Sheets (CRM)

---

## Tecnologías usadas

| Herramienta | Uso |
|---|---|
| Make (Integromat) | Automatización del flujo completo |
| WhatsApp Cloud API | Canal de mensajería |
| Groq (LLaMA 3.3 70B) | Clasificación de intenciones |
| Gmail | Alertas al vendedor |
| Google Sheets | CRM y catálogo de servicios |


---

## Estructura del repositorio
 README.md
 02_prompt_y_guion.md -  Prompt del clasificador y guion de bienvenida        
 notebook_clasificador.ipynb 
 index.html                   
 Landing page (GitHub Pages)

---

## Métricas del clasificador

| Métrica | Resultado |
|---|---|
| Accuracy intención | 100% |
| Accuracy nivel de interés | 100% |
| Mensajes de prueba | 20 |
| Modelo | Grok |

---

## Flujo del escenario en Make

WhatsApp → Webhook → Groq (clasifica) → Parse JSON → Router
├── precio/disponibilidad → respuesta automática
├── listo_compra → respuesta + Gmail vendedor
├── queja → mensaje empático + Gmail vendedor
└── saludo/fuera_tema → redirección cordial
