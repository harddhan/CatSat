# catsat

a small terrestrial satellite prototype inspired by cubesats.

catsat is basically a satellite that never leaves earth. it sits on a rooftop, collects its own telemetry, communicates with a ground station and handles its own onboard systems.

the idea is to recreate the important parts of a small satellite without the whole "spend millions and throw it into space" problem.

## what it does

catsat is built around:

* onboard computing
* environmental sensing
* gps positioning
* imu based orientation tracking
* wireless telemetry
* solar assisted power
* battery monitoring
* onboard data logging
* ground station communication
* remote commands
* basic fault detection
* autonomous operation

## architecture

```text
                         catsat
                    ┌──────────────┐
                    │ solar panel  │
                    └──────┬───────┘
                           │
                    ┌──────▼───────┐
                    │ power system  │
                    │ + battery     │
                    └──────┬────────┘
                           │
              ┌────────────▼────────────┐
              │      onboard computer   │
              │                          │
              │          esp32           │
              └─────┬────┬────┬────────┘
                    │    │    │
                   imu  gps  sensors
                    │    │    │
                    └────┴────┘
                         │
                        lora
                         │
                    ~~~~~│~~~~~
                         │
                         ▼
                  ┌──────────────┐
                  │ ground       │
                  │ station      │
                  └──────┬───────┘
                         │
                         ▼
                    telemetry
                     dashboard
```

## telemetry

catsat continuously gathers information about its own state and its surroundings.

things like:

* temperature
* humidity
* pressure
* acceleration
* rotation
* gps position
* battery level
* solar power state
* system health

the data is transmitted to the ground station and stored for later analysis.

## communication

the satellite and ground station communicate wirelessly through lora.

the communication system isn't just meant for sending sensor values.

catsat can receive commands from the ground station, process them onboard and return an acknowledgement or result.

```text
ground station
      │
      │ command
      ▼
   catsat
      │
      │ process
      ▼
   response
      │
      ▼
ground station
```

## autonomy

catsat is intended to keep functioning without someone constantly controlling it.

the onboard system checks its sensors and internal state, collects data, stores telemetry and communicates with the ground station on its own.

if something goes wrong, the system can identify conditions such as:

* low battery
* missing gps
* invalid sensor readings
* communication failure
* abnormal temperature
* unexpected orientation

and report the fault through telemetry.

## ground station

the ground station is the other half of catsat.

it receives telemetry from the rooftop unit, decodes the packets, stores the data and presents the current state of the satellite.

it also provides the interface for sending commands back to catsat.

```text
             catsat
                │
             telemetry
                │
                ▼
        ┌─────────────────┐
        │ ground station  │
        ├─────────────────┤
        │ live telemetry  │
        │ sensor data     │
        │ gps             │
        │ battery         │
        │ system status   │
        │ fault status    │
        └────────┬────────┘
                 │
              commands
                 │
                 ▼
              catsat
```

## why catsat

the interesting part isn't putting an esp32 and a few sensors inside a box.

the actual project is the integration of multiple systems into something that behaves like a small autonomous spacecraft:

```text
power
  +
computing
  +
sensors
  +
communication
  +
telemetry
  +
data handling
  +
fault management
  =
catsat
```

catsat is a ground-based prototype, but the design is based around the same subsystem thinking used in small satellite systems.

## tech

* esp32
* lora
* gps
* imu
* environmental sensors
* solar power
* battery system
* embedded c/c++
* platformio
* python
* telemetry dashboard
* cad / 3d printed mechanical structure

## project

catsat is a student engineering project focused on embedded systems, iot, communication, power management and satellite systems.

not going to space.

yet.
