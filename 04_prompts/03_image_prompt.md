# Prompt estándar para generación de imágenes

## 1) Rol del generador de imagen
Eres un diseñador gráfico senior y marketer B2B. Debes crear imágenes profesionales de marketing para una marca de software B2B enfocada en pymes de LATAM, con criterios claros de realismo, confianza y tecnología accesible.

## 2) Contexto de marca
**Salvatec** es un software B2B para pymes en LATAM. La comunicación visual debe transmitir soluciones tecnológicas confiables, modernas y cercanas, evitando lo futurista extremo. La imagen debe sentirse usable, real y alineada con necesidades empresariales.

## 3) Reglas visuales obligatorias
- Estilo realista (fotográfico o hiperrealista, sin ilustraciones).
- Sensación de confianza (expresiones seguras, ambientes profesionales, orden visual).
- Tecnología accesible (dispositivos y escenarios cotidianos, no ciencia ficción).
- Paleta principal: rojo y blanco (accesorios, vestimenta, acentos, fondos neutros).
- Poco texto integrado en la imagen (máximo 3–5 palabras si es inevitable).

## 4) Variables que se reemplazan
- **{{persona}}**: perfil del cliente (p. ej., dueña de pyme, gerente comercial, equipo administrativo).
- **{{escenario}}**: contexto de uso (p. ej., oficina, local comercial, call center, planta ligera).
- **{{emocion}}**: emoción principal (p. ej., confianza, tranquilidad, control, optimismo).
- **{{beneficio}}**: beneficio clave del software (p. ej., ahorro de tiempo, mejor gestión, ventas ordenadas).

## 5) Prompt base (listo para copiar)
```
Fotografía ultra realista de {{persona}} trabajando en {{escenario}} real de negocio en LATAM. 
Estilo fotográfico profesional, iluminación natural suave, profundidad de campo realista, nivel DSLR / mirrorless. 
La escena transmite {{emocion}} y sensación de {{beneficio}} al usar tecnología práctica.

Composición limpia y sobria, con espacio visual vacío en el {{lado_reservado}} de la imagen para uso de branding posterior.
Colores neutros con acentos sutiles en rojo y blanco en vestimenta o entorno (sin saturación).

No incluir texto, logotipos, marcas, nombres de empresas ni pantallas legibles.
No estilo ilustrado, no caricatura, no 3D, no CGI, no render.
Apariencia 100% fotográfica, real, profesional y usable para marketing B2B.


```

## 6) Prompt negativo (qué evitar)
logo, brand name, text overlay, watermark,
invented logo, fake brand, misspelled text,

beauty lighting, cinematic portrait,
perfect skin, plastic skin,
model face, influencer style,
anime, illustration, render 3D,
AI art, unreal proportions,

oversharpen, oversmooth,
neon colors, fantasy lighting,
studio glamour photography



## 7) Checklist de calidad visual (5 puntos)
1. La escena luce realista y profesional.
2. Se percibe confianza y cercanía B2B.
3. La tecnología se siente accesible y útil.
4. Predominan rojo y blanco sin saturar la imagen.
5. Hay poco o ningún texto integrado.
