

from [[03-03-2025-Mon]]
- water filters replaced
- humidity tank cleaned
- humidity BEHAVIOR is unchanged, still climbing higher than programmed

- ev3 error - check in the manual
- fuji PX4F loop controller on our machine

ideas for what could still be going on / things to check based on the manual
- check the the water level in the humidity chamber is about 0.75 inches above the humidifier cross beam
- try autotuning the controller and chamber again 
- something wrong with the dehumidifier (pg 122 says ev3 is linked to the dehumidifier)
	- do our chambers have a dehumidifier?
	- dehumidifier operation mode accidentally changed?
- find and clean the humidity sensor inside of the chamber
- pg169 - reset the humidity to 70%, turn off and open for 4 hours, then power back on
- pg 170 -   "At set values 60.0% RH or less, ensure that the humidifier's ball valve on the dry pipe has been adjusted to approximately 75.0% closed."\
	- dont futz with this piece of advice too long, chamber is only at 60% to compensate for it going too high in the first place
- pg 172 - no dehumidifier and high RH% READ THROUGH AND CHECK
	- *based on a quick visual inspection it doesnt seem like our chambers have an external dehumidifier*
	- 'ev3 and heat only mode' - get the chamber out of heat only?

OKAY lets confirm if we have a dehumidifer or not and then check the ev3 heat only setting situation - change this and see if anything happens?
THEN reset, doors open and power off (set gabriel to 9-9, move flies to gabriel) for at leat 4 hours, power back and see if that helps

### EV3
- its not an ev3 led, its a little light up letter block - the same thing?
- check if its in heat mode only (BEFORE you fuck with settings TAKE PICTURES of what the current settings are)
what is heat mode only? what mode are beez and gabe both in?
ev3 indicator visible = setting on or off?
some indication that ev3 can mean multiple things? i checked the manual using 'ev3' and did not achieve clarity on this

[[03-05-2025-Wed]]
if the transducer was worn out it wouldnt be producing higher RH than required