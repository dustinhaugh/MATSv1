SOFTWARE SETUP INSTRUCTIONS FOR MATS VERSION 1

1. Modify config.json

	

1.1 Open config.json
It will look similar to this:


{
    "comPort": "COM9",			# ADJUST IF NECESSARY: COM port to the PTR, this can be found using Device Manager
    "gps_altitude": 2993.0,		# ADJUST IF NECESSARY: PTR altitude in ft
    "gps_latitude": 43.049511,		# ADJUST IF NECESSARY: PTR location in DD format
    "gps_longitude": -115.866452,	# ADJUST IF NECESSARY: PTR location in DD format
    "ipAddress": "0.0.0.0",		# ADJUST IF NECESSARY: DIS feed ip address
    "port": 12345,			# ADJUST IF NECESSARY: DIS is port 12345 for the RANS
    "targetMarking": "0165"		# DO NOT ADJUST: The target will be modified by mats_gui.exe
}

1.2 The DIS feeds from com are being sent to a specific address and port, get that information from them. 

1.3 Adjust comPort if necessary:  (This is a string and needs "" around the value.)
		Search for "Device Manager" in your computer task bar. In the device manager look for Ports (COM & LPT).
		Look for devices connected. It might be under "Prolific PL2303GT USB Serial COM Port". Record that
		com port to the key value "comPort" in config.json.


1.4 Adjust gps_altitude if necessary:  (This is an integer so do not put "" around the value)
		This value will be in ft. Any necessary offset to correct and correlate with targets is fine to add here.

1.5 Adjust gps_latitude and gps_longitude if necessary:  (These are integers so do not put "" around the value)
		These values are in Decimal Degree format. For example -115.866452 is an acceptable value.

1.6 Adjust ipAddress if necessary:  (This is a string and needs "" around the value.)
		Default value: "0.0.0.0"

1.7 Adjust port if necessary:  (This is a string and needs "" around the value)
		The range network on mt home typically uses port 12345 for DIS but check with COM.
		The DIS feed is sent via the MSCT at Cowboy to specific IP addresses. 



2. Modify local network adapter

2.1 Open Control Panel > Network and Sharing Center > Change adapter settings > 
2.2 Look for the network adapter that is currently being used to connect to the range network.
2.3 Right lick on that adapter and choose properties.
2.4 Double left click on Internet Protocol Version 4 (TCP/IPv4) Properties.
2.5 Set the IP address and Subnet mask to values given by COM for the JMR Tracker DIS.
2.6 Select OK (window closes) and select OK again (next window will close).
2.7 Close Control Panel Window(s).
	


3. Check PTR connection

The PTR can be connected in a variety of ways by either using a USB to RS-232 adapter, or directly using 
an RS-232 cable depending on your needs. If you run the mats.exe program and it is not able to talk to
the PTR despite having the correct settings the PTR might need to be reset. To do this you can use the 
QPT-20/90 Remote Control Emulator program to do so. Follow the following procedure to reset the PTR.

3.1 Open the QPT-20/90 Remote Control Emulator program
3.2 Set Port to the correct COM port connected to the PTR. 
	If using a USB to RS-232 adapter it might be setup using COM9. This program only allows COM1-8. 
	If this is the case and it needs to be reset, contact Dustin for a python program that will 
	reset the PTR. 
3.3 Select the "Start" button
3.4 It will go through a process to clear internal flags and allow movement of the PTR. 



4. Execute mats.exe


5. Execute mats_gui.exe


6. Open another program that allows you to see an air picture or open airpicture.json in VS Code

6.1 airpicture.json will automatically populate with aircraft Mode 3's captured in DIS within the last 10 seconds. 

This is an example of airpicture.json:

{
    "airPicture": [
        "4323",
        "0161",
        "0142",
        "0162",
        "0165",
        "6053",
        "0141",
        "1772",
        "6333",
        "0163",
        "6077",
        "7470",
        "6066",
        "1652",
        "3376",
        "0234",
        "3626",
        "4340",
        "0572",
        "4335",
        "2452"
    ]
}

If airpicture.json populates with Mode 3's then you are getting DIS feeds correctly. If your PTR doesn't move and
you are getting an air picture then the PTR needs to be reset. 
