# Representing-how-a-robot-walks-using-a-Servo-Motor
![servo motor](https://github.com/user-attachments/assets/015cb0f8-cb51-47bc-b463-361e54c16355)

Creating an algorithm to represent a robot’s walking motion using servo motors involves several steps:
## step 1/ Define the Robot’s Gait
Gait Cycle: Determine the sequence of movements for the robot’s legs.
Common gaits include walking, trotting, and running.
Phases: Dividing the gait cycle into phases such as stance and swing.
## step 2/ Kinematics
Forward Kinematics: Calculate the position of the robot’s feet based on joint angles.
Inverse Kinematics: Determine the required joint angles to achieve a desired foot position.
## step 3/ Servo Motor Control
PWM Signals: Use Pulse Width Modulation (PWM) to control the position of the servo motors.
Timing: Synchronize the servo movements to match the gait cycle.
## step 4/ Balance and Stability
Center of Mass: Ensure the robot’s center of mass stays within its support polygon to prevent falling.
Feedback Control: Use sensors (like gyroscopes and accelerometers) to adjust the robot’s posture in real-time.
## step 5/ Algorithm Implementation using Python language
1. Define the Gait Cycle
```
gait_cycle = [
    {"leg1": 30, "knee1": -30, "leg2": 30, "knee2": -30},  # Phase 1
    {"leg1": 0, "knee1": 0, "leg2": 0, "knee2": 0},        # Phase 2
    {"leg1": -30, "knee1": 30, "leg2": -30, "knee2": 30},  # Phase 3
    {"leg1": 0, "knee1": 0, "leg2": 0, "knee2": 0}         # Phase 4
]
```
2. Function to Send PWM Signals to Servos
```
import pyfirmata
import time

# Setup the Arduino board
board = pyfirmata.Arduino('/dev/ttyUSB0')

# Define servo pins
servo_pins = {
    "leg1": 9,
    "knee1": 10,
    "leg2": 11,
    "knee2": 12
}
```
# Initialize servos
```
servos = {joint: board.get_pin(f'd:{pin}:s') for joint, pin in servo_pins.items()}
```
# Function to send PWM signals to servos
```
def move_servos(angles):
    for joint, angle in angles.items():
        servos[joint].write(angle)
```
# Main loop
```
while True:
    for phase in gait_cycle:
        move_servos(phase)
        time.sleep(0.5)  # Adjust timing as needed
```
The libraries used in the provided code are:
1. pyfirmata: This library is used to communicate with the Arduino board. It allows you to control the pins on the Arduino from Python.
2. time: This is a standard Python library used to handle timing and delays in the code.

Finally, this code sets up the basic walking motion of a bipedal robot using servo motors.
