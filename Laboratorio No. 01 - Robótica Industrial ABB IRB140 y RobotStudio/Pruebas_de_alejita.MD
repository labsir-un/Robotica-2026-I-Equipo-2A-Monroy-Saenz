```mermaid
flowchart TD

    A[Inicio] --> B[Loop infinito]

    B --> C{DI_03 = 1?}
    C -- Sí --> C1[Activar banda atrás\n(SET DO_03 + BWD_Conveyor)]
    C1 --> C2[Esperar 4s]
    C2 --> C3[Detener banda\n(RESET)]
    C3 --> B
    C -- No --> D{DI_01 = 1?}

    D -- Sí --> D1[Activar banda adelante]
    D1 --> D2[Esperar 4s]
    D2 --> D3[Detener banda]
    D3 --> D4[Esperar 5s]
    D4 --> D5[Activar herramienta (DO_01)]

    %% SECUENCIA DETALLADA
    D5 --> N1[Nombre integrante 1]
    N1 --> N2[Nombre integrante 2]
    N2 --> H[Corazón]

    H --> D6[Volver a Home]

    D6 --> D7[Activar banda adelante]
    D7 --> D8[Esperar 4s]
    D8 --> D9[Detener banda]
    D9 --> D10[Desactivar herramienta]
    D10 --> B

    D -- No --> E{DI_02 = 1?}

    E -- Sí --> E1[Activar modo mantenimiento (DO_02)]
    E1 --> E2[Ir a posición de mantenimiento]
    E2 --> E3[Esperar 1s]
    E3 --> E4[Volver a Home]
    E4 --> E5[Desactivar mantenimiento]
    E5 --> B

    E -- No --> B
```
