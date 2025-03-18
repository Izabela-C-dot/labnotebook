# obstacles
## Model swapping the Identity of the flies (female and male) during the experiment

## male fly stops moving and won't perform any behaviors
- overstimulated by the opto? 
- confused by the opto being triggered in error - so not in response to the male flies behavior - so they don't do any behavior in order to avoid triggering the opto?
	- (ie they don't know whats causing them to be hurt - so they just try and be not hurt by not moving)

# troubleshooting ideas

## lower the frame rate of the video
- mateo has found that lowering the frame rate of the camera has positive effects on the latency (ie lower frame rate lower latency) so this could be a worthy thing to look at first
	- latency is causing the opto to trigger considerably after the male performs a behavior - so decoupling the punishment from the behavior, which removes the teaching element
	- the goal is to have the camera frame rate at 150 Hz (to capture all fly behaviors) BUT there is some wiggle room here
### what do i need to do this?
- how do i find the framerate of the video camera
- how do i lower the framerate of the video camera?
- how do i quantify latency?
- what will indicate to me that lowering the framerate is worth removing latency?
	- ie. what do we get from higher vs. lower framerate? what do we get from lower latency?

## maybe the hotcell line isnt the best to use in this experiment
- how would i determine this?
	- papers talking about hotcell vs other genotypes?
		- what makes hotcell special - what does hotcell actually do - what other lines do things like what hotcell can do
	- starting other crosses to test against the hot cell line
		- find other genotypes and compare them on paper to hotcell (whats similar / whats different)
		- find them and order them - quarantine them and cross them
		- test them against hotcell flies in the same schema - which performs better?
			- how to run these tests?
			- how to quantify what better means?
## use a visual indicator of the hotcell in the arena
- provide the flies with light and an indication of the different sections (ie a line in the center - a different color background?)
	- *how would this interact with sleap models?*

## add a sight light so the flies can see each other in the arena
- it is possible the flies can't see each other at all, which would contribute to the males not engaging in mating behaviors
	-  *how would this interact with the camera?*
	-  *how would this interact with the sleap model?*
## let the male acclimate in the arena before adding the female
- this would allow the male to learn how the hotcell arena works before adding in any other stimulation / information
	- if the male would get overloaded with stimulation this might not work 
	- it might be hard to load in another fly while one is in the arena 
	- we need to solve the ID flip issue before this - whats the point of the male fly learning if he gets triggered erroneously

## add a white dot of elmers glue on the female fly to allow the bonsai to see the female better
- less incorrect hotcell triggers on the male, so they can learn the hot zone + not be too stressed to court
	- how would this affect the sleap model?
	- how could be get the sleap model to know that the white dot means female?
	- would the glue dot affect the female flies behavior in a measurable way?
	- would the glue dot change how the male fly attempts to court the female fly?
	- how much time would the labor of adding the glue dot to all females add to this experiment?
## have the flies start courting and then turn on the opto 
- have the female and male fly in the arena together with the male able to go everywhere in the arena and then turn on the opto later 
	- how would this affect the flies learning?

# ideas for further research to inform troubleshooting
- are there other boundary experiments? Is the boundary marked? would marking the boundary make the safe and not safe zones easier to learn?
	- how would this affect the sleap model? would it need to be retrained?
	- would the model be able to read position of the flies while they are over top the boundary?

# order
- ~~contact mary for her NSF paper
- ~~read hot cell paper
- ~~get marys hotcell powerpoint
- write out hotcell ideas and questions 
- set up a meeting with mary about hotcell 

develop an understanding of the component of hotcell project
- sleap model
- closed loop
- bonsai
- hotcell genotype
- what has been tried previously

~~know the details of the hardware and software to begin playing with parameters~~
play with parameters AND learn about the system simultaneously 

# structure

there are different layers of a problem that are happening here and they need to be addressed sequentially.

**LAYER 1:** Functionality
- Latency between the male entering the 'hot' half of the arena and receiving optogenetic stimulation
- The identification of the male and female fly switching in the middle of the experiment - causing the male fly to receive optogenetic stimulation when it is NOT in the 'hot' half of the arena

**LAYER 2:** Having the intended effect
- Is the male fly able to learn that there is a 'hot' half and a 'safe' half?
- Is the female fly able to learn that there is a half where it will not be persistently courted?
- Will the male fly attempt courting in this arena at all?

- how do we prove that the experimental rig is functioning as intended?
	- *ie how do we prove that the dros are doing what theyre doing for the reasons we say they are doing it*

**LAYER 3:** Experimental function
- What experiments do we design with this rig?
	- what do we want to test?
	- how do we set up an experiment to test it?
	- how do we know we are testing what we want to test?

right now we are focused on **functionality** - actually getting the rig to behave how we want it to

## LAYER 1
- what could be affecting latency?

- what could be affecting identification switching?