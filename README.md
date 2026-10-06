# Automated NERF Turret

An Arduino Nano-based NERF turret with an automated trigger that fires a dart roughly every 2 seconds. A hydraulic scissor mechanism, pushed by hand with syringes, raises and lowers the cannon to the desired height.

It's a simple, low-cost build made from ice cream sticks, but the structure can also be 3D printed if you prefer. A single servo pulls the trigger, and the whole thing runs from a power bank.

> This was my first project, so it's simple and a bit rough, and it's kept here for reference.

## Demo


https://github.com/user-attachments/assets/0e67062d-1ad3-44e2-92f6-20011747f1ae

<img width="768" height="1024" alt="pic 2" src="https://github.com/user-attachments/assets/7ac189c3-a0a0-4d88-a351-793ba998038c" />
<img width="768" height="1024" alt="pic 1" src="https://github.com/user-attachments/assets/cb9dc645-79e5-49bc-8290-3627a2c72111" />

<!-- Drag your demo video or photos here -->

## Features

- **Automated trigger:** a servo pulls the trigger on its own, about every 2.4 seconds
- **Hydraulic scissor lift:** a syringe-based hydraulic system raises and lowers the cannon, pushed by hand
- **Low-cost build:** made from ice cream sticks, with an optional 3D-printed version
- **Minimal electronics:** one Arduino Nano and one servo
- **Portable power:** runs from a standard power bank

## How It Works

| Part | How it's controlled |
|---|---|
| Trigger | Automated: the Arduino drives a servo that pulls the trigger |
| Cannon height | Manual: syringes connected by tubing form a hydraulic system, and you push the syringe by hand to extend the scissor mechanism |

The firing cycle repeats continuously:

1. The servo rests at 60 degrees for 2 seconds while the turret waits.
2. The servo swings to 180 degrees and holds for 0.4 seconds, pulling the trigger.
3. The loop repeats, giving one shot roughly every 2.4 seconds.

The scissor lift is hydraulic: two syringes joined by fluid-filled tubing transfer motion from the syringe you push to the one that extends the scissor mechanism. It needs no gears or lead screws.

## Components

- Arduino Nano
- 1 servo motor (trigger)
- Syringes and flexible tubing (hydraulic system, fluid-filled)
- NERF cannon and darts
- Ice cream sticks for the frame and scissor mechanism (or 3D-printed parts)
- Power bank (USB, 5 V)
- Jumper wires, glue, and fasteners

## Wiring

| Servo wire | Arduino Nano pin |
|---|---|
| Signal (orange/yellow) | D7 |
| Power (red) | 5V |
| Ground (brown/black) | GND |

The Arduino Nano is powered from the power bank over USB.

## Code

```cpp
#include <Servo.h>
Servo s;

void setup() {
  s.attach(7);
}

void loop() {
  s.write(60);    // rest position, waits before the next shot
  delay(2000);
  s.write(180);   // pulls the trigger
  delay(400);
}
```

Adjust the `60` and `180` angles to match how your servo is mounted on the trigger, and change the `2000` delay to change the time between shots.

## Build Notes

1. Build the base and frame from ice cream sticks (or print the parts).
2. Assemble the scissor mechanism so it can raise and lower the cannon.
3. Fill the syringes and tubing with fluid and remove air bubbles. Air in the line makes the lift spongy.
4. Attach the output syringe to the scissor mechanism, and push the other syringe by hand to raise the cannon.
5. Mount the cannon and attach the servo so it pulls the trigger when it swings to 180 degrees.
6. Wire the servo to the Arduino Nano and plug in the power bank.

## Getting Started

1. Install the [Arduino IDE](https://www.arduino.cc/en/software).
2. Open the sketch above in the IDE.
3. Select **Arduino Nano** as the board and choose the correct port.
4. Upload the sketch, then power the turret from the power bank.

## Future Improvements

- Automate the lift by driving the syringe with a second servo
- Add a sensor (ultrasonic or camera) to aim at targets
- Add a manual or remote control mode
- Build a sturdier 3D-printed version

