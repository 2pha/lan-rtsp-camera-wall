# lan-rtsp-camera-wall
Self hosted rtsp security camera viewer.

I use this to monitor my home security cameras on a dedicated machine.  
I was using the Reolink app but a recent update borked things and it did not work well anymore.
  
Runs a MediaMTX docker container and a container to serve the html page (localhost:8080).

Command to run on machine startup `google-chrome --kiosk http://localhost:8080/`
  
Notes:  
1. Only tested on Ubuntu and Chrome.
2. No sound as MediaMTX did not easily support the sound my Reolink cameras put out. Though you could add this and add a sound button to the html.  
3. No way to reorder the cameras in the html page itself. You can change the html source to do it (it's just css changes).

