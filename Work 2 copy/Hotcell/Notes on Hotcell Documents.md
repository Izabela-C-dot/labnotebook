# NSF grant
## notes
EXPERIMENTAL GOALS (once hotcell experimental set up troubleshot)
1) Does female mating status affect female driven courtship?
	1) virgin female flies with hotcell males and previously mated female flies with hotcell males, expect the previously mated females to vigorously reject male advances
	2) Do female flies take an active role in initiating copulation or do they wait to be courted (which is the assumed paradigm in traditional courtship assays)
2) How does auditory stimulus affect female behavior during courtship?
	1) female fly and mute (wingless) male fly with either a) conspecific courtship song or b) synthetic songs (ie some noise not courtship specific)
	2) How do female flies respond to these different songs? Do the conspecific songs lead to the female fly initiating more courtship behaviors?
3) Test proposed neural circuits related to mate rejection
	1) R2/R4m neurons signal using dopamine. Using RNAi to break down this signaling has decreased copulation in past assays. It is unknown if this break down in signaling affects only short term rejection behavior (ex. kicking) or if it has some affect on outright mate rejection. Affecting outright rejection would imply that the R2/R4m neurons have a role in mate evaluation and therefore higher level decision making in the fly.
	2) Do female flies with lowered dopaminergic signaling (ie less R2/R4m activation) avoid the male flies more often?

POSSIBLE RESULTS
1) female flies stay on the male seeking side (ie not hot cell activating side) but still show 'rejection' behaviors (wing flicking, kicking, running away) 
	1) this would reframe 'rejection' behaviors as a part of the courtship process (imply more of a give and take? a call and response to courtship?)
2) female flies generally stay on the male avoiding side (hot cell activating side) - leads to further work about what neurogenetic factors affect this behavior (ie we now have an experimental set up and a baseline (female avoid male) to test out different genes to see which have an affect on female courtship willingness(?))
## questions
- is it important that the female knows that one side of the arena is a 'safe' zone?
	- how quickly can they learn this, or would they just naturally run away, end up in the 'safe' side and realize the male can't follow them?

# female choice pilot project pptx
## notes
- delay on opto means the male walks into the refuge, pause, opto leading to the male trying to run further into the refuge 
	- male is not learning where the refuge is
- male won't attempt courting at all, won't move, even when the opto is off 
	-  *i think this is because the male is getting opto in a way that feels unlinked to its behavior - ie there isn't a clear connection to the fly between behavior and stimulus so its trying to remove all behavior to avoid stimulus*
## questions
- what did the previous frequency filter do? (like it cut down ID switching, but functionally what did it do to achieve that result?)
	- it added latency, but could we add the filter back and cut latency in another way (ie frame rate) to compensate?
	- what contributes to latency generally? ie what are the features that increase latency and what are the features that decrease it, and how can we play around with them?
	- BUT the frequency filter maybe led to skipping frames - which would be BAD (less accurate read of behavior -> less accurate teaching signal)

# female choice pilot project notes
## notes
- adding back the frequency filter is likely a nonstarter - caused dropped frames and huge latency - see what else we can do to improve identification
## questions
- what is the issue with the mesh refuge? 
	- *cant observe using cameras*

# Effect of a refuge from persistent male courtship in the _Drosophila_ laboratory environment (ie mesh refuge)

## notes
- yeah we dont want to do a mesh refuge because it is unable to be filmed in our rig AND controlling for body size the way they have to sounds like it takes a long ass time + a lot of effort

- so remating is lower with a refuge but female harm is unchanged with a refuge
	- female harm measured by fecundity
- there was significant remating in the refuge vials (like ~32%), even if there was a reduction when compared to the no refuge vials
	- so a lack of refuge changes male-female fly interactions, but not the harm caused to the female flies?
- SUMMARY 
	- the lack of a refuge in past experiments does not have a large/significant effect on harm done to female flies
	- (they dont really provide a conclusion for the mesh refuge/remating experiment so i will write one myself)
		- the presence of a refuge changes remating reates by changing the interactions between male and female flies - when the female flies have the ability to escape male courtship, there is a reduction in courtship - this implies that there is more research to be done in the area of female driven courtship 
			- what other changes appear when female flies have more control over courtship? do the observed behaviors change? does mate choice change?
## questions
- is visual separation from the male important? this paper includes it in the secondary experiment, but i dont know if its actually a valuable thing to try and achieve or just a purported benefit of the specific refuge set up this group made
- "The observed significant reduction in female remating when a refuge was present indicates that the lack of a refuge in the laboratory has an effect on male–female interactions, *but the fact that remating rate was reduced by ∼25% indicates that this effect is quantitative, rather than qualitatively changing the net harmful effect to females of persistent male courtship*."
	- i am confused on what this is trying to say - the effect of a refuge has a quantitative effect (numerical) on remating, not an observed effect on harm done to female flies 
		- *is female fly harm not quantitative - they dont really talk about it in this paper*
		- so remating can't be the main reason of harm due to female flies? because there was remating but no change in harm?
	- paraphrase - male harm to female flies cannot be attributed to a lack of spatial refuge

- ALSO the animals were nutritionally manipulated (females smaller, males larger) for the experiments, and large males normally do more harm than smaller males
	-  this would make the harm done to females higher in this experiment than it would be normally, but the fact that no significant difference in harm was seen even with this intensifying factor makes the results more convincing (?)
# Ovipositor Extrusion Promotes the Transition from Courtship to Copulation and Signals Female Acceptance in _Drosophila melanogaster_

## notes
- there is give and take in dros mating 0 female extends ovipositor in response to the males song to signal acceptance (active participant)
- has to extend and then retract to show acceptance and allow a mating attempt to occur
- the female takes active steps in not just rejecting a mating attempt but accepting a mating attempt (so its not like the options are 'no' or 'indifference and passivity' its 'no' and 'yes')
	- there is female agency in mating
	- *having a experimental rig where that agency can be more fully expressed (ie full escape from mating attempts) would be helpful*

- this experiment uses a closed loop system - will it go into depth how?
	- specifically on the position of the two flies (not sex id(?) but of different sex)

- ovipositor retraction is an ACTIVE movement that overrides the IR light stimulation
	- mating drive strong enough to override the neuro manipulation and allow the copulation attempt to proceed
## questions

# general questions
- other papers with closed loop experimental rigs?
- i think it would be useful if i get a basis in bonsai 
	- basics + information how tos?
	- i have to know what is happening to know where to go
- is hotcell only on prometheus or epimetheus as well?

- watch the hotcell videos to get a sense of what is going on 