# TP7 — Interactividad y Captura de Datos: Formularios en el Álbum Web
**Laboratorio de Programación · 6° G · 2026**

---

## Descripción del proyecto

Este trabajo práctico extiende el álbum web de coleccionables desarrollado en el TP6, incorporando una página de registro completa con formularios HTML5. El objetivo fue aprender a estructurar, vincular y validar campos de captura de datos desde el lado del cliente (Front-end), dejando la estructura lista para su futura conexión con un servidor (Back-end).

La nueva página `registro.html` mantiene la identidad visual del proyecto anterior, reutilizando la hoja de estilos `estilos.css` y el mismo header, nav y footer.

---

## Archivos entregados

| Archivo | Descripción |
|---|---|
| `index.html` | Página principal del álbum (TP6, actualizada con link a Registro en el nav) |
| `registro.html` | Página de registro con el formulario completo (TP7) |
| `estilos.css` | Hoja de estilos externa compartida — contiene los estilos del TP6 y los nuevos del TP7 |
| `README_TP7.md` | Este informe |

---

## Requerimientos técnicos cumplidos

### Estructura del formulario `<form>`

Todo el bloque de interacción está envuelto en una única etiqueta `<form>` con los siguientes atributos:

```html
<form id="form-registro" method="GET" action="#" autocomplete="off">
```

- `method="GET"` — los datos ingresados se añaden como parámetros en la URL al presionar enviar, tal como indica el enunciado para esta etapa sin Back-end.
- `autocomplete="off"` — desactiva el autocompletado del navegador en los campos pertinentes.

---

### Datos Personales e Identificación

Todos los campos de esta sección usan el atributo `required` para bloquear el envío si están vacíos.

**Nombre y Apellido** — dos cajas de texto individuales con `type="text"`, organizadas en una fila de dos columnas:

```html
<input type="text" id="nombre"   name="nombre"   required>
<input type="text" id="apellido" name="apellido" required>
```

**Correo Electrónico** — campo `type="email"` que verifica de forma nativa la estructura de una dirección válida antes de permitir el envío:

```html
<input type="email" id="email" name="email" required>
```

**Contraseña** — campo `type="password"` que oculta los caracteres mientras el usuario escribe:

```html
<input type="password" id="contrasena" name="contrasena" required>
```

---

### Restricciones de Edad y Selección Única

**Edad** — control numérico con `min="6"` y `max="99"`. El navegador rechaza valores fuera de ese rango sin necesidad de JavaScript:

```html
<input type="number" id="edad" name="edad" min="6" max="99" required>
```

**Categoría de Álbum** — tres botones de opción `type="radio"` que comparten exactamente el mismo atributo `name="categoria"`, lo que hace que sean excluyentes entre sí: marcar uno desmarca los demás automáticamente:

```html
<input type="radio" id="cat-inicial"   name="categoria" value="inicial">
<input type="radio" id="cat-avanzado"  name="categoria" value="avanzado" checked>
<input type="radio" id="cat-legendario" name="categoria" value="legendario">
```

---

### Selección Múltiple y Menús Desplegables

**Temáticas de Interés** — seis casillas `type="checkbox"` independientes entre sí, organizadas en una grilla de dos columnas. El usuario puede marcar una o varias a la vez:

```html
<input type="checkbox" id="int-futbol"  name="intereses" value="futbol" checked>
<input type="checkbox" id="int-comics"  name="intereses" value="comics">
<!-- ... -->
```

**Sección del Álbum** — menú desplegable con `<select>` y seis `<option>`, permitiendo elegir sobre qué grupo de figuritas el coleccionista necesita más ayuda o intercambios:

```html
<select id="seccion-album" name="seccion_album">
  <option value="grupo-a">Grupo A — Porteros y Defensores</option>
  <!-- ... -->
</select>
```

---

### Campos Especiales

**ID de Sesión (solo lectura)** — campo de texto con `readonly` que muestra el valor `100`. El usuario puede verlo pero no modificarlo. En CSS se le aplica un fondo y color diferenciado para indicar visualmente que no es editable:

```html
<input type="text" id="id-sesion" name="id_sesion" value="100" readonly>
```

