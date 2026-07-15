# Fragmentación Técnica del Pedido

**Pedido original (Dev):**
> "Dev, quiero que los choferes vean viajes cercanos en tiempo real, pero que sea seguro y no se roben los datos. Y que si aceptan, les diga la ruta más corta para no gastar gas. Ah, y que la app no se trabe si hay 1,000 personas al mismo tiempo."

---

## 1. Requisitos No Funcionales (RNF)

| ID | Categoría | Requisito |
|----|-----------|-----------|
| RNF-01 | Seguridad | Todas las comunicaciones entre la app del chofer y el backend deben viajar cifradas (TLS 1.2+). |
| RNF-02 | Seguridad | Los datos de ubicación y viaje deben protegerse contra acceso no autorizado (autenticación por token, control de acceso por rol). |
| RNF-03 | Rendimiento | El sistema debe soportar al menos 1,000 usuarios concurrentes sin degradación perceptible (tiempo de respuesta < 2s en el 95% de las solicitudes). |
| RNF-04 | Disponibilidad | El servicio de viajes en tiempo real debe tener una disponibilidad mínima del 99.5%. |
| RNF-05 | Escalabilidad | La arquitectura debe permitir escalado horizontal (ej. balanceo de carga, colas de mensajes) para picos de demanda. |
| RNF-06 | Eficiencia | El cálculo de ruta más corta debe responder en menos de 3 segundos tras la aceptación del viaje. |
| RNF-07 | Usabilidad | La visualización de viajes cercanos debe actualizarse en tiempo real (latencia máxima de 5 segundos). |

---

## 2. Historias de Usuario

### Historia de Usuario 1

**Como** chofer registrado en la plataforma,
**Quiero** ver en un mapa los viajes cercanos disponibles en tiempo real,
**Para** poder elegir y aceptar el viaje más conveniente sin exponer mis datos ni los del pasajero.

**Criterios de aceptación (resumen):**
- Ver viajes solo dentro de un radio configurable (ej. 5 km).
- Los datos personales del pasajero no se muestran hasta que el chofer acepta el viaje.
- La lista/mapa se actualiza automáticamente sin recargar la app.

---

### Historia de Usuario 2

**Como** chofer que acaba de aceptar un viaje,
**Quiero** recibir automáticamente la ruta más corta hacia el punto de recogida y destino,
**Para** ahorrar combustible y tiempo en el trayecto.

**Criterios de aceptación (resumen):**
- El cálculo de ruta considera tráfico en tiempo real si está disponible.
- Se muestra distancia estimada y tiempo estimado.
- Si no hay conexión a datos, se muestra la última ruta calculada con aviso de "sin conexión".

---

## 3. Criterios de Aceptación en Gherkin

### Historia 1: Ver viajes cercanos en tiempo real

```gherkin
Característica: Visualización de viajes cercanos en tiempo real

  Escenario: El chofer ve viajes disponibles dentro de su radio
    Dado que el chofer tiene la app abierta y su ubicación activada
    Cuando existan viajes solicitados dentro de un radio de 5 km
    Entonces el chofer debe ver esos viajes reflejados en el mapa en un lapso máximo de 5 segundos

  Escenario: Los datos del pasajero permanecen protegidos antes de aceptar
    Dado que el chofer visualiza un viaje disponible en el mapa
    Cuando el chofer aún no ha aceptado el viaje
    Entonces el sistema no debe mostrar datos personales del pasajero (nombre completo, teléfono, dirección exacta)

  Escenario: La comunicación de datos está cifrada
    Dado que la app del chofer solicita la lista de viajes cercanos al servidor
    Cuando se realiza la petición
    Entonces la conexión debe utilizar TLS 1.2 o superior
```

### Historia 2: Ruta más corta al aceptar un viaje

```gherkin
Característica: Cálculo de ruta más corta tras aceptar un viaje

  Escenario: El chofer recibe la ruta óptima al aceptar
    Dado que el chofer ha aceptado un viaje
    Cuando el sistema procesa la aceptación
    Entonces debe mostrarse la ruta más corta disponible en un máximo de 3 segundos

  Escenario: La ruta considera el tráfico en tiempo real
    Dado que existe información de tráfico disponible para la zona
    Cuando se calcula la ruta
    Entonces el sistema debe priorizar la ruta con menor tiempo estimado, no solo la de menor distancia

  Escenario: Comportamiento sin conexión
    Dado que el chofer aceptó un viaje y luego pierde la conexión a datos
    Cuando la app no puede recalcular la ruta
    Entonces debe mostrarse la última ruta calculada junto con un aviso de "sin conexión"
```

### Requisito transversal: Carga de 1,000 usuarios concurrentes

```gherkin
Característica: Estabilidad de la app bajo alta concurrencia

  Escenario: 1,000 choferes conectados simultáneamente
    Dado que 1,000 choferes tienen la app abierta al mismo tiempo
    Cuando todos solicitan actualizaciones de viajes cercanos en el mismo intervalo
    Entonces el sistema debe responder sin caídas ni tiempos de espera mayores a 2 segundos en el 95% de las solicitudes
```

---

## 4. Notas de Proceso (Equipo)

1. **Trabajo en equipo:** este documento debe revisarse y validarse con el equipo del proyecto integrador antes de su implementación.
2. **Formato:** redactado en Markdown (`.md`) para integrarse directamente a la documentación técnica del repositorio.
3. **Entrega:** subir este archivo al repositorio Git del equipo antes del cierre, idealmente dentro de una carpeta `docs/` o `requisitos/`.
