# Python
Paciencia


class Producto:
    def __init__(self, nombre, cantidad, precio):
        self.nombre = nombre
        self.cantidad = cantidad
        self.precio = precio

    def actualizar_cantidad(self, cantidad):
        self.cantidad += cantidad

    def mostrar_detalles(self):
        print(f"Producto: {self.nombre}, Cantidad: {self.cantidad}, Precio: ${self.precio:,.2f}")


class TallerFinal:
    def __init__(self):
        self.productos = []

    def buscar_producto(self, nombre):
        for producto in self.productos:
            if producto.nombre == nombre:
                return producto
        return 

    def agregar_producto(self):
        total = 0
        while True:
            nombre = input("Nombre del producto: ")
            cantidad = int(input("Cantidad: "))
            precio = float(input("Precio por unidad: "))
            subtotal = cantidad * precio
            total += subtotal

            producto = self.buscar_producto(nombre)
            if producto:
                print(f"Actualizando cantidad del producto '{nombre}'.")
                producto.actualizar_cantidad(cantidad)
            else:
                print(f"Agregando producto '{nombre}' al inventario.")
                self.productos.append(Producto(nombre, cantidad, precio))

            print(f"Producto agregado o actualizado. Subtotal: ${subtotal:,.2f}")
            if input("¿Deseas agregar otro producto? (si/no): ").lower() != 'si':
                break
        print(f"Total a pagar por los productos agregados: ${total:,.2f}")

    def realizar_venta(self):
        nombre = input("Nombre del producto a vender: ")
        cantidad = int(input("Cantidad a vender: "))
        producto = self.buscar_producto(nombre)

        if producto:
            if producto.cantidad >= cantidad:
                producto.actualizar_cantidad(-cantidad)
                print(f"Venta realizada: {cantidad} unidades de '{nombre}'.")
            else:
                print(f"No hay suficiente cantidad de '{nombre}' para la venta.")
        else:
            print(f"El producto '{nombre}' no existe en el inventario.")

    def consultar_inventario(self):
        if self.productos:
            print("Inventario actual:")
            for producto in self.productos:
                producto.mostrar_detalles()
        else:
            print("El inventario está vacío.")

    def verificar_stock(self):
        umbral = int(input("Umbral de stock bajo: "))
        productos_bajos = [p for p in self.productos if p.cantidad < umbral]

        if productos_bajos:
            print("Productos con stock bajo:")
            for producto in productos_bajos:
                producto.mostrar_detalles()
        else:
            print("No hay productos con stock bajo.")


def menu():
    taller = TallerFinal()
    opciones = {
        "1": taller.agregar_producto,
        "2": taller.realizar_venta,
        "3": taller.consultar_inventario,
        "4": taller.verificar_stock,
    }

    while True:
        print("\nMenú de opciones:")
        print("1. Agregar productos")
        print("2. Realizar venta")
        print("3. Consultar inventario")
        print("4. Verificar stock bajo")
        print("5. Salir")

        opcion = input("Selecciona una opción: ")
        if opcion == "5":
            print("Saliendo del programa.")
            break
        elif opcion in opciones:
            opciones[opcion]()
        else:
            print("Opción no válida, intenta nuevamente.")


menu()



