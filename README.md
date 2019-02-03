#BLE Simulator

This BLE emulator is a library which simulates mobile OS Bluetooth Low Energy behavior by mocking mobile OS BLE interface.

#Goal of Project

The goal of this project is to fully simulate mobile OS BLE interaction in application layer with minimum application code change.

#Challenge During Mobile BLE development
* Hard to run automatic test with synchronized BLE peripheral hardware
* Hard to trigger end cases and timing condition
* Mocked code presents unfaithful logic
* Hard to test background/idle mode
* Can not Step by Step debugging
* software development has to wait till firmware & hardware is developed

#BLE Simulator High Level Design
![BLE Simulator High Level Design](high-level-design.jpg)


