# DynamicForm.js
La idea del **DynamicForm.js** es evitar escribir manualmente formularios con múltiples campos.
### Ejemplo de uso

```jsx
<DynamicForm 
	fields={fields}
	values={formData}
	onChange={handleChange}
	formDirection="grid-3"
/>
```

A continuación se detallan los parámetros que se utilizan.

---
## fields

Es uno de los parámetros obligatorios del componente.  
Es un arreglo de objetos que generalmente siguen la misma estructura, exceptuando los de tipo **select**.

```js
const fields = [
	{ 
		label: "Nombre del Inventario",
		name: "Nombre del Inventario",
		type: "text",
		placeholder: "Nombre del Inventario..." 
	},
	{ 
		label: "Descripcion del Inventario",
		name: "Descripcion del Inventario",
		type: "text",
		placeholder: "Descripcion del inventario..."
	},
	{ 
		label: "Fecha de revision",
		name: "Fecha de revision",
		type: "date"
	},
	{ 
		label: "Tipo del Atributo",
		name: "tipo-atributo",
		type: "select",
		options: [
			{ label: "opcion1", value: "opcion1" },
			{ label: "opcion2", value: "opcion2" },
			{ label: "opcion3", value: "opcion3" },
			{ label: "opcion4", value: "opcion4" }
		]
	}
];
```

Los objetos siguen la convención **atributo:valor**, siendo los atributos los mismos que los tipos de input de HTML.  
Por ejemplo, **type:"text"** hace referencia al input de tipo texto de HTML.  
Se pueden usar todos los tipos comunes de HTML: _mail, date, text, password, number_, etc.

---
## values

Este parámetro almacena los datos escritos en los campos del formulario.  
A medida que el usuario escribe o selecciona opciones, los valores se cargan dentro de este objeto.

```jsx
const [formData, setFormData] = useState({});

const handleSubmit = async () => {
	const inventoryForm = {
		name: formData["Nombre del Inventario"],
		description: formData["Descripcion del Inventario"],
		revision_date: formData["Fecha de revision"],
		attributesIds: selectedAttributes,
	};
	
	try {
		await onSubmit(inventoryForm);
		close();
	} catch (e) {
		console.error("Failed to create inventory:", e);
	}
};

<DynamicForm 
	fields={fields}
	values={formData}
	onChange={handleChange}
	formDirection="grid-3"
/>
```

En este ejemplo, se crea un objeto `inventoryForm` con los datos del formulario.  
Los valores se obtienen del `formData` usando las claves definidas en los `fields`.  
El `useState` mantiene el estado actual del formulario.

---
## onChange

Este parámetro define cómo se actualizan los valores dentro del estado del componente padre.  
Debe ser una función que reciba dos parámetros: el **nombre del campo** y su **nuevo valor**, y actualice el estado.

```js
const handleChange = (name, value) => {
	setFormData({ ...formData, [name]: value });
};
```

Cada vez que el usuario modifica un campo, el componente ejecuta `onChange(field.name, e.target.value)`.  
De esta manera, el componente padre mantiene sincronizado el objeto `formData`.

---
## formDirection

Controla la disposición visual de los campos dentro del formulario.  
El componente soporta varias configuraciones predefinidas:

|Valor|Descripción|
|---|---|
|`"column"`|Muestra los campos en una sola columna|
|`"row"`|Muestra los campos en una fila|
|`"grid-2"`|Distribuye los campos en dos columnas|
|`"grid-3"`|Distribuye los campos en tres columnas|
|`"default"`|Equivalente a `"column"`|

Ejemplo:

```jsx
<DynamicForm 
	fields={fields}
	values={formData}
	onChange={handleChange}
	formDirection="grid-2"
/>
```

Esto define una grilla de dos columnas donde los campos se distribuyen automáticamente.  
Los estilos se gestionan desde el archivo `DynamicForm.css`.

---
## Ejemplo completo


```jsx
import React, { useState } from "react";
import DynamicForm from "../components/DynamicForm";

function Inventories() {
  const [formData, setFormData] = useState({});

  const handleChange = (name, value) => {
    setFormData({ ...formData, [name]: value });
  };

  const fields = [
    { 
      label: "Nombre del Inventario",
      name: "Nombre del Inventario",
      type: "text",
      placeholder: "Nombre del Inventario..." 
    },
    { 
      label: "Descripcion del Inventario",
      name: "Descripcion del Inventario",
      type: "text",
      placeholder: "Descripcion del inventario..."
    },
    { 
      label: "Fecha de revision",
      name: "Fecha de revision",
      type: "date"
    }
  ];

  const handleSubmit = () => {
    console.log("Datos del formulario:", formData);
  };

  return (
    <div>
      <h2>Crear nuevo inventario</h2>
      <DynamicForm 
        fields={fields} 
        values={formData} 
        onChange={handleChange} 
        formDirection="grid-3" 
      />
      <button onClick={handleSubmit}>Guardar</button>
    </div>
  );
}

export default Inventories;
```
Perfecto.  
Aquí tienes la documentación en formato **Markdown** siguiendo exactamente el mismo estilo, tono y estructura que el documento anterior (`DynamicForm.js`). Explica el uso del componente, los parámetros y cierra con un ejemplo completo de implementación.

