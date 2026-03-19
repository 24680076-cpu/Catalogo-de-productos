# Diagrama de Clases
Este diagrama representa la arquitectura de "Dulce Delirio". Muestra cómo la clase ProductoCard hereda de Flet y cómo se relaciona con los datos de la dataclass.

<img width="311" height="451" alt="image" src="https://github.com/user-attachments/assets/525cce13-97f5-4235-a1c7-20870aabe789" />

# Explicación de la Herencia
Para el desarrollo del componente personalizado ProductoCard, se utilizó la clase base ft.Container de Flet.

¿Por qué se eligió esta clase?

* Encapsulamiento: Al heredar de Container, pudimos agrupar dentro de un solo objeto visual todos los sub-controles (imágenes, textos y botones).

* Extensibilidad: Nos permitió definir propiedades estéticas globales (como el border_radius, bgcolor y shadow) directamente en el constructor (__init__), asegurando que cada tarjeta generada sea idéntica sin repetir código.

* Comportamiento nativo: La clase hija conserva todas las capacidades de un contenedor estándar, facilitando su inserción en layouts complejos como filas o columnas.
# Gestión de Recursos (Assets)
Para que el framework reconozca las imágenes de los postres, se realizó la siguiente configuración técnica:

* Estructura de Directorio: Se creó una carpeta raíz denominada assets/ al mismo nivel que el archivo main.py.

* Vinculación en el Código: En la función de arranque de la aplicación, se especificó el parámetro assets_dir="assets" dentro del método ft.app().

* Referencia Relativa: En la capa de datos (dataclass), las rutas de las imágenes se definieron de forma simplificada (ej. "frappe.png"). Flet, al estar configurado con el directorio de recursos, busca automáticamente estos archivos dentro de la carpeta mencionada, permitiendo que las imágenes se desplieguen correctamente tanto en modo escritorio como en el servidor web.
