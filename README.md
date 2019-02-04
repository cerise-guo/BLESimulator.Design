# BLE Simulator

This BLE emulator is a library which simulates mobile OS Bluetooth Low Energy behavior by mocking mobile OS BLE interface.

# Goal of Project

The goal of this project is to fully simulate mobile OS BLE interaction in application layer with minimum application code change.

# Challenge During Mobile BLE Development
 * Hard to run automatic test with synchronized BLE peripheral hardware
 * Hard to trigger end cases and timing condition
 * Mocked code presents unfaithful logic
 * Hard to test background/idle mode
 * Can not Step by Step debugging
 * software development has to wait till firmware & hardware is developed

# BLE Simulator High Level Design
![N|Solid](high-level-design.png)

All simulator code is behind the simulated Mobile BLE interface. Caller, namely mobile application, will only see same BLE interface as native BLE.

# Benefit of Software BLE Simulator
* Since the simulated BLE peripheral code/logic runs inside same process as application, very easy to control and synchronize the peripheral behavior, which facilitates the automatic test.

* When the simulated peripheral logic runs together as part of application, no wireless communication and mobile OS interaction, it allows to simulate different error & end cases. It is also able to simulate timing conditions easily, e.g. when reading is returned. It definitely allows step by step debugging without connection timeout.

* By simulating exact mobile OS BLE interface, mobile application needs very limited code change to switch between real BLE and this simulated BLE library.

* BLE simulator is able to simulate background BLE behavior. This is a big benefit for testing since background BLE behavior highly relies on mobile OS scheduling, hard to predict.

* The code of BLE simualtor is neutral and independent from particular project, it can be used by other projects. 


# BLE Simulator Middle Level Design
![N|Solid](middle-level-design.png)

Behind the simulated Mobile native BLE interface, two services are responsible for BLE request before and after the connection establishment.

To keep simulated mobile BLE interface efficient, the interface layer just puts BLE request in a queue and returns immediately. The two services run asynchronously from the BLE interface and pull BLE request from queue to process.

The gray blocks in the diagram show where project particular peripheral logic inhabits. A user of the BLE simulator library should only change/add logic in these gray area.

Since the BLE callback function by caller is unknown for BLE simulator, the code in two gray blocks runs asynchronously from the callback function with exception catcher which guards the issues thrown from user's BLE callback.

# BLE Simulator Low Level Design
![N|Solid](low-level-design.png)
This diagram shows some of low level design.

Here are some low level design consideration. Will update periodically:

 - Use containers for peripheral, service, characteristic and description object.
 - Avoid keeping strong reference besides the container. 
 - Background mode suspends peripheral callback until condition is satisfied.
 - Pass UUID internally instead of object e.g. characteristic object.
 - Package internal sub-class has more capability


 