**Identificador del Sistema (oculto)** — campo `type="hidden"` que no aparece en pantalla pero viaja al servidor junto con el resto de los datos del formulario, simulando metadatos internos:

```html
<input type="hidden" id="sistema" name="sistema" value="SistemaAlbumWeb-v2">
```

---

### Área de Texto `<textarea>`

Campo de texto largo para que el coleccionista redacte su perfil o liste las figuritas que busca. La etiqueta de cierre `</textarea>` está en la misma línea que la de apertura para evitar que se generen espacios o tabulaciones por defecto dentro del cuadro:

```html
<textarea class="form-textarea" id="perfil-texto" name="perfil" rows="5"></textarea>
```

---

### Accesibilidad con Etiquetas `<label>`

Todos los controles visibles tienen su etiqueta `<label>` con el atributo `for` que coincide exactamente con el `id` del campo asociado. Esto permite que al hacer clic en el texto de la etiqueta, el navegador enfoque automáticamente el campo correspondiente:

```html
<label for="nombre">Nombre</label>
<input type="text" id="nombre" ...>
```

Los campos radio y checkbox usan la etiqueta `<label>` como contenedor envolvente, lo que amplía el área clickeable a toda la fila:

```html
<label class="opcion-item" for="cat-inicial">
  <input type="radio" id="cat-inicial" name="categoria" value="inicial">
  📦 Álbum Inicial — Para nuevos coleccionistas
</label>
```

---

### Botones de Envío y Reinicio

El formulario cierra con dos botones implementados con la etiqueta `<input>`:

```html
<input class="btn-submit" type="submit" value="ENVIAR REGISTRO">
<input class="btn-reset"  type="reset"  value="RESTABLECER CAMPOS">
```

- **Submit** — valida el formulario y, si todo es correcto, muestra un mensaje de confirmación en pantalla.
- **Reset** — limpia instantáneamente todos los campos devolviéndolos a su estado original sin recargar la página.

---

### Estilos CSS requeridos

Los nuevos estilos del TP7 se agregaron al final de `estilos.css`, respetando las variables y la paleta del TP6.

| Propiedad | Aplicación |
|---|---|
| `text-transform: uppercase` | Botones `.btn-submit` y `.btn-reset` — texto siempre en mayúsculas |
| `cursor: pointer` | Todos los botones — muestra el ícono de mano al pasar el cursor |
| `padding: 11px 14px` | Todos los campos de texto — espaciado interior prolijo |
| `margin-top: 18px` | `.form-grupo` — separación entre controles para evitar que queden amontonados |

Además, el botón de envío hereda el comportamiento del TP6: en `:hover` cambia el color de fondo y aumenta el tamaño de fuente simultáneamente.

---

## Validación implementada

La validación opera en dos niveles complementarios:

**Nivel 1 — Validación nativa HTML5** (sin JavaScript):
- `required` bloquea el envío si el campo está vacío.
- `type="email"` verifica que el formato incluya `@` y dominio.
- `min="6"` y `max="99"` en el campo numérico rechazan valores fuera del rango.

**Nivel 2 — Validación con JavaScript** (complementaria):
- Verifica que nombre y apellido no estén en blanco.
- Comprueba que la contraseña tenga al menos 8 caracteres.
- Si todo es válido, muestra un mensaje de confirmación personalizado con el nombre del usuario.
- El botón Reset oculta el mensaje de confirmación si el usuario limpia el formulario.

---

## Organización de archivos

```
proyecto-album/
│
├── index.html          ← Álbum principal (TP6 + link a Registro)
├── registro.html       ← Formulario de registro (TP7)
├── estilos.css         ← Estilos compartidos TP6 + TP7
└── README_TP7.md       ← Este informe
```

---

## Cómo ejecutar

1. Colocar todos los archivos en la misma carpeta.
2. Abrir `index.html` en cualquier navegador moderno.
3. Hacer clic en **📝 Registro** en la barra de navegación para acceder al formulario.
4. No requiere servidor ni instalación de dependencias.

---

*Laboratorio de Programación · 6° G · 2026*