---
# Button.js
El componente **Button.js** centraliza la creación de botones reutilizables con estilos y tamaños predefinidos.  
Su propósito es mantener una interfaz coherente sin necesidad de definir manualmente los estilos para cada botón.

### Ejemplo de uso

```jsx
<Button
  icon="pi pi-trash"
  onClick={onDelete}
  color="secondary-inverse"
  name="Eliminar"
/>
```

A continuación se detallan los parámetros que se utilizan.

---
## Props

### type

Define el tipo de botón.  
Afecta principalmente al radio de borde y, en algunos casos, al estilo general.

| Valor           | Descripción                                                    |
| --------------- | -------------------------------------------------------------- |
| `"default"`     | Botón estándar con bordes redondeados.                         |
| `"icon-button"` | Botón diseñado para contener únicamente íconos (más compacto). |
| `"tab"`         | Botón diseñado para destacar sobre los demás.                  |

Ejemplo:

```jsx
<Button type="tab" name="Configuraciones" />
```

---
### size

Controla el tamaño del botón.  
Afecta la altura, el ancho y, en el caso de botones con íconos, el tamaño del ícono.

|Valor|Descripción|
|---|---|
|`"small"`|Tamaño pequeño.|
|`"medium"`|Tamaño intermedio.|
|`"large"`|Tamaño grande.|
|`"default"`|Tamaño por defecto, equivalente a `"medium"`.|

Ejemplo:

```jsx
<Button type="icon-button" size="small" icon="pi pi-plus" />
```

---

### color

Define el color del fondo y del texto del botón.  
Los colores están basados en el sistema de diseño **Material Deisgn** y variables CSS definidas en `Button.css`.

| Valor                   | Descripción                                         |
| ----------------------- | --------------------------------------------------- |
| `"primary"`             | Color principal del tema.                           |
| `"primary-container"`   | Variante más clara del primario.                    |
| `"secondary"`           | Color secundario.                                   |
| `"secondary-container"` | Variante más clara del secundario.                  |
| `"tertiary"`            | Color terciario.                                    |
| `"tertiary-container"`  | Variante más clara del terciario.                   |
| `"primary-inverse"`     | Variante inversa del primario (colores invertidos). |
| `"secondary-inverse"`   | Variante inversa del secundario.                    |

Ejemplo:

```jsx
<Button color="tertiary" name="Guardar" />
```

---

### name

Texto visible dentro del botón.  
Si no se define, el botón mostrará únicamente el ícono (si se usa `icon`).

```jsx
<Button name="Aceptar" />
```

---

### icon

Define el ícono mostrado dentro del botón.  
Utiliza clases de **PrimeIcons** (por ejemplo: `"pi pi-trash"`, `"pi pi-plus"`, `"pi pi-pencil"`).  
El ícono se ajusta automáticamente en tamaño según el `size` del botón.

```jsx
<Button icon="pi pi-pencil" color="primary" />
```

---

### onClick

Función que se ejecuta al presionar el botón.  
Generalmente definida por el componente padre.

```jsx
<Button name="Eliminar" icon="pi pi-trash" onClick={handleDelete} />
```

---
## Ejemplo completo

A continuación se muestra un ejemplo completo de uso dentro de un componente funcional:

```jsx
// src/components/MenuLateral.js
import React from "react";
import Button from "./Button";

function MenuLateral({ titulo = "default", elementos, onCreate, onDelete }) {
  return (
    <aside className="menu-lateral">
      <h3>{titulo}</h3>

      <div className="menu-lateral--acciones">
        <Button
          icon="pi pi-plus"
          onClick={onCreate}
          color="primary"
          name="Nuevo"
        />

        <Button
          icon="pi pi-trash"
          onClick={onDelete}
          color="secondary-inverse"
          name="Eliminar"
        />

		{/* Este boton no hace nada pq no tiene definido el onClick xd */}
        <Button
          type="icon-button"
          size="small"
          icon="pi pi-cog"
          color="tertiary"
        />
      </div>
    </aside>
  );
}

export default MenuLateral;
```
---

# Modal2.js

