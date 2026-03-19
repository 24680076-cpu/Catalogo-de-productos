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
# Codigo 
``` python
import flet as ft
from dataclasses import dataclass
from typing import Final

@dataclass
class Producto:
    id: int
    nombre: str
    descripcion: str
    precio: float
    ruta_imagen: str
    categoria: str

class ProductoCard(ft.Container):
    def __init__(self, producto: Producto):
        super().__init__()
        self.width = 250
        self.padding = 15
        self.border_radius = 15
        self.bgcolor = ft.Colors.WHITE  # Corregido: Colors
        self.shadow = ft.BoxShadow(blur_radius=15, color=ft.Colors.BLACK12) # Corregido: Colors
        self.border = ft.border.all(1, ft.Colors.BROWN_100) # Corregido: Colors

        self.content = ft.Column(
            tight=True,
            spacing=10,
            controls=[
                ft.Stack(
                    controls=[
                        ft.Image(
                            src=producto.ruta_imagen, 
                            width=220,
                            height=160,
                            fit="cover", 
                            border_radius=10
                        ),
                        ft.Container(
                            content=ft.IconButton(
                                icon=ft.Icons.FAVORITE_BORDER, # Corregido: Icons
                                icon_color=ft.Colors.RED_400,   # Corregido: Colors
                                icon_size=20,
                            ),
                            left=5,
                            top=5
                        )
                    ]
                ),
                ft.Column(
                    spacing=2,
                    controls=[
                        ft.Text(producto.nombre, size=18, weight="bold", color="brown900"),
                        ft.Text(producto.descripcion, size=12, color="grey700", max_lines=2, overflow="ellipsis"),
                    ]
                ),
                ft.Row(
                    alignment="spaceBetween", 
                    vertical_alignment="center", 
                    controls=[
                        ft.Text(f"${producto.precio:.2f}", size=18, weight="bold", color="brown700"),
                        ft.ElevatedButton(
                            "Agregar",
                            icon=ft.Icons.ADD_SHOPPING_CART, # Corregido: Icons
                            bgcolor="brown400",
                            color="white"
                        )
                    ]
                )
            ]
        )

def main(page: ft.Page):
    page.title = "Dulce Delirio - Menú"
    page.theme_mode = "light"
    page.bgcolor = "#FFFBF5"
    page.scroll = "adaptive"
    page.padding = 40
    
    page.appbar = ft.AppBar(
        title=ft.Text("DULCE DELIRIO", weight="bold", color="brown900"),
        bgcolor="brown50",
        center_title=True,
    )

    menu: Final[list[Producto]] = [
        Producto(1, "Frappé Mocha", "Delicioso café frío con chocolate.", 65.0, "frappe.png", "Frappé"),
        Producto(2, "Galleta Choco", "Galleta artesanal crujiente.", 25.0, "galleta.png", "Galleta"),
        Producto(3, "Pastel Red Velvet", "Suave bizcocho con crema.", 55.0, "pastel.png", "Pastel"),
        Producto(4, "Café Capuchino", "Café espresso con leche.", 35.0, "capuchino.png", "Café"),
        Producto(5, "Gelatina Cream", "Postre refrescante de leche.", 30.0, "gelatina.png", "Postre"),
    ]

    catalogo = ft.ResponsiveRow(
        spacing=30,
        run_spacing=30,
        controls=[
            ft.Column(
                [ProductoCard(p)],
                col={"xs": 12, "sm": 6, "md": 4, "lg": 3},
                horizontal_alignment="center"
            ) for p in menu
        ],
    )

    page.add(
        ft.Column([
            ft.Text("Nuestra Selección de Hoy", size=32, weight="bold", color="brown900"),
            ft.Divider(height=20, color="transparent"),
            catalogo
        ])
    )

if __name__ == "__main__":
    ft.app(target=main, assets_dir="assets")
``` 
# Captura  de Pantalla
<img width="1326" height="665" alt="image" src="https://github.com/user-attachments/assets/591a089c-184f-4ecd-8bd8-bd28c289f936" />

# Link de la pagina web en netlify
https://silly-lokum-08d706.netlify.app/
