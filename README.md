# Simulador de red logística — Buenos Aires → San Lorenzo

Simulación por eventos de una red de dos escalones: consolidación en origen,
tramo de línea, clasificación en el centro de distribución y reparto de última milla.

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

Seis etapas medidas por separado:

1. Espera de consolidación — disparador por cantidad `Q` o por espera máxima `T`
2. Espera de camión — utilización de la flota de línea
3. Tramo de línea — `distancia / velocidad` con ruido lognormal
4. Clasificación — cola FIFO a `operarios × paq/hora`, sólo dentro de la ventana de trabajo
5. Espera de corte — hasta el próximo horario de salida
6. Reparto — aproximación continua de ruteo, distancia entre paradas ≈ `0,57·√(A/n)`

La semilla fija el azar: con el mismo número, el mismo resultado.
