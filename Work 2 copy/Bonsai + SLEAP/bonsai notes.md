
[[1-28-2025-Tue]]
going through bonsai github

[numpy primer](https://numpy.org/doc/stable/user/absolute_beginners.html)
- how is np.arange() different than np.linspace()?
- whats an indirect sort?
- concatenate?
- c type index order? fortran index order?
- really strong foundation in array + index + indices + vector 

the count starts at 0, row is labeled first ([row,column])
rows = 0
columns = 1

[[1-29-2025-Wed]]
python has a built in help() function to access documentation inside of the program
? also gets you to the documentation

importing and exporting a CSV is easiest with pandas
import pandas as pd

matplotlib could be a useful thing to learn (later on, not for hotcell rn)

[bonzeb](https://ncguilbeault.github.io/BonZeb/basics/)
i cant access bonsai on the mac i have in my office - so where would be the best place to sit and learn it?
- 342?
- my laptop?
- 365?
	- probably not 365 if people need to be running tests in there

Basic layout
- toolbar on the left of the interface - modules browsed and selected here - can use the search bar to find modules if you know the name
- set the specifics of each module (the time for a timer, where to save + what to name a file etc) on the right hand side with properties
- the specific module that causes an error will turn red - to indicate that it is the area that is causing a problem

hot and cold sequences
- hot sequences - always producing new data regardless of whether or not the downstream nodes are ready to receive new input 
- cold sequences - waits to produce new data until the downstream node is ready to accept new input

- bakery analogy
	- hot - bakery makes bread every hour + throws away bread if it is left over from the previous hour. if a customer comes in and buys the bread, the second customer must wait until the new hour for new bread 
		- *the data produced is independent from the thing using/requesting it*
	- cold - bakery only makes bread after receiving a customer request
		- *data is not produced until it is needed*
- hot and cold sequences - even if they appear equivalent, can produce very different outcomes

types of nodes
- a few major classes of modules
	- sources
	- transforms
	- conditionals
	- sinks 
	- combinators

- SOURCES
	- produce data 
	- usually upstream in the pipeline
	- ex. cameras, arduinos, microphones, timers etc

- TRANSFORMS
	- take input and produce and output
	- sometimes the input and output will be the same type of data, sometimes the input will be one type of data and the output is a different type of data

[[1-30-2025-Thu]]

- CONDITIONALS
	- apply some operation to filter the input
	- like an if statement EXCEPT the output is the original input and the boolean operation is used to decided to pass the data down or not
	- *like a gate - the data is unchanged, it either passes through or is stopped*
- SINKS
	- perform side operations on the input without modifying the data 
	- ex - saving data to a CSV, writing videos
- COMBINATOR
	- catch all class for all other nodes
	- combinators have specific functions

data types
- bonsai contains standard data types 
	- integers, floating point numbers, character strings etc
- output of a module can be a standard data type or a data structure 
	- output of FIleCapture mod (reads and video and outputs the frames inside a bonsai workflow) is a OpenCV.Net.lplImage
		- complex data structure that contains the image itself AND properties about the image
- view output type by clicking on it and looking at the properties popup

member selectors
- properties of any output can be accessed individually by selecting the property OR by using a MemberSelector node
- THEN the output properties can be used as (passed down as) inputs in downstream nodes 

externalized properties 
- each modules has a unique set of user defined properties 
- these properties can be changed manually 
OR
- set the value of the properties within the workflow using externalized properties and property mapping
- externalize a property - make it accessible in the bonsai workflow (IE able to be changed by things in the bonsai workflow)
- right click a node, select the property to externalize from the 'externalize property' list

property mapping
- output of a module can be passed as an input to a property
	- this is used to change a property at the start of a workflow OR dynamically
	- NOTE some properties update while a workflow is running and some only update once the workflow has been restarted
- PropertyMapping module used to map inputs to properties of a module in a single node
- InputMapping node is different - synchronize the update of a property to the timing of an input
	- string node can be used as input to the FileName externalized property of the FileCapture node

- in an externalized property, the externalized definition will override the property set in the nodes property section
- changing the property in the property section WONT propagate upstream to the value of the externalized property 
- REMEMBER the value of the upstream externalized property must be set in order to update the property of a node downstream
	- *ie if the definition of a property is externalized upstream of the node the property is attached to, changing the externalized property value in the properties section WONT define it in the upstream section*

property source
- used to generate a source node corresponding to a property of a node
- the property source will generate the same data type of the property selected 
	- PS used to set the property of a node using property mapping
- USEFUL FOR - making a source node for a specific data type and then broadcasting the property to nodes throughout the workflow

- EX - PositionUnits property of FileCapture modules uses a specific data type called CapturePosition
	- CapturePosition not available as a source module in the toolbox, so a PositionUnits property source can be generated from the FileCapture module to set the PositionUnits property
	- *ie use a property source to set the properties of a data type that isnt available to select from the bonsai library - create a way to set a property directly from the node that needs to have the property set itself*

visualizers 
- allow users to view the observable sequence generate by each module
- appear when the workflow is started and node attached to visualizer is operating
- each module has a different set of visualizers associated with their specific data types

data type visualizers
- many visualizers can exist for the same data type
- double click on node while workflow is running to see the first visualizer

combinators
- diverse group of useful operations
- key combinators to understand? (these three all combine individual elements from multiple data streams into one data stream with multiple elements)
	- zip
	- combinelatest
	- withlatestfrom

ZIP
- only produces output when all upstream data streams produce a value
- limited by the timing of the slowest input stream 
- output always link the sequences of inputs together
	- VALUES FROM THE FASTER DATA STREAM WILL BE SLOWED DOWN / LIMITED BY THE SLOWER DATA STREAM *ie the faster one cant fire as fast as it wants, so the values it produces are delayed*

COMBINELATEST
- produces an output each time an input datastream is updated
- timing is faster than all input data streams
- output consists of the most recent combination of inputs
	- produces more values than either upstream data stream, because a new value is made every time one of the upstreams fire

WITHLATESTFROM
- produces an output each time the driving input produces a value
- timing is the same as the driving sequence
- output consists of the most recent combination of input streams when the driver stream produced a new value

NOTE - You can set 2 timers to both fire at 5 seconds BUT the timings are not synchronized and the timing will be off - keep this in mind while building pipelines

groups
- a module that is a subclass of a combinator 
- encapsulate a more complex workflow into a single node 
- various different types of groups including -

NESTEDWORKFLOW
- puts a complex workflow into a single node + sequesters it
- defining something in a nestedworkflow will make it only accessible to subscribers INSIDE of the nestedworkflow

GROUPWORKFLOW
- puts a complex workflow into a single node
- subjects defined inside can be accessed outside of the groupworkflow

INCLUDEWORKFLOW
- encapsulates an EXTERNAL bonsai workflow (one that was saved into a separate file) and brings it into the current workflow as a single node
- subjects defined inside are globally accessible outside of includeworkflow

CREATEOBSERVABLE
- generates a higher order observable sequence using the enclosed workflow
- higher order? essentially an observable sequence of observable sequences *a folder*

SELECTMANY *what?*
- similar to create observable EXCEPT it generates a single observable sequence for each input + merges the inputs together to generate output
- *i think it means that it makes a little data line (little plotted out node and connection line) for each input BUT combines all the inputs to generate 1 output (a folder that condenses what is within it)*

SCAN
- similar to a recursive function - a function that calls itself, used to solve problems that can be broken down into sub problems
- input to SCAN includes an output input sequence AND the output of the scan sequence

CONDITION
- a type of group node that filters input data
- use the encapsulated workflow to run a boolean comparison of the dat
	- if true? - data passed downstream
	- if false? - no data passed down

subjects
- take the output of any module and broadcast it to other parts of the workflow
- functions like a global variable
- different ways to define subjects to produce different workflow results
(from [bonsai documentation on subjects](https://bonsai-rx.org/docs/articles/subjects.html))
- acts as a bridge - subscribes to an observable sequence and passes all items to multiple downstream operators 
- ie - turn complicated parts of code into modular bits that can be replaced easily

- source v. sink subject
	- source subject - no pre-existing input, they are a way to redirect multiple data writers (a direct source of data like a camera, not a bonsai input) into a single reader (for logging or control)
	- 

TYPES OF SUBJECTS
- PublishSubject - changes a cold sequence into a hot sequence
- ReplaySubject - changes a hot sequence into a cold sequence
- BehaviorSubject - sim to replaysubject except that it will wait for subscription even if the sequence it is broadcasting has been terminated *what does that mean*
- MulticastSubject - pushes values from one data stream into a subject originating from a different subject
- SubscribeSubject - gives access to the observables of a subject (use to access the observable sequence of another subject)

multicast and subscribe are used to access existing SUBJECTS to either write or read (multicast = write / subscribe = read)
behavior depends on what type of subject they are accessing

depending on the subjects placement in the group nodes they will only broadcast the subject within the group node and not to the whole workflow

[[2-3-2025-Mon]]
subjects example with timers
EXAMPLE 1 (timer at 3 and 5, zip, combinelast, withlatestfrom combinators)
- subjects are also used to LABEL THINGS in workflows
	- which timer fires at 3 seconds and which at 5?
	- which combinator (zip, combinelast, withlatestfrom) corresponds to which data stream?
- PublishSubject nodes added to label the outputs
	- subjects are a type of sink, they pass along input without modifying it
	- here, just used to label 

EXAMPLE 2
- timer set to fire every 2 seconds
- output passed to either a ReplaySubject or PublishSubject
- in SEPARATE DATA STREAM - SubscribeSubject is used to access the data from either Replay or Publish, with a DelaySubscription mod used on Subscribe to delay subbing to data for 3 seconds

- after 2 seconds, timer values are sent to publish and replay
- after 3 seconds, subscribe has passed the delay period and separate subscribe mods are now subbing for both publish and replay
NOW
- only Replay produced a value on subscription (its a cold data stream, so it gave the subscribe mod the most recent value)
- Publish is a hot data sequence, so the value that got sent out BEFORE subscription was tossed
NOW A CHANGE - take module added post timer to stop the workflow after the first value is produced
- BehaviorSubject added to the workflow
- despite the take module, the workflow continues to run 
	- Behavior will wait to produce a value to any mod subscribed to the sequence, even if the data stream producing values has been terminated
	- only works if a subscriber is stuck to behavior, remove SubscribeSubject from BehaviorSubject and the workflow terminates as normal
*^^ i dont understand what this means*

Bonsai shaders, vertex files, fragment files, shader configuration, uniform variables all skimmed because i do not think they will be particularly relevant to the work i need to do

OKAY bonzeb done

[bonsai documentation on the website](https://bonsai-rx.org/docs/articles/packages.html)

# get started
## package manager
- when you first run bonsai required packages are auto installed
- you can add other additional packages (made by bonsai or by other users)
## workflow editor
- the editor has three main panels 
	- toolbox - to grab new modules
	- workflow - to arrange observable sequences
	- properties - configure the modules

### toolbox
- organized into 6 main categories - color and shape coded
	- source, transform, sink, combinator, workflow, subject
	- (green, blue, purple, yellow, yellow with dashes, X)

- double click or drag your chosen operator into the workflow 
- OR right click and select a specific place 

- search operators
	- you can search for operators directly, specific names and category names
	- can also find existing instances of an operator in the workflow

### workflow
- the panel where you combine operators to create pipelines
- nodes are pulled from the toolbox and then connected together

- right click to bring up the context menu for the specific node you selected OR a list of possible actions you can do with the current selection
- one node selected? output menu displays the type of elements emitted by the operator sequence

- right clicking brings up the context menu which allows you to externalize public properties as explicit nodes in the workflow by using the 'externalize property' drop down menu
- externalized properties can be connected to other nodes to dynamically change the property value

- you can also group nodes and encapsulate workflow fragments into a single node (GroupWorkflow)
	- can be assigned a name and a description

type visualizers
- you can inspect the data generated from a specific node during the execution of the workflow
- visualize the result of specific operations or to debug the behavior of the workflow
assigning visualizers
- types can have more than one visualizer 
	- image data streams can be displayed using the default image visualizer BUT you can also select to inspect image parameters to find the size and pixel bit depth 

workflow extensions
- you can create and save workflow extensions by selecting one of more nodes and then 'Save Workflow As'
- allow you to reuse common workflow patterns across a large project 
- extensions show up in the tool box panel for placement
	- placing a workflow extension creates a new 'Include Workflow' operator that directs to the saved workflow 

any named externalized properties from nodes in IncludeWorkflow will be shown as properties of the include node itself
these externalized values can be different in different instances of the same workflow extension

you cannot change the internal structure of the extension once it is loaded into the workflow, only the properties inside of the extension

to change the implementation of the extensions
- ungroup the IncludeWorkflow operator 
- this makes a copy of the included work flow and places it inside of GroupWorkflow
- THEN you can modify the internal nodes, and then save the extension again with 'Save Workflow as'

NOTE 
when you change the structure of the included workflow and save it over the original, all previous mentions of the workflow extension will be automatically reloaded and updated to ensure the extension is consistent throughout the code

### properties
each operator has a set of properties that set the operators behavior 

properties panel will display all available properties for the chosen operator

most properties can be configured by changing the value in the corresponding row of the property grid
some have further specialized editors that can be accessed by clicking the drop-down or dialog button

### commands and shortcuts
oh this is just a list of shortcuts - we will come back to this if i need to, but i won't take notes on it rn

the majority of things seem to be accessed by right clicking or double clicking

when im working more vigorously on the code ill look into shortcuts

## bonsai gallery
examples of code are in the bonsai gallery of example workflows
access this in the 'tools' section in the workflow editor

you can run adn modify the example, everytime you open the example it will generate a new clean copy of the workflow

ENVIRONMENTS LEFT
https://bonsai-rx.org/docs/articles/environments.html

[[2-4-2025-Tue]]

## environments
- an environment ins a self contained + portable installation of bonsai that records a snapshot of all packages required to run your workflow
	- this is to protect against updates breaking older workflows / workflows containing obsolete packages being unusable
	- it also makes it easier to share projects + keep track of individual projects on the local machine

### environment basics
(details on making environments, similar to the shortcuts, record this later)

[[2-11-2025-Tue]]
# language guide
## observables
observable sequences are the central concept in bonsai
what is an observable sequence and how are they manipulated in bonsai?

### introduction
an observable is a sequence of elements ordered in time 
they are asynchronous

OSs (observable sequences) can be infinite or finite and can terminate with 'OnCompleted' or 'OnError'

### reactive programming
in reactive programming we compose operations on sequences in order to define new sequences
(ie you apply an operation to a sequence and it generates a different output sequence based on the operator)

### bonsai workflows 
bonsai uses a graphical representation called a workflow to create and image complex combinations of operations on sequences

in a workflow each node is an operator
nodes can be connected to other nodes
- nodes to the right are 'upstream' and nodes to the left are 'downstream'

chain nodes together to make complex interactive systems 

workflows can be visualized using marble diagrams but they are NOT equivalent (marble diagram shows whats happening as we move through time, workflow is just a map of the total operation without consideration to time)

marble diagrams can be useful to graphically convey what an operator is doing (use in troubleshooting maybe)

### hot vs. cold observable sequences
different delivery method of information affects the 'temperature' of a sequence which changes the side effects of subscription

(ie CameraCapture vs. FileCapture - different temp, different effects on the system)

#### hot
Hot observable sequence : bread is baked once every hour and if no one picks the bread up, its thrown out OR it is a movie seen in the theaters, you show up late and you miss the beginning, there's no going back to see it 

CameraCapture is a HOT sequence - if the camera starts recording at t=0 and a sequence subscribes at t=3, all of the data captured by the camera before t=3 is lost and NOT passed downstream

ALSO every subscriber gets attached to the same data producer (ie the camera feeds all of them information based on when they subscribe, and they can never receive data from BEFORE they subscribed)

the hot observable produces data EVEN IF no one is subscribed (the camera will still see you even if no one is saving )

#### cold
Cold observable sequence : bread is baked whenever there is an order for bread placed OR it is a movie watched on netflix, put it on whenever and you get the whole movie

FileCapture is a COLD sequence - the data is stored in the computer, and any subscriber will receive ALL of the data, no matter when they subscribe

data is only produced from a cold observer when it is requested, and every request gets the same set of data

understanding the temperature of an OS is super important when more the sequence is shared with multiple operators BECAUSE the different temperatures interact with operators differently 
- ie if you are using a hot sequence and don't subscribe at the beginning of the workflow you will LOSE DATA
- whats the effect of subscribing at different times?

you can also change the temperature of an OS using certain operators
- REPLAY can be used to subscribe to camera and record all incoming images
	- anytime a downstream operator subscribes to replay it will receive all images taken from the camera, no matter when it subscribed
	- hot sequence transformed into a cold sequence
- PUBLISH can be used to share a single subscription to a video file with multiple operators
	- anytime a downstream operator subscribes it will receive the images CURRENTLY coming from the original subscription
	- cold sequence into a hot sequence

benefits of hot vs cold?
- HOT
	- PROS 
		- single input stream able to be sent to multiple subscribers
		- all subscribers receive the same sequence of values at the same time starting from when they subscribe
		- dont have to create a new connection for each subscriber, saves space
	- CONS
		- data produced prior to subscription is lost
- COLD
	- PROS
		- each subscriber gets its own sequence of values
		- ideal for asynchronous operations

## operators
bonsai programs are built on chained operators to create sequences 

operators can be roughly grouped into different characteristics
- source
	- generate event streams 
- transform
	- convert/change individual data items
- condition
	- filter data items based on a condition
- sink
	- save data or trigger external outputs
- combinator 
	- complex - manage flow or synchronize inputs

### SOURCE
create sequences the generate data spontaneously - they don't need to have anything upstream of them - they generate input for other nodes
- HOWEVER they can be attached downstream to nodes for a variety of reasons
	- to precisely control video playback - only advancing in a video when input is received etc

every bonsai program has at least one source

usually sources represent streams of data coming from DEVICES or FILES (ie a camera or a video file, a microphone or a .wav file)

### TRANSFORM
transforms apply an operation to individual data items in a sequence 

they take exactly one input and produce exactly one output that ALWAYS has the same number of elements as the original input BUT the elements have been modified according to the function of the transform

every transform produces exactly 1 output for each input
the output is created immediately when the input is received 

when the input sequence terminates, the transformed sequence terminates

the only difference between transforms is the exact function applied to the input sequence (grayscale, find contours etc)

### CONDITION
conditions apply filters to individual data items in a sequence 
they take exactly one input and produce exactly one output

the output sequence contains SOME OF the original input sequence 
- items that meet the condition are passed along UNCHANGED

similar to a transform, condition is applied immediately when the node receives input, and items are passed down the line as soon as they are found to meet criteria

the filtered sequence terminates as soon as the original sequence terminates for any reason

the criteria of the condition operator can be specified using a node group
- the input is the unfiltered sequence and the output is a sequence of bool elements (true or false) depending on if the current item matches the criteria or not

### SINK
sinks apply a function to every individual element of a sequence, BUT the sink does not alter or modify the input in any way
the output sequence is the exact same as the input sequence

sinks are used to save data or trigger an external output or some other side effect with the data produced in bonsai
a sink is how bonsai communicates with an external function, be it saving the data externally or moving / changing something outside of bonsai

because the input and output of a sink is always the same, a sink can be placed at any point of a workflow without breaking the existing workflow

multiple sinks can be chained, so long as the input is compatible with all of them (ie they all need to take the same kind of input because the data isnt changed when passing through a sink)
convenient when multiple things need to be triggered by the same data stream
- ie save data to a file and simultaneously transmit the data to an external device

### COMBINATOR
combinators group together all of the more complex types of operator, but the behavior is very diverse in the group

examples
- merge data from multiple sources
- control when sequences start and stop
- dynamically create new sequences

an incredibly flexible toolkit
## property mapping 
each bonsai operator has a set of configuration properties that allow you to parameterize (describe in terms of numerical factors) the behavior of the operator 

these parameters can be configured manually in the properties panel 
BUT
what if you need to map the properties of an operator dynamically based on the output of other observable sequences

how would you change the volume of an audio file dynamically based on the position of the cursor?
- property mapping!

Property mapping operators 
- take a single input sequence 
- THEN react to the input by changing the PROPERTY VALUES in a SUBSEQUENT node

three types of property mapping operators
- externalized mapping (externalized mapping node)
	- externalizes one or more operator properties 
	- ext. properties can be named and will show up in the properties panel for node groups
- mapping a sequence to a property (property mapping node)
	- mapping multiple properties simultaneously
	- individual members of input data can be mapped to DIFFERENT PROPERTIES in the target node
- mapping properties simultaneously (input mapping node)
	- maps multiple properties synchronized with input notifications
	- same as property mapping node BUT property changes are only applied when a notification is transmitted to the target node

### externalized properties
ExternalixedMapping - operator creates externalized properties
you can externalize multiple properties from the same node

NOTE - all externalized properties in the same workflow must have DIFFERENT NAMES
externalizing multiple conflicting properties? use DisplayName property to give them all unique names

when ext properties are nested in an operator group they will be shown as member properties of the node group itself
- when the group node (folder of nodes) is selected, all named externalized properties will show up in the properties panel for that node group

### mapping a sequence to a property
after a property has been externalized, you can connect any sequence to the mapping node SO LONG AS the the output of the sequence is a data type compatible with the property

when you do that, any time the property source sequence emits new data, the mapping operator will take that data and use it as the value of the mapped property
- ie the output of the mapping sequence is used as the input for the externalized property

DYNAMICALLY CHANGES THE PROPERTIES OF SEQUENCES BASED ON OTHER SEQUENCES IN THE WORKFLOW

the connection between the property mapping and the target node only affects the properties NOT the function of the workflow 
the behavior of the target operator is unchanged EXCEPT for the changed property/properties
(dashed line instead of solid line when connecting in bonsai)

[[2-12-2025-Wed]]
NOTE - property values can change even while the target operator (operator with the externalized properties) is reacting to notifications from other nodes

care must be taken to ensure that changing the property state like this doesnt break the workflow

SPECIFICALLY some operators respond to parameter changes only at specific moments
- parameters of a timer node must be set before the sequence is initialized 
- the input to the externalized property MUST be emitted immediately for the mapping to work (since the timer value must be in asap)

### mapping multiple properties
the PropertyMapping operator can simultaneously map multiple properties from the same source sequence

select properties to map using the editors in the property grid
each mapped property needs a specific source selector (an expression that specifying which members of the input data type are used to assign values to the mapped property)

NOTE 
- if the selected member from the input does not match the type needed for the property, a conversion is attempted
- if no compatible conversion is found, bonsai tries to construct the required value type for the property from the other members of the input

PropertyMapping operators can be connected to multiple target nodes

the properties tied to a single PropertyMapping operator are simultaneously updated when the source sequence sends out a new value

### Mapping properties synchronously
sometimes you need to synchronize property updates with data flow (ie property mapping operator needs to change the property value ONLY when the source sequence emits notifications)

InputMapping operator allows you to synchronize property updates with input notifications 

InputMapping fundamentally works the same as PropertyMapping, but now the connection from the mapping operator to the target node (node with the properties that are being mapped) is done through upstream sources

What does that mean?
- only values from an upstream source sequence can be used to map properties in a target node
HOWEVER you can specify which specific member of the original data source should be used as property input to the target node using the Selector property

whenever the input sequence sends out new data, all specified property mappings will update at the same time BEFORE the data item is passed down steam to hit the target node

this insures that no property changes occur between the upstream notifications 

Example
- a transform operator converts a source sequence between different formats
- the output format is given by a set of operator properties
- the target format needs to change dynamically BUT you also need to guarantee that the format specs don't change while the operator is converting input 
	- ie the output function is a property of the transform and it can't change MID transformation, we only want it to change at specified times
	- SO it must be synchronized with the output of a given upstream operator

## higher order operators
Sometimes you need to deal with a system with an unknown number of sources

example - you want to merge together several video files
- if you knew the number of source files ahead of time, you could use a Concat operator 
- BUT what if you don't know beforehand how many files you want to combine AND you want to merge all the videos without needing to manually place a source node for every file?

Start with an EnumerateFiles source
- this operator creates and OS that emits all of the file names in a specified folder one after another

if you wanted to merge all of these manually you would need to create a different FileCapture source for every file name emitted and then pass all of these sources to a Concat to merge all of the frames into a single sequence

whenever an operator receives or emits a sequence of sequences (like EnumerateFiles) we call it a **higher-order operator** 
these HOOs are particularly powerful in bonsai
### higher-order workflows
higher order operators are represented as nodes in the workflow
However, some allow you to specify their behavior using node groups, which allows you to program how the sequences created in the HOO behave using other nodes

an HOO is like a loop, you can take an unknown number of inputs, do the same thing to all of them and then send them out to a single downstream node

in the example of combining an unknown number of videos -
- use a HOO to take the files from EnumerateFiles
- assign the filename as an externalized property of FIleCapture, and have the filename property update to match the current file pulled by EnumerateFiles
- THEN have FileCapture output to Concat + a VideoWriter sink

HOO show up as a CreateObservable node - with an expanded window to show its contents
- the input is Source1 + specified from the upstream node
- the output is WorkflowOutput and leads directly into the following downstream node

NOTE 
CreateObservable creates new sequences for every input notification BUT it doesn't automatically subscribe to them 
You need another higher order operator (something that can take a sequence of sequences as input) to subscribe to the output sequences of CreateObservable for them to be passed along 

you make a sequence of sequences with CreateObservable and then you condense it to a single sequence using Concat

## subjects
subjects are a special type of operator that allow for the reusing and sharing of observable sequences

a subject is a bridge or proxy, it subscribes to an observable sequence and passes all the items it receives to multiple down stream operators 
this allows multiple downstream operators to share a single subscription to the source sequence

most subjects are given a name 
you can subscribe to a named subject from anywhere in the workflow using the SubscribeSubject operator - making subjects very useful to organize complex workflows into modular components
- you can change the subject in the workflow and then call it and not need to rewrite that section of the workflow each time you want to call it

subjects also control the temperature of a shared sequence
- convert a sequence from cold to hot using PublishSubject
- convert a sequence from hot to cold using ReplaySubject
### scope of subjects
[[2-13-2025-Thu]]

subjects can be access in the same workflow where they were defined or inside any workflows nested inside operators that are defined at that level

HOWEVER if a nested operator defines their own local closed scope and the subject is declared inside of that, it will NOT be accessible outside of the nested operator where it was defined

a node group with a dashed border means a subject is accessible outside of it, a node group with a solid border means a subject defined inside will NOT be accessible outside of it

if node groups are used to define higher order observable sequences any subjects defined inside will be unique to each created sequence
- ie subjects defined inside of loops are unique
### branching subjects
branching subjects define a PublishSubject

all branches are subscribed to the subject AND THEN subscribe to the common source sequence
- this guarantees that every value is delivered to all branches, assuming its given immediate subscription

NOTE
- dangling branches operate independently from each other and independently from the subscription to the source sequence
- if one branch terminates and then resubscribes to the source while other branches keep going this DOES NOT reinitialize the shared subscription to the source
- if you want it to reinitialize a shared subscription to the source you need to merge all branches figure out cancellation and re subscription down stream from the merge point

### source subjects
subjects can be declared as a sink from an existing observable sequence or as a source

source subjects do not have a pre existing input where values are generated from. INSTEAD they are a set up to redirect inputs from multiple writers into one reader, for logging or control purposes

if subjects are created as a source the type of the subject needs to be declared explicitly ON CREATION
- select the source sequence in the workflow whose type you would like to share and then right click

### subject types
there are different subjects with different purposes and uses
each subject operator has its own symbol to identify the type of subject it is

#### AsyncSubject
- stores and passes the last value, and ONLY the last value, emitted by a source sequence to each subscribed observer
- the value is only sent out after the source sequence terminates
- if the source terminates without emitting any values, the subject will terminate without emitting any values

you can use the Take operator before AsyncSubject to store the first value from an infinite sequence

any observers that subscribe after the source sequence terminates will immediately receive the stored value
if the source sequence terminates with an error the AsyncSubject will not emit any values, but will pass down an error notification

#### BehaviorSubject
stores and passes the latest value emitted by the source sequence and THEN continues to emit any subsequent values

any observers that subscribe later will immediately receive the latest stored value

HOWEVER if the source sequence terminates with an error, the subject does not submit any values, but passes along an error notification to all observers

NOTE - BehaviorSubject is designed to multicast + share updates from multiple sources. If one of the source sequences emitting values to BehaviorSubject terminates successfully, the BehaviorSubject will not send a termination message. BehaviorSubject only closes when the whole workflow closes, in order to give any sources feeding into it a change to update the shared state

#### PublishSubject
PublishSubject only passes values to a subscriber that are emitted AFTER the time of subscription

if a subscriber joins late, it will lose data published before it subscribed
If you need all values, make sure everything is subscribed upon workflow initiation.
if subscription upon initialization isnt possible, use Replay or Async (for multiple or a single value, respectively)

terminates with error = no items to subsequent subscribers, just the error message

turns something into a hot data sequence

#### ReplaySubject
ReplaySubject passes on all emitted values to every subscriber, no matter when they subscribe

can be set to throw out old values after a period of time, if that would be desirable

turns something into a cold data sequence

#### ResourceSubject 
ResourceSubject stores and passes the single last value emitted on termination of the source data flow. If the source emits no values, ResourceSubject also emits no values

NOTE - the type of stored value must be IDisposable - meaning when the workflow is terminated the value will be disposed of to free up any resources allocated to it

subscribers that join after termination receive the stored value
source terminates with error = no values emitted, error message passed along

#### SubscribeSubject
SubscribeSubject works as a source that accesses a named subject and subscribes to it 
behavior is defined by the type of subject it is accessing
values from the underlying sequence are passed to operators downstream of SubscribeSubject as if they were directly connected to the subject in question

#### MulticastSubject
MulticastSubject works like a sink that accesses the subject with a specific name and forwards upstream values to the called out subject
depending on the behavior of the subject these values will then be passed to any operators subscribed to the subject, including termination and error notifications

(lets you feed other values into a subject to be passed down, depending on the subject)