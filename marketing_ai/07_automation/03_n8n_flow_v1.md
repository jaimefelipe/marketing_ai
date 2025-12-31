# Flujo n8n v1 — Marketing AI Salvatec

Objetivo: describir el flujo n8n versión 1 del sistema de marketing AI de Salvatec, basado en el mapa de automatización aprobado.

## 1) Trigger inicial
- **Trigger**: Manual o Cron (configurable)
  - **Manual**: ejecución puntual para pruebas y QA.
  - **Cron**: ejecución programada (ej. lunes 09:00 hora local).

## 2) Nodos del flujo (en orden)

### 1. Start Trigger
- **Nombre del nodo**: Start Trigger
- **Tipo de nodo n8n**: Manual Trigger / Cron
- **Qué hace**: inicia el flujo por disparo manual o programado.
- **Inputs**: ninguno.
- **Outputs**: señal de inicio + timestamp de ejecución.

### 2. Cargar parámetros base
- **Nombre del nodo**: Base Params
- **Tipo de nodo n8n**: Set
- **Qué hace**: define variables base del ciclo (marca, objetivo, canal, calendario, placeholders faltantes).
- **Inputs**: señal de inicio.
- **Outputs**: objeto con parámetros del ciclo (ej. campaña, buyer persona, CTA, fecha objetivo).

### 3. Obtener brief aprobado
- **Nombre del nodo**: Fetch Approved Brief
- **Tipo de nodo n8n**: HTTP Request
- **Qué hace**: consulta el repositorio/drive con el brief aprobado del ciclo.
- **Inputs**: Base Params (ID de campaña/fecha).
- **Outputs**: brief estructurado (texto/tabla).

### 4. Validar completitud de brief
- **Nombre del nodo**: Validate Brief
- **Tipo de nodo n8n**: IF
- **Qué hace**: verifica si el brief trae datos mínimos (público, oferta, CTA, restricciones).
- **Inputs**: brief.
- **Outputs**:
  - **True**: brief completo.
  - **False**: brief incompleto.

### 5. Solicitar ajustes de brief
- **Nombre del nodo**: Brief Fix Request
- **Tipo de nodo n8n**: HTTP Request / Email
- **Qué hace**: notifica al responsable para completar datos faltantes.
- **Inputs**: resultado False de Validate Brief + lista de faltantes.
- **Outputs**: ticket/solicitud enviada.

### 6. Generar outline de contenido
- **Nombre del nodo**: Content Outline
- **Tipo de nodo n8n**: GPT
- **Qué hace**: genera la estructura base (Hook/Beneficio/Prueba/CTA) y recomendaciones por canal.
- **Inputs**: brief completo + Base Params.
- **Outputs**: outline por pieza (post, reel, historia).

### 7. Generar copy principal
- **Nombre del nodo**: Draft Copy
- **Tipo de nodo n8n**: GPT
- **Qué hace**: redacta copies y variantes usando el outline aprobado.
- **Inputs**: outline + brief.
- **Outputs**: borradores de copy por canal.

### 8. Validación de reglas de contenido
- **Nombre del nodo**: Content Rules Check
- **Tipo de nodo n8n**: IF
- **Qué hace**: verifica reglas (CTA presente, tono profesional, sin promesas falsas, placeholders si faltan datos).
- **Inputs**: borradores de copy.
- **Outputs**:
  - **True**: cumple reglas.
  - **False**: incumplimientos detectados.

### 9. Ajuste de copy por incumplimientos
- **Nombre del nodo**: Copy Fix
- **Tipo de nodo n8n**: GPT
- **Qué hace**: corrige el copy para cumplir reglas de contenido.
- **Inputs**: borradores + lista de incumplimientos.
- **Outputs**: copy corregido.

### 10. Generar lineamientos de diseño
- **Nombre del nodo**: Design Directions
- **Tipo de nodo n8n**: GPT
- **Qué hace**: define guía visual de la pieza (colores rojo/blanco, poco texto en imagen, elemento salvavidas opcional).
- **Inputs**: brief + copy final.
- **Outputs**: lineamientos de diseño.

### 11. Preparar paquete de entrega
- **Nombre del nodo**: Package Assets
- **Tipo de nodo n8n**: Set
- **Qué hace**: arma el paquete con copy final, variantes y guía visual.
- **Inputs**: copy final + lineamientos de diseño.
- **Outputs**: payload listo para revisión humana.

### 12. Revisión humana
- **Nombre del nodo**: Human Review
- **Tipo de nodo n8n**: Manual/Approval
- **Qué hace**: revisión editorial y de marca antes de publicar.
- **Inputs**: paquete de entrega.
- **Outputs**:
  - **Approved**: contenido aprobado.
  - **Rejected**: comentarios y ajustes solicitados.

### 13. Aplicar ajustes post-revisión
- **Nombre del nodo**: Post-Review Fix
- **Tipo de nodo n8n**: GPT
- **Qué hace**: aplica cambios solicitados en la revisión.
- **Inputs**: comentarios + paquete de entrega.
- **Outputs**: versión final ajustada.

### 14. Guardar entregables
- **Nombre del nodo**: Save Deliverables
- **Tipo de nodo n8n**: HTTP Request / File
- **Qué hace**: guarda copies y lineamientos en el repositorio/drive.
- **Inputs**: versión final ajustada.
- **Outputs**: enlaces/IDs de archivos guardados.

### 15. Publicación (manual)
- **Nombre del nodo**: Publish Hand-off
- **Tipo de nodo n8n**: Manual/Notification
- **Qué hace**: entrega el material aprobado para publicación manual en canales.
- **Inputs**: enlaces/IDs de archivos guardados.
- **Outputs**: notificación enviada.

## 3) Puntos donde se requiere revisión humana
- Validación del brief cuando falta información crítica.
- Revisión editorial y de marca del paquete de entrega.
- Aprobación final antes de publicación (siempre manual en v1).

## 4) Qué se guarda en archivos vs qué se publica
- **Se guarda en archivos**:
  - Brief aprobado.
  - Outline por pieza.
  - Copy final y variantes.
  - Lineamientos de diseño.
- **Se publica**:
  - Solo el material aprobado tras revisión humana.
  - La publicación es manual en v1 (handoff, no post automático).

## 5) Qué se deja fuera de la versión 1 (scope control)
- Generación automática de creatividades (imágenes/video).
- Publicación automática en redes sociales.
- A/B testing automatizado.
- Integración con CRM para seguimiento post-publicación.
- Dashboards de performance y reporting automático.
