# 📐 Sistema de Modelos 3D - Verificación SOS

Sistema para visualizar modelos 3D de proyectos en la web usando Model-Viewer de Google.

## 🗂️ Estructura de Archivos

```
sergeolitegui-ai.github.io/
├── galeria-3d.html          # Galería de modelos del usuario
├── visor-3d.html            # Visor 3D interactivo
└── models3d/
    ├── models.json          # Configuración de modelos
    ├── yanamarca/
    │   ├── modelo.glb       # Modelo 3D en formato GLB
    │   └── thumbnail.jpg    # Imagen preview (16:9, recomendado 800x450px)
    ├── hacienda-colpa/
    │   ├── modelo.glb
    │   └── thumbnail.jpg
    └── ...
```

## ➕ Cómo Agregar un Nuevo Modelo

### Paso 1: Preparar el Modelo GLB

**Opción A: Convertir desde OBJ (OpenDroneMap)**
```bash
# Instalar herramienta
npm install -g obj2gltf

# Convertir
obj2gltf -i modelo.obj -o modelo.glb
```

**Opción B: Usar Blender (Recomendado para optimización)**
```
1. Abrir Blender
2. File → Import → Wavefront (.obj)
3. Seleccionar malla → Modifiers → Decimate (reducir polígonos)
4. File → Export → glTF 2.0 (.glb)
5. Opciones: ✓ Apply Modifiers, ✓ Compression
```

### Paso 2: Optimizar (Importante para Web)

**Tamaño recomendado:** < 50MB
- Reducir polígonos: 500K - 2M triángulos máx
- Comprimir texturas: 2K (2048x2048) máx
- Formato: GLB (binario comprimido)

**Herramientas:**
- Blender: Decimate modifier
- gltf-pipeline: `npm install -g gltf-pipeline`
- Online: https://products.aspose.app/3d/compress

### Paso 3: Crear Thumbnail

```
- Tamaño: 800x450px (16:9)
- Formato: JPG (optimizado)
- Captura del modelo desde mejor ángulo
```

**Crear thumbnail en Blender:**
1. Posicionar cámara en buen ángulo
2. Render → Render Image
3. Image → Save As → JPG

### Paso 4: Subir a GitHub

```bash
# Crear carpeta para el proyecto
mkdir models3d/nombre-proyecto

# Copiar archivos
cp modelo.glb models3d/nombre-proyecto/
cp thumbnail.jpg models3d/nombre-proyecto/

# Commit
git add models3d/nombre-proyecto
git commit -m "Agregar modelo 3D: nombre-proyecto"
git push
```

### Paso 5: Actualizar models.json

Editar `models3d/models.json` y agregar:

```json
{
  "id": "nombre-proyecto-2024",
  "title": "Título del Proyecto",
  "description": "Descripción detallada del levantamiento 3D",
  "modelPath": "models3d/nombre-proyecto/modelo.glb",
  "thumbnailPath": "models3d/nombre-proyecto/thumbnail.jpg",
  "location": "Ubicación, Cajamarca",
  "area": "X,XXX m²",
  "date": "2024-03-15",
  "userEmails": [
    "cliente@ejemplo.com"
  ]
}
```

### Paso 6: Push Final

```bash
git add models3d/models.json
git commit -m "Asignar modelo a cliente@ejemplo.com"
git push
```

## 👥 Asignar Modelos a Usuarios

Para que un usuario vea un modelo, agrega su email al array `userEmails`:

```json
"userEmails": [
  "cliente1@ejemplo.com",
  "cliente2@ejemplo.com"
]
```

**Múltiples clientes = Mismo modelo**
Un modelo puede ser visible para varios usuarios.

## 🎨 Características del Visor 3D

✅ Rotación automática (on/off)
✅ Zoom y pan con mouse/touch
✅ AR (Realidad Aumentada) en móvil
✅ Pantalla completa
✅ Captura de pantalla
✅ Reset de cámara
✅ Sombras y materiales PBR
✅ Responsive (desktop y móvil)

## 📱 Cómo los Clientes Acceden

1. Iniciar sesión en verificacionsos.pe
2. Click en avatar → "Tus Modelos 3D"
3. Ver galería de proyectos asignados
4. Click en proyecto → Visor 3D interactivo

## ⚙️ Requisitos de Archivos

| Tipo | Formato | Tamaño Máx | Notas |
|------|---------|-----------|-------|
| Modelo 3D | GLB | 50MB | Comprimido, optimizado |
| Thumbnail | JPG | 500KB | 800x450px, 16:9 |

## 🚫 Límites de GitHub

- **Archivo individual:** 100MB máx
- **Repositorio total:** 1GB recomendado
- **Archivos grandes:** Considera usar Git LFS si >50MB

## 💡 Tips de Optimización

1. **Reducir polígonos:**
   - Usa Decimate en Blender
   - Target: 500K-2M triángulos

2. **Comprimir texturas:**
   - Resize a 2K (2048x2048)
   - Compresión JPG 85%

3. **Limpiar geometría:**
   - Eliminar duplicados
   - Merge vértices
   - Remove doubles

4. **Test de carga:**
   - Modelo debe cargar en <10 segundos
   - Test en móvil también

## 🆘 Troubleshooting

**Modelo no carga:**
- Verificar que modelo.glb existe en la ruta
- Revisar consola del navegador (F12)
- Confirmar que email del usuario está en `userEmails`

**Modelo muy lento:**
- Reducir polígonos con Blender Decimate
- Comprimir texturas a 1K o 2K
- Usar herramienta gltf-pipeline

**Usuario no ve su modelo:**
- Verificar email en `models.json`
- Confirmar que el usuario está logueado
- Revisar que el ID del modelo es correcto

## 📞 Soporte

Para preguntas: contacto@verificacionsos.pe
