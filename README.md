# neath
Neath is a project to create new UI languages, frameworks, primitives, etc. that can transcend the web UI that's most prevalent today. Its main intention is to develop a way to build UI for Urbit apps (and eventually the base OS) that is more native to Urbit itself and hopefully cross-platform. 

## together
Something like neath is an extremely large undertaking. It's so large that it's difficult to even pick angle to start from. The hope here is that a loose group of people can come together to start driving development on this enormous task and help each other get started.

Sometimes you need others working on the same idea to motivate you to get started and really develop useful new paradigms. Neath wants to achieve this by becoming a UI working group.

## areas of work
- graphics rendering and drawing instructions
- UI expression and ergonomics
- state management and mapping data to UI
- accessibility and performance

## avenues & decisions
Some potential avenues and starting points include:
- a way to dynamically distribute Javascript components for other hoon apps to consume and use
- a UI kit that hoon data structures can map to for semi-automated UI creation
- a dialect of hoon or a new language that compiles to hoon which spits out some intermediate format for UI platforms to interpret
- developing a UI vane which works with the runtime to draw graphics on the host OS

Some decisions have to be made around where UI creation and rendering actually happen, however, everyone can make different choices. 
- Should we send UI over the wire in a sort of "server-side-rendered" fashion? 
- Should someone need to run Urbit locally and actually interact directly while syncing state to a remote Urbit?
- Should we have some sort of separate "client" that is able to render instructions sent from a hoon app?
- How should state be handled? Should UI state be separate from gall state? Is there a syncing mechanism?

## first step
For those that are interested we should start meeting informally and regularly. It would be great to come up with some achievable goals and get a sense of what talents we have amongst us. I think there are enough of us that we can come up with a few ways to start making progress on the project.

I intend this repository to act as a sort of haven for work in this realm. Each of us can contribute whether that's through writing, prototyping, or just providing commentary. We should all feel comfortable to share half-baked ideas, barely working prototypes, and genuinely embody the spirit of experimenting.

## structure
The project is structured as follows:

- **notes**: a folder which contains writings from various contributors
	- **your-name**: a folder of your personal writings which you would like to keep separate
	- **topic**: a folder concerned with a specific topic, the files within should be descriptively named
- **proto**: a folder of code for the development and generation of UI
	- **name**: projects within proto should be self-contained and named appropriately. each one will likely have a different structure based on what problems it's solving
- **meetings**: a folder containing the record of meetings that we have
	- **meeting-name-2022.08.04.md**: files labelled by date should represent notes taken for a specific meeting
	- **index.md**: a file explaining what meetings are ongoing and the links to their respective calendar invites.
- **CODE_OF_CONDUCT.md**: a file explaining what behavior will or will not be tolerated
- **CONTRIBUTING.md**: describes the practices around how contributions should be made and in what format, etc.
- **LICENSE**: the license for all works contained within, at this time it will be *MIT* unless we agree on something else
- **README.md**: this file which acts as a general overview for the project

## home
The main source of communication around the project should be the [holy grail ui](web+urbitgraph://group/~nocsyx-lassul/holy-grail-ui) group on urbit.
