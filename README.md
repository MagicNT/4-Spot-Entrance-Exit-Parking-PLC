# PLC Project: 4-Spot Entrance/Exit Parking

## Objective
The purpose behind this project is to write a PLC program to handle a parking area with 4 available spots having an entrance path limited by 2 gates and an exit path bordered by 2 gates. The design job will be to control the 4 gates mechanism while ensuring a valid and secure parking system.

## Design Control Components

The design consists of 6 discrete inputs:

- I1: “car at gate A” which is the signal input obtained from a weight-metal detecting coil placed before gate A at entrance. [1]
- I2: “car at gate B” which represents the input obtained from a weight-metal detecting coil placed before gate B at entrance. [2]
- I3: “car at gate C” which represents the input obtained from a weight-metal detecting coil placed before gate C at exit. [3]
- I4: “car at gate D” which represents the input obtained from a weight-metal detecting coil placed before gate D at exit. [4]
- I5: “gate A SENSOR” which represents the input signal obtained from a sensor placed under gate A at entrance and it detects the presence of an object or human under gate. [5]
- I6: “gate C SENSOR” which represents the input obtained from a sensor placed under gate C at exit and it detects the presence of an object or human under gate. [6]

When each of these switches are pressed they signal a car being on top (in case of a coil input) or a car being under (in case of a sensor input).

The design consists of 2 Zx-keys input:

- Z1: “enter BUTTON” which represents the input signal from a button placed next to gate A at entrance, when pressed to state that a driver wishes to get in to the parking. [7]
- Z1: “exit BUTTON” which represents the input signal from a button placed next to gate C at exit, when pressed to state that a driver wishes to exit from the parking. [8]

The design consists of 6 discrete outputs:
- Q1: “open gate A” which controls the opening and closing of gate A [9]
- Q2: “open gate B” which controls the opening and closing of gate B [10]
- Q3: “open gate C” which controls the opening and closing of gate C [11]
- Q4: “open gate D” which controls the opening and closing of gate D [12]
- Q5: “GREEN” which signals to the cars outside the parking that there are still free spots to park inside [13]
- Q6: “RED” which signals to the cars outside the parking that the parking is full and therefore no car can enter [14]

Each of these outputs when activated is visualized by a turned ON light lamp on the ZelioSoft2 simulation panel.

Other technical components: 
- C1: which is a counter used to keep hold of the number of free parking lots.
- T1, T2, T3, T4: Each gate has got its own 7 seconds timer.
- M1, M2: Two auxiliary relays used to save the status for enter and exit buttons.
- M3, M4: Two auxiliary relays used in order to keep gates A and C open when a car is detected by sensors.
- M5, M6, M7: Three auxiliary relays used to keep status if car has exited, car inside entrance path and if car is inside exit path respectively.

![parking](https://user-images.githubusercontent.com/86275885/122982181-ecf1ce80-d370-11eb-8d83-fda7bf442042.png)

[15] On the figure represents the 4 available parking spots that can be occupied by cars.

## Design Details

- The goal is to control access to this parking by orchestrating the opening and closing of all 4 gates where the gates on the entrance and on the exit should be able to work efficiently in parallel if a car is entering and another is exiting at the same time. 
- The design uses separate paths for entrance and exit.
- Detection of entering and exiting cars is done by means of metal and weight detection coils that do not detect/accept people. They work by creating a magnetic electrical field when a car (heavy metal) is upon them.
- Detection of objects, cars and humans under gate A and C is made by means of 2 sensors at each of these gates.
- The project used a time delay of 7 seconds to close each gate giving an enough time period to allow a valid car to pass securely inside the paths and also prevent a car from sneaking in illegally. 
- In case a car is under a gate A or gate C before it closes, a sensor will detect it and will not allow these gates to close until the car is out of sensor reach. This will preserve security and safety of cars.
- Once gate A or C close and there are cars inside each path, the other gates will open automatically to allow cars to either exit or enter the parking.
- The project also implements 2 output light bulbs: one green and one red where the green signals an availability of space for cars to still come in while the other signals unavailability due to the 4 spots already being occupied.
- The design has been programed and tested against various logical scenarios in order to ensure stability and security.


## Design Mechanism Description

- Entrance: When a car is detected outside gate A by 1st coil and the enter button is pressed, if there are spaces free inside the parking, gate A opens and then closes after 7 seconds if no car (and object or human) is under the gate and if a car is now inside path else it remains open until the car moves away. Once car inside entrance path is detected by 2nd coil and gate A closed for sure, gate B opens for 7 seconds and allows car to go inside and then increments the count of cars within the parking. 

- Exit: When a car is detected before gate C by 3rd coil and the exit button is pressed, gate C opens and then closes after 7 seconds if no car (object or human)  is under the gate and if a car is inside path else it remains open until the car moves away. Once car inside exit path is detected by 4th coil and gate C closed for sure, gate D opens for 7 seconds and allows car to go outside the parking and then decrements the count of cars within the parking. 


## Conclusion
This project mainly focused on teaching us the concepts, usage and technicality behind several new components such as timers, counters and auxiliary relays. I had to learn to use these elements by reading the help offered byZelioSoft2 as well as learn the different utilities they can provide in order to efficiently employ them for this program design. 







