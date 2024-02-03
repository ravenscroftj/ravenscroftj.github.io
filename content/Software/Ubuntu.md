- ## Sound Problems - 20.04
	- Occasionally after connecting a bluetooth headset or even just on restarting the system, garbled sound output is produced
	- ### Restart Pulse Audio
		- Try running:
		  ```
		  pulseaudio --check
		  pulseaudio -D
		  ```
-