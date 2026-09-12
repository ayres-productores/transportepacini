# Qué hay en cada nave — Buenos Aires y San Lorenzo

Simulador paso a paso (5 minutos por paso) de dos sucursales de una red logística,
con una pestaña por nave que muestra el estado en cada momento: paquetes sueltos,
pallets armándose, camiones en playa o en ruta, pallets por desarmar, colas de
logueo y clasificación, paquetes listos por localidad y la flota de reparto.

Un solo archivo estático (`index.html`), sin build, sin dependencias.
Las tipografías se cargan de Google Fonts y degradan a fuentes del sistema si no hay red.

## Publicar en Cloudflare Pages

- Build command: *(vacío)*
- Build output directory: `/`
- Production branch: `main`

## Estructura

    index.html   la aplicación completa (HTML + CSS + JS)
    _headers     cabeceras que aplica Cloudflare Pages

## Modelo

**Buenos Aires (receptoría y consolidación)**

1. Llegadas Poisson por hora dentro del horario de recepción; cada paquete nace con tamaño (S/M/L) y destino según pesos.
2. Un pallet abierto por vez, se llena al ritmo de armado; se cierra por capacidad o por edad máxima.
3. Camiones de línea (lista editable): cada uno sale cuando junta su capacidad en pallets o cuando el pallet cerrado más viejo venció la espera máxima. Viaje con ruido lognormal; descarga en San Lorenzo y vuelve.

**San Lorenzo (centro de distribución y despacho)**

4. Desarme de pallets, logueo (lectura de dirección) y clasificación (tamaño + vehículo viable): tres colas FIFO en serie con su tasa, activas sólo dentro del turno.
5. Paquetes listos por localidad. Los que no admite ningún vehículo quedan apartados.
6. Flota de reparto (lista editable de tipos: unidades, tamaños admitidos, capacidad, horarios de salida, velocidad, minutos por parada). En cada salida cada unidad libre carga un solo destino y entrega parada a parada.

La semilla fija el azar: con el mismo número, el mismo resultado. Las tasas se pueden cambiar mientras corre; agregar o quitar camiones, destinos o vehículos reinicia la corrida.
