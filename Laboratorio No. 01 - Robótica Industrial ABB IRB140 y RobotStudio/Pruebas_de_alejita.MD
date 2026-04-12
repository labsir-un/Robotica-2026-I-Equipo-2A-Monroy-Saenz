```mermaid
---
config:
  layout: dagre
---
flowchart TB
    C{"DI_03==1?"} -- Si --> D["DO_03=1"]
    C -- No --> F["DI_01==1?"]
    n1["Creación de los targets"] --> C
    n2["Creación del objeto de trabajo y la herramienta"] --> n1
    D --> n3["BWD_Conveyor=1"]
    n3 --> n4["Esperar 4 segundos"]
    n4 --> n5["DO_03=0"]
    n5 --> n6["BWD_Conveyor=0"]
    F -- Si --> n8["FWD_Conveyor=1"]
    F --> n9["DI_02==1?"]
    n8 --> n10["Esperar 4 segundos"]
    n10 --> n11["FWD_Conveyor=1"]
    n11 --> n12["Esperar 5 segundos"]
    n12 --> n13["DO_01=1"]
    n13 --> n14["Ir a home"]
    n14 --> n15["Trazar los nombres"]
    n15 --> n16["Trazar la figura"]
    n16 --> n17["Ir a home"]
    n17 --> n18["FWD_Converyor=1"]
    n18 --> n19["Esperar 4 segundos"]
    n19 --> n20["FWD_Conveyor=0"]
    n20 --> n21["DO_01=0"]
    n6 --> F
    n9 -- Si --> n22["DO_02=1"]
    n22 --> n23["Ir a posición de mantenimiento"]
    n23 --> n24["Esperar un segundo"]
    n24 --> n25["Ir a home"]
    n25 --> n26["DO_02=0"]
    n21 --> n27["Untitled Node"]
    n27 --> n9
    n26 --> C
    n9 --> C

    F@{ shape: diam}
    n1@{ shape: rect}
    n2@{ shape: rect}
    n9@{ shape: diam}
