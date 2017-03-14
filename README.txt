Environment: ubuntu 16.04/14.04 with (default-jre package installed)

*** TO COMPILE:
	make

*** TO RUN:
1. Run the controller (server):
	make server
OR
    java ControlServer

2. Run the client (Applet):
	make client
OR
    appletviewer Client.java -J-Djava.security.policy=Client.policy

3. Simulation parameters in the Applet:
   (1) Simulation Speed: 
       This is the ratio of simulation clock's speed over the real 
       time clock speed. If this value is 0.1, then when real time 
       elapses 1 seconds, the simulation clock will elapse 0.1 second.

   (2) Simulation step size (in second):
       In this time-driven simulation, time is increased with fixed
       steps. This is the size of each step. It specifies how much 
       time in each step. 

   (3) Sensor Type
       Choose Time-Based sensor or Event-Based sensor.
       Time-based sensor will send the data to the controller each 
       time it does a measurement. Event-based sensor will only send 
       the data when the angle of the pole exceeds a threshold, which
       will be specified in (5).

   (4) Sensor sampling rate (per simulation second):
       How many samples the sensor will measure per simulation second.

   (5) Threshold for the event based sensor (in degrees):
       As explained in (3), this dialog input the threshold for the 
       event-based sensor.

4. Code:
   ControlServer.java:
       This is the main class for the controller. It contains the 
       PoleServer_handler class, which is a thread that continuously 
       reads the sensor data from socket and reply the controller 
       output to the actuators through socket. The control algorithm 
       is in this file.

   Client.java:
       This is the main class for the client. The client is the 
       simulation of inverted pendulum. It is a Java Applet. The 
       client consists of the following parts: 
           Pendulum.java: Pendulum object
           Physics.java:  A thread to simulate the states of the pendulums
	   Sensor.java:   A thread to simulate the sensors
           Actuator.java: A thread to simulate the actuators
           UpdatingUIThread.java: A thread to update graphical user interfaces
           
5. Configuration:
   To set the number of the pendulums and their initial position, change the
   the following lines accordingly:

	Server Side: (in ControlServer.java) 
		private static final int NUM_POLES = 2;

	Client Side: (in Physics.java)
		public final int NUM_POLES = 2;
       		public final double[] pole_init_pos = {-2.0, 2.0};
