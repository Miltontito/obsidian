# DynamicForm.js
---
La idea del DynamicForm.js es ahorrarse el escribir un formulario de multiples campos. 

Ejemplo de uso:

```
<DynamicForm 
	fields={fields}
	values={formData}
	onChange={handleChange}
	formDirection = "grid-3"
/>
```

A continuación se detallan los parámetros que se utilizan:
## fields
Es uno de los parámetros obligatorios del componente, es un arreglo de objetos que generalmente siguen la misma estructura exceptuando los de tipo select, ejemplo:

```
const fields = [
	{ label: "Nombre del Inventario",
	  name: "Nombre del Inventario",
	  type: "text",
	  placeholder: "Nombre del Inventario..." 
	},
	{ label: "Descripcion del Inventario",
	  name: "Descripcion del Inventario",
	  type: "text",
	  placeholder: "Descripcion del inventario..."
	},
	{ label: "Fecha de revision",
	  name: "Fecha de revision",
	  type: "date"
	}
	{ label: "Tipo del Atributo",
	  name: "tipo-atributo",
	  type: "select",
	  options: ["opcion1", "opcion2", "opcion3", "opcion4"]
	}
];
```
Como se ve en el ejemplo, los objetos siguen la convención de atributo:valor, siendo los atributos **los mismos** que los tipos de input de html. (revisar la documentación de HTML, inputs y forms.)

Por ejemplo **type:"text"**  hace referencia al input de tipo texto de **HTML**, se pueden usar todos los tipos comunes de HTML, como mail, date, text, password, etc.
## values
Este parámetro se encarga de almacenar los datos escritos en los campos especificados, ya sean 2 campos de texto, uno de contraseña, otro de correo, etc. A este parámetro se cargaran los datos. 

Ejemplo:
```
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
	formDirection = "grid-3"
/>
```

En este caso se crea un objeto llamado inventoryForm (todos los objetos en javascript siguen la convención atributo:valor, este caso NO es la expeción).

Se cargan los datos como name usando el formData, para acceder a los datos del formData se hace a través del "name" que se definen en los "fields". 

Se usa un useState para almacenar el estado de los formularios.
