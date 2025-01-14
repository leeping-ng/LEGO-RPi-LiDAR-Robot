# Raspberry Pi Robot with LEGO Chassis and 2D LiDAR (WIP)

## Current Draw

| Component      | Operating Voltage | Max Current  |
|----------------|-------------------|--------------|
| Raspberry Pi 5 | 5V                | 5A           |
| 2D LiDAR       | 5V                | 0.3A         |
| Arduino Nano   | 5V                | 0.1A (est)   |
| DC Motors      | 12V               | 0.7A (stall) |

Assumptions made:
- Rated current for DC motors was not given in the [datasheet](https://thepihut.com/products/brushless-dc-motor-with-encoder-12v-159rpm?variant=27740916241), so we will conservatively use the stall current instead.
- It's unlikely that the RPi 5 will be maxing out at 5A, so we are being conservative here as well.
- We ignore all power losses in the wiring, step-down converter etc. We should have some buffer from the above assumptions... hopefully.


## Electrical Schematic

- This isn't a proper circuit diagram, but it helps to understand how the components are wired together and the currents in each wire. 
- Calculations for current:
    ```
    Current into RPi = 5A + 0.3A + 0.1A = 5.4A
    Current into Step-Down Converter = 5V*5.4A/11.1V = 2.4A
    Current out of Battery = 2.4A + 0.7A*2 = 3.8A
    ```

![diagram](schematic.drawio.svg)