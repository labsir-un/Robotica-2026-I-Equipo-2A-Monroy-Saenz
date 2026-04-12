flowchart TB
    C{"DI_03==1?"} -- Si --> D["DO_03=1"]
    C -- No --> F["DI_01=1?"]
    n1["Creación de los targets"] --> C
    n2["Creación del objeto de trabajo y la herramienta"] --> n1
    D --> n3["BWD_Conveyor=1"]
    n3 --> n4["Esperar 4 segundos"]
    n4 --> n5["DO_03=0"]
    n5 --> n6["BWD_Conveyor=0"]
    F --> n8["FWD_Conveyor=1"] & n9["Untitled Node"]
    n8 --> n10["Esperar 4 segundos"]
    n10 --> n11["FWD_Conveyor=1"]
    n11 --> n12["Esperar 5 segundos"]
    n12 --> n13["DO_01=1"]
    n13 --> n14["Ir a home"]
    n14 --> n15["Trazar los nombres"]
    n15 --> n16["Trazar la figura"]
    n16 --> n17["Ir a home"]
    n17 --> n18["FWD_Converyor=0"]
    n18 --> n19["Esperar 4 segundos"]

    F@{ shape: diam}
    n1@{ shape: rect}
    n2@{ shape: rect}
