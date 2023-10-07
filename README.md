# rover-Testbed

Repo for rover testbed operations. This repo contains both components, basestation and rover in their respective folders.<br>


## Software Pre-reqs

The Nuc on the testbed is good to go!<br>
The BaseStation computer will need several things.
 - ROS2 Humble
	 - Follow the standard ROS2 humble install process. Linux recommended. 
	 - https://docs.ros.org/en/humble/Installation.html
 - Colcon
	 - `$ sudo apt update`
	 - `$ sudo apt install python3-colcon-common-extensions`
 - Configured Static IP for Ubiquiti bullet 
	 - This process will depend on the system, but you'll need this for using the Ubiquiti network with the M2 bullets.
	 - Settings:
		 - Net Mask: 255.255.255.0
		 - IP Address: 192.168.1.x
			 - This can be just about anything, just not ending in 1.20, 1.21, 1.69, or 1.0
		 - Gateway: 192.168.1.0
 - Clone this github repo on the BaseStation computer
	 - Navigate (cd) into the rover_bs_ws folder and perform `colcon build`
		 - You'll only need to do this the first time, and whenever you pull new code
	 - Optional (linux): Source the setup script in your `~/.bashrc` script
		 - edit your `~/.bashrc` script
		 - at the bottom add `source ~/.../rover_bs_ws/install/setup.bash`
			 - Enter the path which points to the setup.bash file in the rover_bs_ws' install folder from the repo



## Hardware Pre-reqs

 - Plug in Rover stuff
	 - Connect the battery. Ensure it's charged and use the smaller size batteries, not the largest one. They should be ~14-16v. Ensure the battery is at least 50% charged to get nominal voltage.
 - Connect BaseStation to other bullet through POE injector
	 - BaseStation is connected to the LAN port on the injector
	 - bullet is connected to the POE port on the injector
	 - Bottom light signals power
	 - Second light signals data transmission
	 - Other lights will light up (red/orange/etc..) once a connection is made to another AP on the network

## Running the BaseStation node

 - Source the setup.bash if you've not added it to your ~/.bashrc script
	 - Naviate (cd) to your rover_bs_ws folder and run
		 - `source install/setup.bash`
	 - You'll need to do this each time you open a new terminal
 - Connect your controller (wired preferred)
	 -Follow GuliKit connection instructions below if using the GuliKit KingKong Pro 2 controller
 - Run `Ros2 run testbed_bs_pkg testbed_bs`
	 - The program will print out controller values being received
	 - Default values will likely be ~0.0032, this is okay

## Running the Rover node

 - Ensure you're either connected directly to the Nuc/Testbed switch over ethernet or connected to an M2 bullet which has connection to the rover (red signal lights on)
 - SSH to the testbed from the BaseStation computer
	 - `ssh clucky@192.168.1.69`
	 - Password: spaceiscool639
 - Once connected, you just need to run `ros2 run testbed_rover_pkg testbed_rover`
	 - You should see "pico found" on a serial line
	 - If not, you'll get an error it's not found and the program will close. Ensure the teensy is connected via usb to the Nuc

## Connecting the GuliKit King Kong Pro 2 Controller (Recommended)

 - Connect controller to pc with USB-C
	 - Select the "D" control mode on the controller. 
		 - Hold the button next to the symbols (windows, android, switch, etc...)
		 - You'll need to release the button and press down again to cycle to the next mode

