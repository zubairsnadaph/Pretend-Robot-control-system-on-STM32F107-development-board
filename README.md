# Pretend-Robot-control-system-on-STM32F107-development-board
Running on STM32F107 development board with uC/OS-III RTOS 
The objective of this project is to implement a robot control system. There are upto 13 robots that may move around on the factory floor. In this project Robot Manager is designed which takes command from control center which then decodes, recreate packets with appropriate robot address and instruction and sends back to control center where the robots are also designed and implemented. 

The control center, bots and robot manager communicate each other over RS-232 and hence use custom designed interrupt based UART driver. The communication can be improved to RF links (e.g. WiFi) which is not demonstrated here. Each component on the network (robots, manager, control center) has a unique 8-bit address (0-255). Address zero means forward to both control center and robot manager, address 1: control center, address 2: robot manager and addresses 3-15 dedicated to 13 robots. The floor for robot is a rectangular grid and each cell in the grid may be occupied by only one robot at a time. Robot locations are given in Cartesian coordinates, a sample of which is attached to the repository. Robots have limited capabilities, i.e a robot can only move one step at a time to an adjacent cell. There are 8 surrounding directions in which robot may step and when asked to move if a cell in the direction is occupied by another robot, then it will avoid that direction and chose another adjacent direction thus avoiding collision.

The algorithm for this project is based on preemptive multithreading (see flow chart for additional details) and communication between threads using queue and mailbox. The algorithm can spawn upto 16 threads if required.

All the source codes for robot manager are in app folder under nadaph.zip
