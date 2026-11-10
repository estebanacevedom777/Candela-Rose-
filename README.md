# **Candela Rose**
Negocio


Candela Rose es una tienda que vende celulares y accesorios para celulares. El sistema permite registrar productos y clientes, vender varios productos en una misma compra, controlar el inventario y emitir un comprobante.

# **Tipos de producto (precio calculado)**

Celular :  Son los teléfonos que vendemos. De cada uno guardamos la marca, cuánto almacenamiento tiene y cuántos meses de garantía extendida lleva. Como la garantía tiene un costo, el precio final sube un 1% del precio base por cada mes que el cliente la extienda. Por ejemplo, un celular de $1.000.000 con 12 meses de garantía se vende en $1.120.000.

Accesorios : Son las fundas, los cargadores, los audífonos y todo lo que acompaña al celular. De cada uno guardamos su categoría y el descuento que tiene. Aquí el precio baja en lugar de subir: un accesorio de $50.000 con 10% de descuento se vende en $45.000.

La diferencia entre estos dos : Un celular es un producto que se encarece según la garantía, y un accesorio es un producto que se abarata según su descuento. Los dos son productos y comparten sus datos básicos, pero cada uno hace su propia cuenta para saber cuánto vale, y eso es lo que muestra la herencia y el polimorfismo en el código.

# **Paquete modelo** 


 .Producto es la clase base de todo lo que se vende. Es abstracta: guarda el código, el nombre, el precio base y las existencias, y obliga a sus hijas a decir cómo calculan su precio de venta mediante el método calcularPrecioVenta().


.Celular es un tipo de producto. Además de los datos comunes, guarda la marca, el almacenamiento y los meses de garantía extendida. Su precio sube según esa garantía.


.Accesorio es el otro tipo de producto. Guarda su categoría y su descuento, y su precio baja según ese descuento.


.Cliente representa a quien compra. Guarda el documento, el nombre y el teléfono.


.ItemVenta es una línea de la venta: un producto con la cantidad que se llevó. Sabe calcular su propio subtotal.


.Venta junta todo: el número, el cliente, sus ítems y el medio de pago. Calcula el subtotal, el IVA y el total, y muestra el comprobante.


MedioPago es una interfaz que dice qué debe saber hacer cualquier forma de pagar: procesar un pago.


Efectivo es una forma de pagar. Revisa que el valor recibido alcance y calcula el cambio.


Tarjeta es la otra forma de pagar. Aplica un recargo sobre el total.

# Paquete logica

.Inventario guarda la lista de productos. Permite registrarlos, buscarlos por código, actualizar su precio, descontar existencias al vender y listar los que se están acabando.


.GestorClientes guarda la lista de clientes. Permite registrarlos y buscarlos por número de documento.


.GestorVentas guarda la lista de ventas. Crea cada venta, lleva el número consecutivo del recibo y la constante del IVA, y arma el reporte con el número de ventas y el total vendido.

# **Paquete ejecucion**

.Main es la clase que arranca el programa. Carga los productos y clientes iniciales y muestra el menú, que permite usar todas las funciones sin reiniciar.

# **Relaciones**

Herencia: Celular y Accesorio extienden Producto.

Realización: Efectivo y Tarjeta implementan MedioPago.

Composición: Venta contiene sus ItemVenta, que no existen sin ella.

Asociación: Venta con Cliente y con MedioPago, e ItemVenta con Producto.

# **Cobertura de los requisitos funcionales**

RF1, gestión de productos. La clase Inventario guarda la lista de productos y permite registrarlos, buscarlos por código y actualizar su precio. Los dos tipos de producto, Celular y Accesorio, calculan su precio de venta de forma distinta.

RF2, control de inventario. Inventario también descuenta las existencias al vender mediante descontarExistencias, que rechaza la venta con un mensaje si se pide más de lo que hay. El método listarExistenciasBajas muestra los productos que están por debajo del mínimo que defina el equipo.

RF3, gestión de clientes. GestorClientes permite registrar clientes, listarlos y buscarlos por número de documento. Para las ventas sin cliente registrado se usa un cliente general precargado.

RF4, registro de ventas. Venta recibe varios ítems con agregarItem y calcula el subtotal de cada uno, el subtotal de la venta, el IVA del 19% y el total. El pago se hace con Efectivo o Tarjeta, las dos formas de pagar que implementan MedioPago.

RF5, comprobante de venta. Venta muestra el recibo con imprimirComprobante. Ahí aparecen el número consecutivo, que genera GestorVentas, el cliente, los ítems con su cantidad y subtotal, el subtotal de la venta, el IVA, el total y el medio de pago.

RF6, reporte de ventas. GestorVentas guarda todas las ventas de la ejecución y su método reporte las lista junto con el número de ventas y el total vendido.

RF7, menú de consola. Main muestra un menú que da acceso a todas las funciones sin reiniciar el programa. Si el usuario elige una opción que no existe, muestra un mensaje y vuelve al menú. Al arrancar carga datos precargados: al menos cinco productos de los dos tipos y dos clientes.

# **Cobertura de los requisitos técnicos**

RT1, clases y objetos. El sistema tiene doce clases propias, además de Main, que contiene el main.

RT2, encapsulamiento. Todos los atributos son private. Solo se crean get y set donde se necesitan, y los set validan que no entren precios, cantidades ni existencias negativas.

RT3, constructores y this. Cada clase del paquete modelo tiene un constructor que inicializa su estado usando this.

RT4, referencias y null. Los métodos buscarPorCodigo y buscarPorDocumento devuelven null cuando no encuentran el elemento. Antes de usar el resultado, el código revisa ese null.

RT5, paquetes. El código se divide en modelo, logica y ejecucion, cada uno con una responsabilidad separada.

RT6, colecciones. Se usan ArrayList en Inventario para los productos, en GestorClientes para los clientes, en GestorVentas para las ventas y dentro de cada Venta para sus ítems.

RT7, herencia. Producto es la superclase, y Celular y Accesorio son sus dos subclases.

RT8, polimorfismo. Celular y Accesorio sobrescriben calcularPrecioVenta() con @Override, y ese método se invoca sobre una lista declarada como lista de Producto.

RT9, abstracción. MedioPago es una interfaz con dos implementaciones, Efectivo y Tarjeta. Además, Producto es una clase abstracta con un método abstracto.

RT10, static. El número consecutivo del recibo y la constante del IVA son static y viven en GestorVentas.



