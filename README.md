# Smart Home Panel
Qt 6 Application for Device Control using MQTT and WebSockets

## Project Description

### Overview
Smart Home Panel is a Qt 6 application designed for monitoring and controlling smart home devices in real time. The system provides a centralized dashboard where users can observe device states, send commands, and receive live updates.

The application uses a QML-based frontend for the user interface and a C++ backend for business logic and networking. Communication with devices is implemented using MQTT for command delivery and WebSockets for real-time updates.

---

### Objectives
- Build a functional Qt 6 application with QML and C++
- Implement real-time communication with external systems
- Demonstrate usage of MQTT and WebSockets together
- Design a clean and responsive user interface
- Simulate or integrate smart home devices

---

### Target Platform
- Desktop (Linux / Windows)
- Extendable to Android or embedded Linux

---

### Key Features
- Real-time device monitoring
- Device control (on/off, sliders, parameters)
- MQTT publish/subscribe communication
- WebSocket live updates
- Multi-screen UI
- Device status synchronization
- Connection monitoring and error handling

---

## UI Design

### Main Screens

#### Dashboard
Displays all available devices and their current states.

### --------------------------------------------------
| Smart Home Panel                                  |
|---------------------------------------------------|
| MQTT: Connected                                   | WS: Connected                  |
| -------------------------------------------------- |
| [Light - Living Room]   ON      [Toggle]          |
| Brightness: [======---] 70%                       |
|                                                   |
| [Thermostat]          22°C   [Details]            |
| Target: 24°C                                      |
|                                                   |
| [Door Sensor]         Closed                      |
|                                                   |
| [Smart Plug]          OFF     [Toggle]            |
| -------------------------------------------------- |
| [Dashboard] [Logs] [Settings]                     |
### --------------------------------------------------

#### Device Details
Detailed control view for a selected device.

### --------------------------------------------------
| Device Details                                   |
|--------------------------------------------------|
| Name: Living Room Light                          |
| Type: Light                                      |
| Status: ON                                       |
|                                                  |
| Power:        [ ON / OFF ]                       |
| Brightness:   [ slider 0-100 ]                   |
|                                                  |
| MQTT Topic: home/livingroom/light/set            |
|                                                  |
| [Back]                                           |
### --------------------------------------------------

#### Logs Screen
Displays system activity and messages.

### --------------------------------------------------
| Event Log                                        |
|--------------------------------------------------|
| 12:40 Connected to MQTT                          |
| 12:41 WebSocket connected                        |
| 12:42 Light turned ON                            |
| 12:43 Temperature updated: 22°C                  |
|--------------------------------------------------|
| [Clear]                                          |
+--------------------------------------------------+

#### Settings
Configuration of network connections.

### --------------------------------------------------
| Settings                                         |
|--------------------------------------------------|
| MQTT Broker:   mqtt://localhost:1883             |
| Username:      [________]                        |
| Password:      [________]                        |
|                                                  |
| WebSocket URL: ws://localhost:9001               |
|                                                  |
| Auto-connect: [x]                                |
|                                                  |
| [Save] [Reconnect]                               |
### --------------------------------------------------

---

### Navigation Flow
- Application starts on Dashboard
- Selecting a device opens Device Details
- Navigation allows switching to Logs and Settings
- Back button returns to Dashboard

---

## Architecture Overview

### High-Level Architecture

QML UI (Frontend)
↓
C++ Backend
↓
MQTT Broker + WebSocket Server
↓
Smart Devices or Simulator

---

### Components

#### QML Frontend
- Displays UI elements
- Handles user interaction
- Binds to backend data models
- Updates automatically when data changes

#### C++ Backend
- Contains core application logic
- Manages device models
- Handles MQTT communication
- Handles WebSocket communication
- Parses incoming messages
- Sends commands to devices

#### Device Manager
- Stores device list
- Updates device states
- Provides data to QML

#### MQTT Client
- Connects to broker
- Publishes control commands
- Subscribes to topics if needed

#### WebSocket Client
- Connects to server
- Receives real-time updates
- Pushes updates to backend

---

## Communication Design

### MQTT (Command Channel)
Used to send commands to devices.

Example:
Topic: home/livingroom/light/set  
Payload:
{
"state": "ON",
"brightness": 70
}

---

### WebSockets (Update Channel)
Used for real-time updates from devices.

Example message:
{
"device": "livingroom_light",
"state": "ON",
"brightness": 70
}

---

## Data Flow

### User to Device
1. User interacts with UI (button, slider)
2. QML sends signal to C++ backend
3. Backend formats MQTT message
4. Message is published to broker
5. Device receives and applies command

### Device to UI
1. Device sends update via WebSocket
2. Backend receives message
3. Data is parsed and stored
4. Device model updates
5. UI reflects changes automatically

---

## Project Structure

### smart-home-panel/
### ├── src/
### │   ├── main.cpp
### │   ├── backend/
### │   │   ├── DeviceManager.cpp
### │   │   ├── DeviceManager.h
### │   │   ├── MqttClient.cpp
### │   │   ├── MqttClient.h
### │   │   ├── WebSocketClient.cpp
### │   │   ├── WebSocketClient.h
### │   └── qml/
### │       ├── Main.qml
### │       ├── Dashboard.qml
### │       ├── DeviceDetails.qml
### │       ├── Logs.qml
### │       ├── Settings.qml
### ├── resources/
### ├── README.md
### └── CMakeLists.txt

---

## Build and Run

### Requirements
- Qt 6
- C++17 compiler
- CMake
- MQTT broker (e.g., Mosquitto)
- WebSocket server or simulator

### Build
mkdir build
cd build
cmake ..
make

### Run
./SmartHomePanel

---

## Testing Approach
- Simulated devices using MQTT topics
- Mock WebSocket server for updates
- Manual UI interaction testing
- Logging for debugging communication

---

## Future Improvements
- User authentication
- Device grouping by rooms
- Persistent storage (database)
- Graphs for sensor data
- Mobile optimization
- Integration with real IoT hardware

---

## Conclusion
This project demonstrates a complete Qt-based application combining a QML frontend with a C++ backend and real-time communication using MQTT and WebSockets. It reflects a realistic smart home control system and provides a foundation for further development.