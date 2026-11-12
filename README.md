# Smart Water Tank Monitoring and Control System

A digital logic system designed in Logisim Evolution for monitoring water level, controlling a pump, displaying the detected level, and signaling when the tank has remained full for three clock cycles.

## Circuit file

[Download the Logisim circuit](https://raw.githubusercontent.com/ridwan-ha/IFT-211-Water-Tank-System/main/IFT%20211%20Smart%20Water%20Tank%20Monitoring%20%26%20Control%20System.circ)
## Requirements

- Logisim Evolution
- The circuit uses digital logic components and a clock input.

## Sensor encoding

The design assumes the level sensors use a one-hot encoding: exactly one sensor should be on for a valid reading.

| Sensor | Tank level | Encoded level |
|---|---:|:---:|
| S0 | Empty | 00 |
| S1 | 25% | 01 |
| S2 | 50% | 10 |
| S3 | Full | 11 |

## System behavior

- `VALID` is on when exactly one sensor is active.
- The level register updates on the rising edge of `CLOCK` when the sensor input is valid.
- For invalid sensor inputs (no sensors or multiple sensors active), `VALID` and `PUMP` turn off, and the register holds its previous level.
- `PUMP` is on for a valid reading unless the tank is full.
- `FULL` is on when the full-level sensor reading is valid.
- The display shows the encoded level from 0 to 3.
- `ALARM` turns on after the tank remains full for three rising clock edges. It clears when the full condition is removed at a clock edge or when reset is applied.
- `RESET` is synchronous and takes effect on a rising clock edge.

## Running the circuit

1. Open the `.circ` file in Logisim Evolution.
2. Use the Poke tool to set the sensor inputs.
3. Set sensor inputs while `CLOCK` is low.
4. Toggle `CLOCK` from low to high to apply a reading. Toggle it back to low before the next rising edge.
5. Observe `VALID`, `LEVEL1`, `LEVEL0`, `FULL`, `PUMP`, the stored level, display, and `ALARM`.

## Tests

The circuit was tested for each individual sensor, invalid inputs (no sensors or multiple sensors active), and the three-cycle full-tank alarm behavior. The tests passed.

## Notes

This repository contains the Logisim circuit for inspection and download. To simulate or modify the system, download the `.circ` file and open it in Logisim Evolution.
