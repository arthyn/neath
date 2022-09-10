# neat, tidy, bord, et al

# The Dream

The dream is to write Urbit apps with UIs which

- are fully reactive and fully composable
- are composable with other app UIs
- are type-safe
- can be cross platform

The dream is to do this without

- writing html, js, or css
- thinking about scries, pokes, or subscriptions between agent and UI
- thinking about reactivity any more than absolutely necessary

For more, see “UI and the Path Forward” in the musings notebook.

# The Proof of Concept

The dream is huge, and I don’t know the best way to tackle it, so I want to start with the smallest possible proof of concept. Right now, I’m thinking that means a demo app, and rudimentary versions of the various systems it needs to satisfy the requirements above.

Things to build

- `verb` - A library (possibly a hoon extension) which adds reactivity. This might not be necessary.
- `tidy` - A language for describing UI components. Compiles to verb/hoon/nock which produces a `neat` UI from state.
- `neat` - A standard for describing a UI.
- `%bord` - A `neat` client for the browser—a web app which renders the `neat` UI, feeds it events, and keeps state in sync with the mothership (possibly using `mira`).
- `mira` - A system running in the `neat` client (`%bord`, in our case) and on the mothership that keeps agent state in sync. This might not be necessary for the POC.
- `%status` - A dead-simple demo app for posting a text status and reading the text statuses of your pals.
- perhaps another dead-simple app to demonstrate composing components from different apps

# The Demo App - %status

## UI Elements

- text input for your status
- button to submit your status
- text: your @p and current status
- list of text: your pals and their statuses
- containers with layout such that it looks ok

## Behavior

- the button is disabled if text is too long
- pressing the button updates the agent state status
- updates to the status are displayed right away
- pal updates appear promptly without refreshing the page
- blank statuses show “status unknown”

# The Tools

## verb (like reverberation, a (k)nock in motion)

An extension of hoon, or maybe just a library, for reactivity. This might not even be necessary, but it seems like it would be helpful for keeping components up-to-date at the very least.

## tidy (like neat)

A language to make writing UI components easy and powerful. Membrane by Adrian Smith will be a good guide/starting point, I think.

All components will be ultimately be variations/elaborations on the most basic component, so everything from text to an input box to a text editor to a word processor app should be equally inspectable, customizable, and reusable.

`tidy` components are compiled to verb/hoon and are functions which return nouns, and those nouns have faces that are defined by the `neat` standard, and the `neat` client (`%bord`) knows how to render them.

An example: A component may provide a position and dimensions, but those could be provided in number of ways. You could say the width is 20px. Or you could say it’s half the container’s width. Or you could say it’s the smaller of 50px and half the container’s width, unless the component has focus, in which case it matches the height.

If we do this right, there should be lots of good defaults similar to basic HTML tags, but everything can be ripped apart and reassembled however you want, and you can make your own defaults and share them with others.

Make it easy to do something, possible to do anything, and possible to make anything easy.

## neat (like neath)

`neat` is just a standard for specifying a UI. It’s not a program you run. You use something like `tidy` to produce a `neat`-compliant noun, and then you pass it to a `neat` client like `%bord` to render. This part in particular is a huge undertaking, but ultimately we’d like to support everything imaginable so that you could use this as a UI framework, a game engine, or anything, really.

For the POC, we should keep it very simple. Colored rectangles, text, and maybe some sort of SVG support should be sufficient to get started. Graphics shaders, advanced layering, blend modes, audio mixer, haptic feedback, etc. can wait.

## %bord - the neat client for the browser (like a smorgasbord of delicious apps)

I’m imagining `%bord` will receive hoon or nock from the gall agent which includes code for rendering the `neat` UI, turning events into user intents, and turning those intents into effects (yes, stealing this from Membrane).

We run the code in a wasm nock interpreter (with jets?). We render the `neat` UI with straight HTML or maybe canvas or webGL. Mouse and keyboard events will be piped into the wasm client of course.

`%bord` is the glue between the `neat` UI and the browser, but it will likely also have some browser-like features of its own, such as handling links, opening tabs, hosting a debugger/inspector.

We also want to support running components of an app within components of other apps, but that may (or may not!) be out of scope for this POC.

## Syncing state - speculative further systems

As for making the effects get persisted in the mothership, and keeping the client updated, we have a few options:

- automatically send pokes and create subscriptions based on the user intents and what data the components ask for.
- do the above but also update the local state so we don’t have to wait for the mothership’s response before we update the UI
- run the same code in the client as on the mothership, so we can just change the state in the client and sync it back to the ship. Instead of sending a poke `%create-todo`, we’d just send a state diff saying a todo had been added. If we go whole hog on syncing state between nock environments, we should probably set up a replication service, which we could call `mira`

In any case, we’ll want to be automatically generating pokes and subscriptions for our app based on the user intent handlers.

### mari - helps you keep things tidy (like Marie Kondo)

On the mothership, automatically generates/handles pokes and subscriptions based on the intent→effects function you provide. On the client, automatically sends pokes etc. to update the ship and then update the UI with the latest state.

### mira - maintains illusion of one thing somewhere else (like a mirage or mirror)

A library which you use in the client and in your gall agent to make sure that you can keep state up to date automatically. Unlike `mari`, which sets up lots of specific endpoints to hit to do different things, `mira` directly syncs state between mothership and client. I think as Urbit matures we’ll see plenty of other cases where we want to sync state between ships and ship-likes.

This will ultimately require a delicate touch, but to start out we can just pass diffs around and in any conflict the mothership wins.

# The Plan

I had better finish my current grant before I put too much time into this, but I’m very interested in working on this when I get the chance. I’m not sure I’m exactly qualified to do any of this, having never written a language or a UI framework, but I’m excited to learn by doing, and hopefully anything I do can at least help other people understand the problem better.

If anyone feels inspired to help me with this, let’s talk. Depending on how many people want to work on this, and how much external interest there is, this could be a hobby project, a grant, a community project, or the primary focus of a Combine company (although I don’t know what the business model would look like).

In any case, I’ll be putting this document and anything related I come up with in the `neath` repo.

If anyone has ideas/feedback about how this should be approached, technical or logistical, I’m all ears. I doubt that I/we will get this right on the first try, but I’d like to get it as right as we can.

Thanks for reading,

~midlev-mindyr