# STG – Sistema de Gestión de Equipos
**Smart Transportation Gateway**

---

## 📁 Estructura del Proyecto

```
STG-project/
├── index.html       ← Aplicación web (Frontend)
├── Code.gs          ← Backend Google Apps Script
├── assets/
│   └── logo.png     ← Logo STG (copiar aquí)
└── README.md        ← Este archivo
```

---

## 🔧 PASO 1 – Configurar Google Sheets

Abra el Google Sheet:
**https://docs.google.com/spreadsheets/d/1sgqvERall1o8aSLPEqO7KrhGELrjDQXM8XxWbV2H23o/edit**

### Hoja: `USUARIOS`
| A | B | C | D | E |
|---|---|---|---|---|
| ID_USUARIO | APELLIDOS | NOMBRES | CARGO | USUARIO_SISTEMA |
| U001 | García | Juan | Técnico | jgarcia |
| ... | ... | ... | ... | ... |

### Hoja: `EQUIPOS`
| A | B |
|---|---|
| ID_EQUIPO | NOMBRE_EQUIPO |
| EQ001 | Laptop Dell Latitude |
| ... | ... |

### Hoja: `REGISTROS`
| A | B | C | D | E | F | G | H | I | J | K | L | M |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| ID_USUARIO | APELLIDOS | NOMBRES | ID_EQUIPO | NOMBRE_EQUIPO_ASIGNADO | FECHA_ASIGNACIÓN | HORA_ASIGNACIÓN | FECHA_DEVOLUCIÓN | HORA_DEVOLUCIÓN | ESTADO | CANTIDAD_TARJETAS_ASIGNADAS | CANTIDAD_TARJETAS_DEVUELTAS | OBSERVACIÓN |

> ⚠️ **Importante:** La fila 1 de cada hoja debe ser el encabezado. Los datos comienzan en la fila 2.

---

## ⚙️ PASO 2 – Desplegar el Backend (Google Apps Script)

1. En el Google Sheet → **Extensiones** → **Apps Script**
2. En el editor, crear un archivo llamado `Code.gs`
3. **Pegar el contenido completo de `Code.gs`** de este proyecto
4. Guardar (`Ctrl+S`)
5. Hacer clic en **Implementar** → **Nueva implementación**
6. Configurar:
   - Tipo: **Aplicación web**
   - Ejecutar como: **Yo (Mi cuenta)**
   - Quién tiene acceso: **Cualquier persona**
7. Hacer clic en **Implementar**
8. **Copiar la URL** que aparece (empieza con `https://script.google.com/...`)

---

## 🌐 PASO 3 – Configurar el Frontend

1. Abrir `index.html` con un editor de texto
2. Buscar la línea:
   ```javascript
   const API_URL = 'TU_APPS_SCRIPT_URL_AQUI';
   ```
3. Reemplazar `TU_APPS_SCRIPT_URL_AQUI` con la URL obtenida en el Paso 2

---

## 🚀 PASO 4 – Publicar en GitHub Pages

1. Crear un repositorio nuevo en **https://github.com**
2. Subir los archivos:
   ```
   index.html
   assets/logo.png
   ```
3. Ir a **Settings** → **Pages**
4. En "Source" seleccionar: **Branch: main** → **/(root)**
5. Hacer clic en **Save**
6. La aplicación estará disponible en:
   `https://TU_USUARIO.github.io/NOMBRE_REPOSITORIO`

---

## 📋 Lógica de Negocio

```
Usuario selecciona ID → Sistema carga info → Presiona "Aceptar"
         │
         ▼
  ¿Último registro con ACTIVO?
         │
    NO ──┴── SÍ
    │         │
    ▼         ▼
SECCIÓN 2  SECCIÓN 3
Asignación Devolución
    │         │
    ▼         ▼
Graba ACTIVO Actualiza → DEVUELTO
en REGISTROS  en REGISTROS
```

### Estados del Registro:
- **ACTIVO** → El usuario tiene un equipo asignado
- **DEVUELTO** → El equipo fue devuelto (cierre de registro)

---

## ⚠️ Restricciones del Sistema

- Un usuario con estado **ACTIVO** solo puede acceder a la **Sección 3**
- Un usuario sin registro o con estado **DEVUELTO** accede a la **Sección 2**
- El campo Observaciones permite máximo **200 palabras**
- El campo Tarjetas acepta solo valores numéricos

---

## 🛠️ Solución de Problemas

| Problema | Solución |
|---|---|
| "No se pudo conectar" | Verificar que la URL de Apps Script es correcta |
| Lista de usuarios vacía | Verificar que la hoja USUARIOS tiene datos desde la fila 2 |
| Error al guardar | Verificar permisos del Apps Script (Anyone) |
| Logo no aparece | Asegurarse de que `assets/logo.png` está en el repositorio |

---

## 📞 Soporte

**Smart Transportation Gateway**
Sistema de Gestión de Equipos v1.0
