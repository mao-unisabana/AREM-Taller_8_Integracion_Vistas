# Registro de Trabajo en Clase - Taller 8

## Fecha de la sesión
_Octubre de 2026 (completar con la fecha exacta de la clase)._

## Integrantes presentes
- Mao Suárez
- Nicolas Clavijo

## Actividades realizadas en clase

Se armó el tablero integrado de FarmApp siguiendo los 5 pasos de la guía, en draw.io ([`tablero-farmapp.drawio`](tablero-farmapp.drawio)), con una página por paso para que se lea sin hacer zoom:

| Página | Paso de la guía | Contenido |
|---|---|---|
| 0 · Capas | Pasos 1 y 2 | Las 5 capas con sus elementos, sin conexiones |
| 1 · Compra Online | Paso 3 | Hilo completo por las 5 capas |
| 2 · Prescripción | Paso 3 (repetido) | Mismo método sobre la validación de fórmulas |
| 3 · Despacho | Paso 3 (repetido) | Alistamiento, inventario y notificación |

**Decisiones de modelado que se discutieron:**

- **Las entidades sí bajan a infraestructura.** En el ejemplo de la guía, Producto/Cliente/Pedido/Descuento quedan sin conexión hacia abajo (la propia tabla del Paso 5 lo admite). En el tablero las cuatro entidades se conectan a la Base de Datos Replicada, para que la capa de Información no quede colgando.
- **La App Móvil consume la API del E-commerce** en vez de ir directo a la Nube Híbrida. Así el inventario y los descuentos tienen una sola fuente de verdad, que es justo el argumento de la narrativa de la guía ("evitar inconsistencias de inventario entre canales").
- **Cada control de seguridad se pega al dato que protege**, no a la aplicación en general: el cifrado al Cliente (datos personales), el monitoreo de fraude al Pedido (pago electrónico) y el control por rol a la Nube Híbrida.
- Con los tres hilos, **ningún elemento queda huérfano**: POS, CRM y Servidores Regionales, que no aparecen en Compra Online, quedan cubiertos por Prescripción y Despacho.

**Herramientas:** draw.io, con la paleta por capas al estilo ArchiMate (negocio amarillo, aplicación azul, información morado, infraestructura naranja, seguridad rojo).

## Boceto inicial del modelo

Ver [`tablero-farmapp.drawio`](tablero-farmapp.drawio).

**Narrativa del hilo Compra Online (Paso 4):** la compra entra por la App Móvil y la Plataforma E-commerce, pero las dos usan la misma API y por eso las mismas entidades (Producto, Cliente, Pedido, Descuento). Si cada canal tuviera su propia copia del inventario, un descuento o un agotado se vería distinto en la app y en la web. La plataforma corre en la Nube Híbrida, sobre la Base de Datos Replicada, para aguantar los picos de las campañas promocionales. El cifrado se ubica en Cliente y el monitoreo de fraude en Pedido porque ahí están los dos activos sensibles del flujo: los datos personales y el pago electrónico.

## Tareas definidas para complementar el taller

| Tarea asignada | Responsable | Fecha estimada |
|----------------|-------------|----------------|
| Tablero integrado de Asul (Parte 2) en draw.io | Mao Suárez | Antes de la siguiente sesión |
| Informe narrativo y tabla de verificación de huérfanos | Mao Suárez / Nicolas Clavijo | Antes de la siguiente sesión |
| Investigación de ejemplos de documentación de vistas | Nicolas Clavijo | Antes de la siguiente sesión |
| Validar con Alejandro los supuestos nuevos (agente de Pipelines, dónde vive la bitácora) | Mao Suárez | Antes del Taller 9 |

---

_Este documento resume el trabajo colaborativo realizado durante la sesión del taller 8 en el curso AREM - Universidad de La Sabana._
