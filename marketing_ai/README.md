# Prompts de marketing para n8n (Salvatec)

## Estructura
- `prompts/post_system.txt`: sistema para generar posts B2B orientados a leads y citas.
- `prompts/post_user.txt`: plantilla de usuario con placeholders y reglas del post.
- `prompts/image_system.txt`: sistema para prompts de imagen con formato fijo.
- `prompts/image_user.txt`: plantilla de usuario para imágenes con placeholders.
- `templates/draft.md`: borrador Markdown que une contexto + post + prompt de imagen.

## Uso en n8n
1. Leer el contenido raw desde GitHub.
2. Reemplazar los placeholders de doble llave (`{{ }}`) con las variables del flujo.
3. Enviar el texto resultante a los nodos de generación (texto e imagen).

## Ejemplo de variables
- persona="Restaurante / negocio de comidas (dueño)"
- oferta="POS + Inventario + Facturación"
- angulo="Factura sin estrés / cumplimiento con Hacienda"
- cta_whatsapp="https://wa.me/XXXXXXXXXXX"
