ACTIVIDAD FORMATIVA Nº2

Diseñando un e-commerce con inteligencia artificial.


Nombre: EcoRetro

Descripción: Es una tienda que comercializa todo lo retro y vintage. Al ser de este tipo creemos que son reutilizables y sustentables y de ahí viene la palabra Eco, unida del tipo Retro, que proviene de lo antiguo o anterior.

La utilización de la clave que se utilizó hace referencia directa al dato principal del ecommerce, en este caso, el producto. Por eso mismo se eligió “id_producto” como clave.


La IA es una herramienta que al utilizarse de manera correcta puede ayudar de maneras increíbles tanto a realizar proyectos como para aprender a hacerlos desde el principio. 
 Facilita la conversión o creación de código como es en este caso y también nos enseña como funciona cada parte del mismo. Ahorra tiempo y facilita la comprensión de problemáticas complicadas.

Código:

# ==========================================
# RETROVERSE E-COMMERCE - ALGORITMOS Y ED
# ==========================================

# 1. DEFINICIÓN DEL REGISTRO PRINCIPAL
# Creamos la clase 'ProductoRetro' que actúa como la estructura de nuestro registro.
class ProductoRetro:
    # El método __init__ es el constructor; define qué campos guardará cada registro.
    def __init__(self, id_producto, nombre, categoria, año_fabricacion, precio, stock, estado_conservacion):
        # Asignamos cada parámetro al campo correspondiente del registro y forzamos su tipo de dato:
        self.id_producto = str(id_producto)          # CLAVE PRIMARIA: Texto (String) único para identificar el objeto.
        self.nombre = str(nombre)                    # Texto (String): Nombre comercial del artículo.
        self.categoria = str(categoria)              # Texto (String): Categoría a la que pertenece (ej: Consolas).
        self.año_fabricacion = int(año_fabricacion)  # Entero (Integer): Año de lanzamiento original.
        self.precio = float(precio)                  # Decimal (Float): Costo del producto en la tienda.
        self.stock = int(stock)                      # Entero (Integer): Cantidad de unidades físicas disponibles.
        self.estado_conservacion = str(estado_conservacion) # Texto (String): Estado físico actual del artículo vintage.

# 2. INICIALIZACIÓN DEL CATÁLOGO (Simulación de Base de Datos)
# Inicializamos un diccionario vacío. Usaremos la CLAVE del registro como 'key' del diccionario 
# para lograr búsquedas directas e instantáneas (Complejidad O(1)).
catalogo_retroverse = {}

# Función auxiliar para dar de alta o insertar un nuevo registro en nuestra estructura de datos.
def registrar_producto(producto):
    # Guardamos el objeto 'producto' en el diccionario usando su campo 'id_producto' como clave de acceso.
    catalogo_retroverse[producto.id_producto] = producto

# Instanciamos (creamos) tres registros de ejemplo con datos retro y los guardamos en el catálogo.
registrar_producto(ProductoRetro("RETRO-001", "Consola Atari 2600", "Consolas", 1977, 180.00, 2, "Excelente"))
registrar_producto(ProductoRetro("RETRO-002", "Cámara Polaroid Sun 600", "Fotografía", 1981, 85.50, 5, "Bueno"))
registrar_producto(ProductoRetro("RETRO-003", "Walkman Sony TPS-L2", "Audio", 1979, 320.00, 1, "Colección - Como nuevo"))

# 3. INTERFAZ EN CONSOLA DEL E-COMMERCE
# Función que simplemente imprime en pantalla el menú de opciones disponibles para el usuario.
def mostrar_menu():
    print("\n--- BIENVENIDO A RETROVERSE E-COMMERCE ---")
    print("1. Ver catálogo completo")
    print("2. Buscar producto por CLAVE (ID)")
    print("3. Salir")

# Función para recorrer y mostrar todos los registros almacenados en el catálogo.
def mostrar_catalogo():
    print("\n--- CATÁLOGO DE PRODUCTOS VINTAGE ---")
    # .values() nos devuelve cada uno de los objetos de tipo 'ProductoRetro' guardados en el diccionario.
    for prod in catalogo_retroverse.values():
        # Imprimimos los campos principales del registro formateados en una sola línea de texto.
        print(f"[{prod.id_producto}] {prod.nombre} | Cat: {prod.categoria} | Precio: ${prod.precio} | Estado: {prod.estado_conservacion}")

# Función principal que demuestra la utilidad de haber definido una CLAVE única para el registro.
def buscar_por_clave():
    # Solicitamos al usuario que escriba la clave a buscar y la transformamos a mayúsculas con .upper().
    clave = input("\nIngrese la CLAVE (ID) del producto a buscar: ").upper()
    
    # Validamos si la clave ingresada existe dentro de los índices del diccionario de manera directa.
    if clave in catalogo_retroverse:
        # Si existe, recuperamos el registro completo asociado a esa clave en una variable 'p'.
        p = catalogo_retroverse[clave]
        # Mostramos detalladamente el valor de cada uno de los campos de ese registro específico.
        print(f"\n¡Producto Encontrado!")
        print(f"----------------------------------------")
        print(f"ID (Clave): {p.id_producto}")
        print(f"Nombre:     {p.nombre}")
        print(f"Año:        {p.año_fabricacion}")
        print(f"Precio:     ${p.precio}")
        print(f"Stock:      {p.stock} unidades")
        print(f"Estado:     {p.estado_conservacion}")
        print(f"----------------------------------------")
    else:
        # Si la clave no coincide con ningún registro, informamos el error.
        print("\n❌ Error: No se encontró ningún artículo con esa clave.")

# BUCLE PRINCIPAL DE LA APLICACIÓN (Control de flujo)
# Un ciclo infinito 'while True' que mantiene la aplicación ejecutándose hasta que el usuario decida salir.
while True:
    mostrar_menu() # Desplegamos el menú de opciones en cada iteración.
    opcion = input("Seleccione una opción (1-3): ") # Capturamos la decisión del usuario.
    
    # Estructura condicional para evaluar la opción seleccionada:
    if opcion == "1":
        mostrar_catalogo() # Llama a la función que lista todos los registros.
    elif opcion == "2":
        buscar_por_clave() # Llama a la función de búsqueda indexada por clave primaria.
    elif opcion == "3":
        # Despedida y cierre del programa rompiendo el bucle 'while' con la instrucción 'break'.
        print("\n¡Gracias por visitar RetroVerse! Apagando sistemas antiguos...")
        break
    else:
        # Manejo de excepciones para cuando ingresan una opción que no figura en el menú.
        print("\nOpción inválida. Intente de nuevo.")
