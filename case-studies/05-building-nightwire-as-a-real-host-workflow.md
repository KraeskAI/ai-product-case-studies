# Case Study 05: Building Nightwire Around the Host's Actual Workflow

**Status:** Working host application with a separate experimental Beta; not a claim that every broadcast or camera feature is production-accepted. Evidence reviewed through November 2026.

## The problem

Hosting community Listening Parties and After Parties meant juggling song links, order, attribution, lyrics, announcements, media playback, discussion pauses, and broadcast presentation across several applications. The tools could each perform a piece of the job, but the host remained the integration layer.

I set out to design one local-first Windows workspace that would make the host's next action clear and keep the audience view distinct from operational controls.

The resulting application, originally named Theatre and now **Nightwire**, grew into a real software product with a Control Desk, an audience-facing stage, native desktop integration, and hardware control support.

## The product decisions

The central challenge was not adding controls. It was deciding what those controls must mean while someone is running a live show.

- **Different shows require different transitions.** A Listening Party pauses after a finished song so people can discuss it; an After Party moves automatically to the next song. The same player needs different semantics depending on the hosting context.
- **The Desk and the audience stage are different products.** Hosts need imports, transport, scene selection, recovery, and errors. Listeners need a legible performance display, not a mirrored control panel.
- **Real playback state matters.** A button that changes appearance while audio keeps playing is not a functioning Pause button. I required the control to reflect actual playback, including recovery, retry, and end-of-track behavior.
- **The live queue is not a disposable list.** Importing into a populated show must distinguish append from replacement, preserve the on-air item, and handle missing or delayed metadata without silently corrupting ordering.
- **Operational controls must fit the real space.** A one-screen Control Desk with persistent transport and bounded scrolling is more useful during a show than a theoretically flexible page requiring the host to hunt for essential controls.
- **Hardware controls need one source of truth.** The Stream Dock actions must address the same state and commands as the Desk, rather than becoming a second implementation of playback logic.

## What changed through testing

This project is a prolonged loop of observation, explicit acceptance criteria, implementation, and rejection of plausible but inadequate results.

Examples include identifying import cases where a held link resolved successfully but was appended to the bottom instead of returning to its intended position; detecting apparently responsive controls that did not correspond to real media state; iterating on a music visualizer where movement looked attractive but did not convincingly correspond to low, mid, and high-frequency content; and separating a frozen Stable installation from an experimental Beta so development could proceed without silently rebuilding the live show version.

Nightwire integrates Suno and YouTube workflows, saved scenes and host messages, a Stream Dock plugin, and experimental local broadcast audio. More ambitious native camera and receiver paths remain subject to real-device and audience-side acceptance. The current README explicitly distinguishes tracked implementation from verified real-world broadcast behavior.

## My contribution

I originated the host workflow and directed its evolution. My contributions include:

- Defining the use cases, operating modes, UI structure, and prioritization.
- Converting observed hosting problems into product requirements and acceptance criteria.
- Directing multiple AI coding agents and reviewing their output against actual behavior.
- Rejecting shortcuts that preserved an attractive interface while leaving host semantics incorrect.
- Establishing the Stable/Beta separation and the need for crash recovery, cold-relaunch, and live-device acceptance before promotion.
- Integrating community and creative requirements without treating every feature suggestion as approved scope.

AI agents produced much of the implementation, tests, and technical research. I am not claiming to have independently programmed the Windows application or its integrations.

## Outcome and limits

Nightwire has a usable host-facing application and an active Beta with additional functionality under evaluation. It is not accurate to present all native audio, camera, or Discord-receiver behaviors as finally accepted. Some issues remain under investigation.

**What this demonstrates:** AI-assisted product ownership, operational UX design, complex requirements management, multi-agent technical direction, integration judgment, live-workflow testing, and the discipline to distinguish a working candidate from a verified release.

The central lesson: the interface is not the product. The product is whether the host can confidently run the show without becoming the glue between incompatible tools.
