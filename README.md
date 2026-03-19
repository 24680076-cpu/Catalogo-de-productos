# Diagrama de Clases
Este diagrama representa la arquitectura de "Dulce Delirio". Muestra cómo la clase ProductoCard hereda de Flet y cómo se relaciona con los datos de la dataclass.

<img width="311" height="451" alt="image" src="https://github.com/user-attachments/assets/525cce13-97f5-4235-a1c7-20870aabe789" />
# Explicación de la Herencia
Para el desarrollo del componente personalizado ProductoCard, se utilizó la clase base ft.Container de Flet.

¿Por qué se eligió esta clase?

* Encapsulamiento: Al heredar de Container, pudimos agrupar dentro de un solo objeto visual todos los sub-controles (imágenes, textos y botones).

* Extensibilidad: Nos permitió definir propiedades estéticas globales (como el border_radius, bgcolor y shadow) directamente en el constructor (__init__), asegurando que cada tarjeta generada sea idéntica sin repetir código.

* Comportamiento nativo: La clase hija conserva todas las capacidades de un contenedor estándar, facilitando su inserción en layouts complejos como filas o columnas.
