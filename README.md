#Repo for exclusively running a S2 Modbus client

#Used for running on Truck's GOI

1. This repo has the required files to run a MODBUS client for the S2 HMI, which would connect to the Server on the Flagship truck's BeagleBone over the S2FlagshipWiFi.

2. This repo also has the necessary executables for the purple dot plotting and Train, Build, Follow. 

3. More details about these files and development notes are available in the developer's repo (which also includes this repo as a sub directory).


#Other notes

>>>>Be sure to check the mbhmi.config file while working with different servers.



#Steps to follow for client start up, and plotting of the data on an empty map

1. Make sure you're in the "hmiserver" directory. (There are sub directories with the same name, to avoid confusion, the "hmiserver" directory mentioned here contains ".sh" files and ".config" files and will have no ".py" files.)
2. Start the hmiservermbc_custom_beaglewifi.sh (by either Double Click, or type "./hmiservermbc_custom_beaglewifi.sh" in the terminal, to start the client software. Before this step, the laptop/computer/GOI should be connected to the S2FlagshipWiFi (or be on the same network connected to the LAN switch via ethernet).
3. On the browser go to http://localhost:8084??/s2o??build.xhtml to open the client HMI on the browser (fill ?? with latest build number "19"). [Sometimes there might be a problem of port being inaccessible, in which case, open the above said ".sh" file and change the port number - to 8085 say, and change it in appropriately in the URL.
4. Go into the hmiserver directory and and run " python hmiMBheartbeatclient.py " in terminal to start the heartbeat. #Currently not needed, as heartbeat is disabled from the server, but for safetly sake, reenabling this on both ends might be considered.
5. In the same directory run " python logXYdata.py " in the terminal to start logging the truck's xy position to file.
6. In the terminal run " gnuplot gnuplot.gnu " to start graphing the data which is updated every 1/2 second.

#Steps to follow for Train and Follow

1. Follow steps 1, 2, 3 as above and have the client started.
2. In the hmiserver sub-directory run the following programs:
	- recordData__.py [starts a recording program, which waits for input from GOI to start recording]
	- recordDataWhilePlayback__.py [does the record to file, during playback - data logging]
	- replayData__.py [Replays data from a successful train]
	- textDisplay__.py [Dispalys text instructions on GOI regarding the Train, Follow routes, this program also marks different states of the robot, which can be used in event of building a statemachine.]
3. Go to the AutoMode screen on the GOI (webpage as opened from the previous steps) and follow instructions on screen.

#Steps to follow for Plotting on Seegrid map

1. Take truck to appropriate position (see Point 4 for positioning details)
2. Start the Modbus server up on the truck.
2. Run the Python program "purplePlot__.py", this program starts recording data in the format to be plotted on the Seegrid map.
3. This program asks for position codes:
	1 - Starts at the bottom left corner of the MFG floor on the map (near the door to the kitchen) and start position faces in the direction of the Engineering Entrance door.
	2 - Starts at the bottom left corner of the MFG floor on the map (near the door to the kitchen) and start position faces in the direction of the MFG inventory/Building's rear exit door.
4. Enter the desired code (making sure the truck is positioned accordingly.
5. Start driving and see the plot live.
6. The server and the client need to be restart everytime you want to restart the mapping because the current software does not Clear encoders (will be fixed in a later version), and restarting the server clears them.

#Steps to follow for the Capture image from front facing IP Camera when truck stops

1. Have the server started on the Truck.
2. Run the python program "capturePic__.py" (from a laptop or whereever you would like to save the pic).
3. This would capture an image everytime the truck stops and save it to the computer.


