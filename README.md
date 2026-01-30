# lan-rtsp-camera-wall
Self hosted rtsp security camera viewer.

I use this to monitor my home security cameras on a dedicated machine.  
I was using the Reolink app but a recent update borked things and it did not work well anymore.
  
Runs a MediaMTX docker container and a container to serve the html page (localhost:8080).

Command to run on machine startup `google-chrome --kiosk http://localhost:8080/`
  
Notes:  
1. Only tested on Ubuntu and Chrome.
2. You need to edit the rtsp paths in mediamtx.yml.
3. No sound as MediaMTX did not easily support the sound my Reolink cameras put out. Though you could add this and add a sound button to the html.  
4. ~~No way to reorder the cameras in the html page itself. You can change the html source to do it (it's just css changes).~~

# My Setup:

I am running a Ubuntu server machine with LightDM and Openbox and I've set the powerbutton to suspend.  
I have it connected to a cheap touchscreen.

LightDM settings at /etc/lightdm/lightdm.conf
```
[Seat:*]
autologin-user=myusername
autologin-session=openbox
```

Openbox settings at ~/.config/openbox/autostart
```
xset s off
xset -dpms
xset s noblank

# Hide mouse cursor when idle
unclutter -idle 2 &

# Give X time to settle
sleep 5

# Auto-restart Chrome if it crashes
while true; do
  chromium-browser \
    --noerrdialogs \
    --disable-infobars \
    --kiosk \
    --touch-events=enabled \
    --disable-pinch \
    --overscroll-history-navigation=0 \
    --disable-features=TouchpadOverscrollHistoryNavigation \
    http://localhost:8080/
  sleep 2
done &

```

Power button set to suspend in /etc/systemd/logind.conf
```
HandlePowerKey=suspend
```

