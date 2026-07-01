# Parche: alertas falsas en sensores

Copia cada archivo de esta carpeta **sobre el original** en tu proyecto Monitoriza.

## Archivos incluidos

| Archivo en este parche | Destino en tu proyecto |
|------------------------|------------------------|
| `frontend/src/utils/constants.js` | `frontend/src/utils/constants.js` |
| `frontend/src/hooks/useSensors.js` | `frontend/src/hooks/useSensors.js` |
| `frontend/src/components/SensorCard.jsx` | `frontend/src/components/SensorCard.jsx` |
| `backend/src/main/resources/application.properties` | `backend/src/main/resources/application.properties` |

## Pasos

1. Haz copia de seguridad de los 4 archivos originales (por si acaso).
2. Copia y pega cada archivo de esta carpeta reemplazando el original.
3. Reinicia el **backend** (Spring Boot).
4. Reinicia el **frontend** (`npm run dev` en `frontend/`).
5. Verifica en `http://localhost:8080/api/mediciones/ultimas` que los datos vienen del nodo real.
6. Comprueba que en consola del backend **no** aparece `[Simulador] Medición guardada...`.

## Qué corrige

- Unifica el redondeo al mostrar y al evaluar alertas (evita falsos positivos en bordes del rango).
- Desactiva el simulador de mediciones (`app.simulador.mediciones.enabled=false`).
- Corrige la clave `db` en la detección de calibración del SensorCard.

## Verificación rápida

| Valor real del nodo | Debería mostrar | Estado |
|---------------------|-----------------|--------|
| Humedad 39.8        | 40.0            | NORMAL |
| Temperatura 22.04   | 22.0            | NORMAL |
| Lux 299.4           | 300             | NORMAL |
| Temperatura 22.1    | 22.1            | ALERTA |
| CO₂ 801             | 801             | ALERTA |
