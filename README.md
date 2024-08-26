# SwarmDrones
Swarm drones involve multiple drones working together as a coordinated group to achieve a common goal. This concept is inspired by natural swarms, such as those seen in birds or insects, where each individual unit operates with simple rules, but collectively, they perform complex tasks. In a drone swarm, each drone communicates with others and follows specific algorithms to maintain formation, avoid collisions, and execute tasks collaboratively. This enables the swarm to cover large areas, perform simultaneous tasks, or provide redundancy, making the system more resilient.

The applications of swarm drones are vast and include search and rescue missions, agricultural monitoring, environmental surveys, and military operations. In these scenarios, swarms can be more efficient and effective than a single drone, as they can operate autonomously in dynamic environments, adapt to changing conditions, and work together to achieve objectives that would be challenging for a single unit. The development of swarm intelligence and communication protocols is key to advancing this technology, enabling drones to perform complex missions with minimal human intervention.


## Hardware Requirements
- Pixhawk based drone with GPS Module (you can use F450 Frame)
- Node MCU wifi module
- Transmitter and receiver
- Laptop
- Router(Optional)

## Software Requirements
- QGroundControl - It is a GCS 

## Setup 
For wifi telemetry you can follow the [setup](https://ardupilot.org/copter/docs/common-esp8266-telemetry.html)

### Connecting Multiple drones to one Ground Control Station

 1. **Configure Telemetry Modules (MAVLink WiFi Bridges)**
   - **Station Mode Setup**: 
     - Access the telemetry module's web interface (usually by connecting to its access point and navigating to `192.168.4.1` in a browser).
     - Set the module to **Station Mode** and connect it to your WiFi network (your home router or a mobile hotspot).
     - Assign a unique **Client Port** to each drone:
       - Drone 1: Set Client Port to **14555**.
       - Drone 2: Set Client Port to **14556**.
     - Set the **Host Port** to **14550** for both drones. This is the port that QGC will listen to for incoming telemetry data.

 2. **Set System IDs on Drones**
   - Connect to each drone via Mission Planner or any other GCS.
   - Set a unique **MAVLink System ID** for each drone:
     - Drone 1: System ID = 1.
     - Drone 2: System ID = 2.
   - This helps QGC differentiate between the drones.

 3. **Set Up QGroundControl (QGC)**
   - **Open QGC** and go to **Settings** > **Comm Links**.
   - Ensure QGC is configured to listen on **UDP port 14550**:
     - If not, create a new UDP link:
       - Name: **UDP Telemetry**.
       - Type: **UDP**.
       - Listening Port: **14550**.
       - Leave the Target Host/IP empty.
     - Click **Connect** to activate the link.

 4. **Verify Connections**
   - Ensure both drones are powered on and connected to your WiFi network.
   - QGC should automatically detect the telemetry streams from both drones, identified by their unique System IDs.

 5. **Monitor and Control Drones**
   - In QGC, you should see both drones appearing in the interface, each represented separately.
   - You can switch between drones in QGC to monitor and control each one.

 6. **Final Checks**
   - Ensure no firewall or security software is blocking UDP port 14550 on your computer.
   - Test the telemetry by moving the drones and checking if QGC receives and displays the data correctly.

This setup will allow you to control and monitor multiple drones simultaneously via QGroundControl using WiFi.
