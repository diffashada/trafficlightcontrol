# 🚦 Traffic Light Simulator using CODESYS (PLC + HMI)

This project simulates a **two-direction traffic light system** (North-South and East-West) using **Structured Text (ST)** in **CODESYS**. The simulation includes PLC logic and an interactive HMI panel to visualize the states of traffic lights.

## 📌 Features

- 4-phase traffic light sequence:
  1. North Green, East Red
  2. North Yellow, East Red
  3. North Red, East Green
  4. North Red, East Yellow
- Timer-based light transitions (20 seconds total cycle)
- Visualization (HMI) for real-time light indicators
- Easily extendable logic for more intersections

## 🛠️ Technologies Used

- **CODESYS V3.5**
- **Structured Text (ST)**
- **HMI Visualization Tool (WebVisu)**

## 🧠 Logic Flow

```pascal
Timer_1(IN := StartBit, PT:= T#20S);
Timer_1_Finished := Timer_1.Q;

IF Timer_1.Q THEN StartBit:= 0;
    ELSE StartBit := 1;
END_IF

IF Ladder_Logic.Timer_1_AccValue >0 AND Ladder_Logic.Timer_1_AccValue <5000 THEN
    NorthGreen_LT := 1;
    NorthYellow_LT := 0;
    NorthRed := 0;
    EastGreen_LT := 0;
    EastYellow := 0;
    EastRed := 1;
END_IF

IF Ladder_Logic.Timer_1_AccValue >5000 AND Ladder_Logic.Timer_1_AccValue <10000 THEN
    NorthGreen_LT := 0;
    NorthYellow_LT := 1;
    NorthRed := 0;
    EastGreen_LT := 0;
    EastYellow := 0;
    EastRed := 1;    
END_IF

IF Ladder_Logic.Timer_1_AccValue >10000 AND Ladder_Logic.Timer_1_AccValue <15000 THEN
    NorthGreen_LT := 0;
    NorthYellow_LT:= 0;
    NorthRed := 1;
    EastGreen_LT := 1;
    EastYellow := 0;
    EastRed := 0;
END_IF

IF Ladder_Logic.Timer_1_AccValue >15000 AND Ladder_Logic.Timer_1_AccValue <20000 THEN
    NorthGreen_LT := 0;
    NorthYellow_LT:= 0;
    NorthRed := 1;
    EastGreen_LT := 0;
    EastYellow := 1;
    EastRed := 0;
END_IF
