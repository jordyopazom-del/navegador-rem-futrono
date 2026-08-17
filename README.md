# Navegador REM 2026 — CESFAM Futrono

Buscador inteligente del Resumen Estadístico Mensual (REM) para apoyo clínico en el box de atención.

## ¿Para qué sirve?
El clínico escribe la prestación que realizó (ej: EMPAM, HTA, curación avanzada) y el sistema le indica exactamente:
- En qué **pestaña REM** debe registrar la atención
- En qué **sección y serie** específica
- Los **cruces obligatorios** (validaciones cruzadas) con otras pestañas

## Estructura del proyecto
```
navegador-rem/
  index.html          ← Aplicación principal (abre en el navegador)
  vercel.json         ← Configuración de despliegue en Vercel
  data/
    rem_rules.json    ← BASE DE DATOS DE REGLAS (editar aquí para actualizar)
```

## Cómo usar localmente
Opción 1 — Servidor Python rápido (recomendado):
```bash
cd "navegador-rem"
python3 -m http.server 8080
```
Luego abre: http://localhost:8080

**¿Por qué no abrir el index.html directo?**
El navegador bloquea la carga de archivos JSON locales por seguridad (CORS). Se necesita un servidor web mínimo.

## Cómo actualizar las reglas (anualmente)
1. Abre  con cualquier editor de texto
2. Modifica los campos de las reglas existentes o agrega nuevas siguiendo el mismo esquema
3. Actualiza  y  al inicio del archivo
4. Guarda y despliega (si estás en Vercel, haz push al repositorio)

## Esquema de una regla
```json
{
  "id": "rem-XXX",
  "prestacion": "Nombre completo de la prestación",
  "terminos_busqueda": ["palabras clave", "sinónimos", "siglas"],
  "registro_principal": {
    "pestaña": "REM XXX",
    "seccion": "Sección X: ...",
    "serie": "Serie X: ...",
    "columnas": "Col. X...",
    "descripcion": "Instrucción clara para el clínico"
  },
  "validaciones_cruzadas": [
    {
      "id": "cruce-XXX-a",
      "pestaña_destino": "REM YYY",
      "seccion_destino": "Sección Y: ...",
      "mensaje": "Descripción del cruce obligatorio",
      "criticidad": "alta | media | baja"
    }
  ]
}
```

## Niveles de criticidad
- 🔴 **alta** — OBLIGATORIO: El registro es mandatorio y su ausencia genera error estadístico
- 🟡 **media** — IMPORTANTE: Se recomienda fuertemente para mantener consistencia
- 🔵 **baja** — RECOMENDADO: Complementa el registro pero no es invalidante

## Despliegue en Vercel
1. Sube esta carpeta a un repositorio de GitHub
2. Importa el proyecto en vercel.com
3. Vercel detectará automáticamente la configuración del 

## Soporte
CESFAM Futrono — Unidad de Estadística (SOME)
Basado en el Manual Instruccional REM 2026, MINSAL Chile