El componente **Modal2.js** gestiona una ventana modal reutilizable que puede contener cualquier contenido interno.  
Su objetivo es ofrecer un contenedor flexible para mostrar formularios, confirmaciones o vistas personalizadas, controlado completamente desde el componente padre.

### Ejemplo de uso

```jsx
<Modal
  isOpen={isOpen}
  onClose={() => setIsOpen(false)}
  title="Eliminar Inventario"
  actions={[
    { label: "Cancelar", 
      onClick: (close) => close(), 
      color: "secondary", 
      size: "small" 
    },
    { label: "Eliminar",
      onClick: handleDelete,
      color: "primary",
      size: "small"
    },
  ]}
>
  <div>¿Desea eliminar este inventario?</div>
</Modal>
```

A continuación se detallan los parámetros que se utilizan.

---
## Props

### isOpen

Controla la visibilidad de la modal.  
Si `isOpen` es `true`, se muestra la ventana; si es `false`, se cierra.

Internamente utiliza una referencia (`useRef`) al elemento `<dialog>` y ejecuta `showModal()` o `close()` según el valor de esta prop.

```jsx
useEffect(() => {
  const dialog = dialogRef.current;
  if (isOpen) dialog.showModal();
  else dialog.close();
}, [isOpen]);
```

---
### onClose

Función que se ejecuta al cerrar la modal.  
Generalmente, esta función cambia el estado `isOpen` a `false` desde el componente padre.  
También se invoca cuando el usuario hace clic fuera del contenido o presiona “Esc”.

```jsx
<Modal isOpen={isOpen} onClose={() => setIsOpen(false)} />
```

El componente la usa en distintos puntos:

- Evento `onCancel` del `<dialog>`.
    
- Clic sobre el fondo oscuro (`overlay`).
    
- Botón de cierre (la “X” en la esquina superior).
    

---
### title

Texto que aparece en la cabecera de la modal.  
Si no se define, simplemente no se muestra un título.

```jsx
<Modal title="Agregar Artículo" />
```

---
### children

Define el contenido principal del cuerpo de la modal.  
El componente admite tres tipos de contenido:

1. **Función render-prop:**  
    Se recibe un hijo que es una función que recibe como parámetro `close` permitiendo al hijo cerrar la modal.    
```jsx
	<Modal>{({ close }) => <Form close={close} />}</Modal>
```
    
2. **Elemento React:**  
    Si el `children` es un componente, se clona e inyecta la prop `close`.
    
```jsx
	<Modal><FormularioInventario /></Modal>
```
    
3. **Contenido estático:**  
    Puede ser texto o cualquier nodo JSX.
    
```jsx
	<Modal><div>¿Está seguro de eliminar?</div></Modal>
```

---
### actions

Arreglo de botones que aparecen en el pie de la modal.  
Cada elemento del arreglo define un botón usando el componente **Button.js**.  
Cada acción es un objeto con la siguiente estructura:

```jsx
[
	{
	  label: "Texto del botón 1",
	  onClick: (close) => { destruirElMundo() },
	  color: "primary",
	  size: "large"
	},
	{
	  label: "Texto del botón 2",
	  onClick: (close) => { cocinarTorta() },
	  color: "secondary",
	  {/* Si no le pongo size se usa el default */}
	},
]
```

El parámetro `close` se pasa automáticamente a `onClick` para permitir cerrar la modal desde la acción.

Ejemplo:

```jsx
actions={[
  { label: "Cancelar",
    onClick: (close) => close(),
    color: "secondary",
    size: "small"
  },
  { label: "Confirmar",
    onClick: handleConfirm,
    color: "primary",
    size: "small"
  },
]}
```

---
## Ejemplo completo (simplificado)

```jsx
import React, { useState } from "react";
import Modal from "../components/Modal2";
import Button from "../components/Button";

function EjemploModal() {
  const [isOpen, setIsOpen] = useState(false);

  const acciones = [
    { label: "Cancelar", onClick: (close) => close(), color: "secondary", size: "small" },
    { label: "Aceptar", onClick: (close) => { alert("Acción confirmada"); close(); }, color: "primary", size: "small" },
  ];

  return (
    <div>
      <Button name="Abrir modal" color="primary" onClick={() => setIsOpen(true)} />

      <Modal
        isOpen={isOpen}
        onClose={() => setIsOpen(false)}
        title="Confirmar acción"
        actions={acciones}
      >
        <div>¿Desea continuar con esta acción?</div>
      </Modal>
    </div>
  );
}

export default EjemploModal;
```

En este ejemplo, el botón “Abrir modal” muestra la ventana.  
La modal incluye un texto simple y dos acciones: **Cancelar** (cierra la ventana) y **Aceptar** (muestra una alerta y luego la cierra).  
Toda la lógica de visibilidad se controla mediante el estado `isOpen`.
