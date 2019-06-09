[1]: https://github.com/ysyesilyurt/RTOS/blob/master/simulator.png

# RTOS
An RTOS project written with C for PIC18F8722 based architecture with PicOS18 which aims to practice necessities of Real-Time tasks.

## Project
This implementation's goal is to guide a robot which tries explore all the unknown parts of its maze and find its way through the exit within 2 minutes in a simulated environment.

Codes are developed on MPLAB X IDE with `C18 v3.40` compiler. `PicOS18` has been used as the RTOS kernel. Implementation was a part of my Undergraduate Embedded Systems Course in METU.

## How to Run?
If you have a PIC18F8722 based board and MPLAB X IDE installed (with `C18` compiler) on your computer, you can create a project in IDE with adding `PicOS18` kernels, libraries, linkers and inserting all the project files in here to there. Then you should be able to compile, load and run it on your board. Afterwards you need to run `simulator/cengrobosim2d/cengrobosim2d_v3.6.py`, as soon as you press 'g' from your keyboard the simulation will begin.

## Internal Details
The simulated robot has an encoder and 4 sensors on its 4 directions. It tries to move in the map using these sensors and encoder. Initially it has no information about the map, then gradually it explores the map as it moves along it. It always starts on top left corner of the map and it does not stop until all the map is explored and robot reaches to the top right corner (exit point in the map) of the map. Below is a screenshot from the simulator with ongoing exploring process with PIC ('Arena' corresponds to real map and 'Current Map' corresponds to explored piece of map),

![alt text][1]

The simulation is being carried out with a simulator (`simulator/cengrobosim2d/cengrobosim2d_v3.6.py`). After the board is loaded with the project and serial communication cable is set, `PIC` and simulator starts to communicate asynchronus with serial communication using `EUSART1` module in PIC. 

Simulator shows robot, actual map, explored map, remaining time and some other information about robot such as its x,y coordinates. PIC also shows the explored map from its LCD with 2 lines at a time (to see the other part of the explored piece of the map `RB4` button is used).

To achieve all these requirements, 3 `tasks` (threads) have been used with several `alarms` and `events`.

### Authors
* Yavuz Selim Yesilyurt
* Alper Kocaman
