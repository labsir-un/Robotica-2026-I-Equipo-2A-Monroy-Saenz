```cpp
MODULE Module1  
    PERS tooldata Marcador:=[TRUE,[[85.45,-1.13,118.934],[0.866025404,0,0.5,0]],[1,[0,0,1],[1,0,0,0],0,0,0]];
    TASK PERS wobjdata Pastel:=[FALSE,TRUE,"",[[0,0,0],[1,0,0,0]],[[193.076,-670.653,608.055],[0.0163836,0.000445408,0.999496,-0.0271948]]];
    !TASK PERS wobjdata Pastel:=[FALSE,TRUE,"",[[0,0,0],[1,0,0,0]],[[387.5,-582.5,530],[0,0,1,0]]];
    !PERS tooldata Marcador_real:=[TRUE,[[100.689,-0.535,124.792],[0.866025404,0,0.5,0]],[1,[0,0,1],[1,0,0,0],0,0,0]];!Real

    CONST robtarget C1_1:=[[62.708,129.951,-1],[1,0,0,0],[0,0,0,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget C1_1_prev:=[[62.708,129.951,-35],[1,0,0,0],[0,0,0,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget C1_2:=[[55.084,138.485,-1],[1,0,0,0],[0,0,0,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    // ... (recortas si quieres, porque esto es demasiado largo para un README)

    PROC main()
        WHILE TRUE DO 
            IF DI_03 = 1 THEN
                SET DO_03;
                SET BWD_Conveyor;
                waittime 4;
                RESET BWD_Conveyor;
                RESET DO_03;
            ENDIF
                
            IF DI_01 = 1 THEN
                SET FWD_Conveyor;
                waittime 4;
                Reset FWD_Conveyor; 
                WaitTime 5;
                SET DO_01; 
                Path_Home; 
                Path_A_1; 
                Path_L;
                Path_E;
                Path_JA;
                Path_A_2;
                Path_N_1;
                Path_D; 
                Path_R; 
                Path_A_3; 
                Path_S; 
                Path_J; 
                Path_U; 
                Path_A_4; 
                Path_N_2;
                Path_10;
                Path_Home; 
                SET FWD_Conveyor;
                waittime 4;
                Reset FWD_Conveyor; 
                RESET DO_01;
            ENDIF

            IF DI_02 = 1 THEN
                SET DO_02;
                Path_Mantenimiento;
                WaitTime 1; 
                Path_Home;
                RESET DO_02;
            ENDIF
        ENDWHILE
    ENDPROC

    PROC Path_Home()
        MoveJ Target_Home,v100,z100,Marcador\WObj:=wobj0;
    ENDPROC

ENDMODULE
```
