epimetheus doesnt have an opto LED or a GPU to run SLEAP

## 3-11-2025 - bonsai and metheus notes with mary
### how to move the arduino?
- check that its off
	- use the opto control script to turn off the light if its on
- unplug the USB from the back (green board on the back) and replug into the other rig

- change the com# in bonsai (com 5 to com 3, or whatever is available on the bonsai)
	- theres only one port option, so just set up the output on that port

### setting up the new script
- switching SLEAP to the single instance model
	- the model file = .pb
	- training config = .json
(this single instance model switch should only need to be done once, so we should be good on this)

this current script does NOT have an ID determination component, i am just looking at if a fly is over the boundary or not AND THEN ill add the ID model
### 

## 2-28-2025
- in order to access opto on prometheus you ned to move the USB on the arduino
- blue is male and orange is female

- the ID model is weak AND the model keeps identifying the different lights as flies 
- SO 
	- take 10-20 (max 50) videos that are 1-5 minutes long
	- move the stadium lights around during the video
	- SLEAP train the model with variable lights (how to do this?)
- AND
	- for the ID model - take videos with clipped wings and unclipped wings to train the identity model
	- *need to buy some scissors to clip / how do other labs clip the wings*

- IDEAS
	- the model drops out when the fly rears up
		- change things in bonsai - if the fly rears up and model drops out have nothing change until the model comes back?
	- use bonsai to crop to the area of interest (the arena and the reporter LED)
		- try out and figure out how to do this - how to crop the image, this could remove the issue of false positives (other than the ones produced by the reporter LED)

get videos and try to crop the video at the same time - multiple avenues to try and solve the problems - work on it all at the same time