# DAY 1
- mostly mouse stuff 

calcium is a proxy measure - keep that in mind
- pick a gcamp based on the speed of the reaction and based on what experiment youre running

calcium can be intracellular or extracellular and right now there is no way to pull those two apart

## Integrating behavior and video data
**the key is that the timing for the video frames and the imaging frames need to be saved IN A CENTRALIZED LOCATION**

each frame needs an associated time code - after the experiment you can sync up the data by syncing up the time codes

there are several methods for syncing video data and imaging data

### with TTL CAMERAS
#### independent 
- send the timing of the 2p frames and the timing for the video frames to an arduino (or DAQ - depends on the microscope) and then align them post hoc
- the video brightness will fluctuate - based on the difference in framerate between the imaging and the video
#### entrained
- the microscope frames go to an arduino / DAQ - this then triggers the camera to record a frame
- the data is already synced and doesn't need to be synced post hox
BUT
- this only works if the video and imaging have the same frame rate / it caps the frame rate of the video to the framerate of the calcium imaging

### non ttl cameras
- a camera that can't record frame timing or be triggered by an arduino/DAQ
heres how to synch data with non ttl cameras
1) record the imaging frame to an arduino / on board microscope DAQ
2) the arduino / DAQ will trigger an LED set in the filed of view of the video camera

using the LED flashes (with timing that is saved in the onboard DAQ with the imaging frames) you can align imaging and behavior video using the LED flashes 