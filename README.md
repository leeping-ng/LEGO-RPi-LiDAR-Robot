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

## Battery Selection

- I chose a 3 cell (3S) LiPo battery because it provides a voltage of 11.1V which is close to the 12V required by the DC motors.
- The step-down converter can step down the voltage to 5V for the rest of the circuit.
- Assuming we want the robot to run for 30 mins:
    ```
    Battery capacity = 3.8A*1000*30/60 = 1900mAh
    ```
- This [2200mAh battery](https://www.overlander.co.uk/catalog/product/view/id/1771/s/2200mah-3s-11-1v-25c-lipo-battery-xt60-overlander-sport/category/442/) has a constant discharge of 25C:
    ```
    Constant drawable current = 25C*2200mAh = 55A > 3.8A
    ```

## TO-DO

- Choose a fuse
- Choose connector type for the battery
- Look into wiring

