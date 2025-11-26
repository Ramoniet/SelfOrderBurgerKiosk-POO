# 🍔 Burger Self-Ordering Kiosk

> **Proyecto desarrollado para la asignatura de Programación Orientada a Objetos.**

## 📘 Descripción General

Este proyecto implementa una simulación de un **kiosco de autoservicio para una hamburguesería** (estilo McDonald's). El sistema guía al usuario a través de una interfaz gráfica interactiva que permite seleccionar el idioma, navegar por el catálogo de productos, personalizar menús, gestionar el pedido y finalizar la compra mediante una pasarela de pago simulada.

---

## ⚙️ Requisitos y Configuración

⚠️ **IMPORTANTE:** Para ejecutar el proyecto, asegúrate de que el directorio de trabajo (Working Directory) contenga los siguientes recursos:

* **`Catalog.xml`**: Base de datos con la estructura de la carta (Secciones, Productos y Menús).
* **Archivos de Idioma**: `espanol.txt`, `ingles.txt`, `frances.txt`, `aleman.txt`.
* **`Discount.txt`**: Fichero de configuración para promociones.
* **Carpeta `PRODUCTOS/`**: Contiene las imágenes de las hamburguesas y complementos.
* **Librerías**: `BurgerSelfOrderKioskSimulator.jar` y `UrjcBankServer.jar`.

---

## 🧩 Arquitectura del Sistema

El código se organiza en paquetes diferenciados para separar la lógica de negocio, los datos y la interfaz de usuario.

### 📦 Paquete `aplicaciónmcdonalds` (Core)
Controladores principales y gestión del flujo:
* **`BurgerSelfOrderKiosk`**: Clase principal (`main`) que inicializa la aplicación y la ventana gráfica.
* **`KioskManager`**: Controlador central (Patrón Singleton/Manager) que orquesta el cambio entre pantallas.
* **`Context`**: Almacena el estado global de la sesión (usuario actual, pedido en curso, idioma seleccionado).
* **`SimpleKiosk`**: Fachada para comunicar nuestra lógica con el simulador gráfico externo.
* **`TranslatorManager` / `Translator`**: Motor de internacionalización que carga los ficheros `.txt` según el idioma.

### 🍔 Paquete `products` (Modelo)
Representación de los datos del dominio:
* **`MenuCard`**: Parsea y almacena la estructura completa de la carta leída desde el XML.
* **`MenuCardSection`**: Representa las categorías (ej. Hamburguesas, Bebidas).
* **`Product`** (Abstracta): Clase base para todos los ítems vendibles.
    * **`IndividualProduct`**: Productos sueltos (ej. Coca-Cola, Big Mac).
    * **`Menu`**: Conjunto de productos con un precio agrupado.
* **`Order`**: Gestiona la lista de productos seleccionados por el cliente y el cálculo del total.

### 🖥️ Paquete `screens` (Vista/Controlador de UI)
Clases que gestionan la lógica de cada pantalla específica (heredan de `KioskScreen`):

* **`WelcomeScreen`**: Pantalla de atracción inicial (Toque para empezar).
* **`LanguageScreen`**: Selección de idioma (Español, Inglés, Francés, Alemán).
* **`OrderScreen`**: Pantalla principal del pedido (Comer aquí / Para llevar).
* **`SectionScreen`**: Vista de las categorías de la carta.
* **`CarouselScreen`**: Lógica base para pantallas que muestran listas rotativas de elementos.
* **`ProductScreen`**: Detalle para añadir productos individuales.
* **`MenuScreen`**: Configuración y selección de los componentes de un menú.
* **`FreeProductScreen`**: Pantalla especial para gestión de promociones o regalos.
* **`PurchaseScreen`**: Resumen final, validación y pago con tarjeta.

---

## 🔁 Flujo del Usuario

1.  **Inicio**: Animación de bienvenida (`WelcomeScreen`).
2.  **Configuración**: El usuario selecciona su idioma preferido (`LanguageScreen`).
3.  **Tipo de Pedido**: Selección de "Para llevar" o "Tomar aquí" (`OrderScreen`).
4.  **Catálogo**: Navegación por secciones (`SectionScreen`) y selección de ítems en carrusel.
5.  **Personalización**:
    * Si es un producto suelto -> `ProductScreen`.
    * Si es un menú completo -> `MenuScreen`.
6.  **Promociones**: Posibilidad de añadir productos gratuitos si aplica (`FreeProductScreen`).
7.  **Cierre**: Revisión del carrito y pago simulado (`PurchaseScreen`).

---

## ✨ Funcionalidades Destacadas

### 🌐 Internacionalización Completa
El sistema soporta 4 idiomas dinámicos. Las cadenas de texto no están "harcodeadas", sino que se cargan mediante `TranslatorManager` desde los ficheros de texto externos.

### 💳 Simulación de Pago Realista
Integración con `UrjcBankServer` para simular la comunicación con una entidad bancaria, validando números de tarjeta de crédito durante el proceso de compra.

### 🖼️ Carga Dinámica de Recursos
Las imágenes y descripciones de los productos se cargan dinámicamente leyendo el fichero `Catalog.xml`, lo que permite modificar la oferta gastronómica sin recompilar el código.

---

## 👨‍💻 Autor

**Ramón Nieto Villegas**
**Raúl Tejada Merinero**
**Jorge Naranjo Ballesteros**
