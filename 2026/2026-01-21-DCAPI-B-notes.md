# FedID WG Telecon — DC API Series B, 2026-01-21

* Moderators: Heather Flanagan

* Scribe: Helen Qin

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia (5 minutes)  
  * Scribe volunteer?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/participants/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/20240318/)  
* Ecosystem Updates (10 minutes)  
* DC API Issues & PRs (45 minutes)  
  * [Define "prepare credential requests" algorithm](https://github.com/w3c-fedid/digital-credentials/pull/420)  
  * [Define "present credential requests" algorithm](https://github.com/w3c-fedid/digital-credentials/pull/419)  
  * [Change from Registry to Supported Protocols \#401](https://github.com/w3c-fedid/digital-credentials/pull/401)  
  * [Security Considerations: Structure and Introduction](https://github.com/w3c-fedid/digital-credentials/pull/424)  
  * [Security Considerations: Secure Context](https://github.com/w3c-fedid/digital-credentials/pull/426)  
* Any Other Business (AOB)   
  * [What protocols should a user agent implement? \#439](https://github.com/w3c-fedid/digital-credentials/issues/439)

# Notes 

## Administrivia

* Reminders:  
  * Working Group Membership  
  * W3C Code of Conduct

## Ecosystem Updates

* Marcos: WebKit bug fixes; tests.  
* Mozilla [making changes](https://bugzilla.mozilla.org/show_bug.cgi?id=2004828)  
* Joint protocol group: seem to head to Fido. DC API should stay as a pipe.

## DC API PRs and Issues

### [Define "prepare credential requests" algorithm](https://github.com/w3c-fedid/digital-credentials/pull/420) \#420

* Marcos: "prepare credential requests" algorithm defines:  
  * Browser parses, converts and / or validates the request  
  * Also added abort signal support for cancellation

### [Define "present credential requests" algorithm](https://github.com/w3c-fedid/digital-credentials/pull/419) \#419

* Marcos: "present credential requests" algorithm defines:  
  * Captures who owns the presentation UI  
  * Results of user behaviors   
  * High level, handles the user and wallet interactions   
  * Error handling. Wallet versus browser errors.  
  * Response propagation.  
* Marcos: The two algorithms together define the javascript side of logic.  
* Marcos: waiting for feedback. It will be nice to have Mozilla feedback too since they are actively implementing the Digital Credentials API. And prove cross-browser compatibility  
* Rick: thanks for putting this together  
* Marcos: great collaboration with Mohamed  
* Matt: It makes more sense to look at both algorithms as a whole thing. Review order also matters as present depends on target. Does it make sense for one (419) to target another (420)?  
* Marcos: yes it makes sense to look at prepare first  
* Helen: I still need to look into the details, but high-level what's the plan for talking about hybrid in this present algorithm?  
* Marcos: On the WebKit side there's no code that does that, it's up to the OS. So I've seen this as outside the scope of the browser API. It's not something as an implementor I have to deal with.  
* Helen: But chrome does. There are API bits which impact the hybrid flow.   
* Tim: This is why we shouldn't go beyond when the request leaves the browser. We can't bring hybrid interop into our spec. Even what is written in [420](https://github.com/w3c-fedid/digital-credentials/pull/420)/[421](https://github.com/w3c-fedid/digital-credentials/pull/421) goes further than it should into the platform.  
* Marcos: That's potentially true. It speaks to when an error is handled.  
* Tim: Could add mapping to error states, but it's hard to go beyond that. Right now Chrome does hybrid on Mac and Windows for this but may not always.  
* John: I agree we should have a clean handoff to the platform. If the platform decides to go back to the browser for some aspects of hybrid that should be a separate issue outside DC API.  
* Heather: It's not part of the spec, right?  
* Marcos / John: Right  
* Heather: A couple more people need to look at this and take a finer look at whether too much of the platform impl is making it in here.  
* Tim: Might be worth a call just to talk about this to dig deeper. 

### [Change from Registry to Supported Protocols \#401](https://github.com/w3c-fedid/digital-credentials/pull/401)

* Heather summarizing the context:  
  * Discussed in series A heavily whether the word supported should be used or not  
  * Captured in the notes. Mohamed seemed to initially not be a fan but then turned around  
* Tim: I just updated the PR to just mention protocols  
* Marcos: Heading is protocols but there is still text talking about supported protocols right?  
* Tim: Why does this matter?  
* Marcos: You should get support for all the protocols but must get at least one.   
* Tim: Valid string as input to the API to get whether it’s supported by the API  
* Marcos: It’s fine to have supported. But it’s also important to get consensus that all agent must support at least one  
* Tim: Yeah, that’s a different issue though.  
* Matt: Referenced instead of supported?  
* Tim: Limited?   
* John: We could say “define the use of” or something like that?  
* Heather: Heard the concern about “supported” and how it may be interpreted differently. In the sense of what protocols does this spec cover, it's pretty clear if we scope the text to this API.  
* Tim: The current text already does this  
* Marcos: The main concern is different people reading it. More clear to highlight that one thing will be supported by a user agent  
* Tim: not sure that solves the issue by mentioning an agent will support one.  
* Matt from chat: "Use of the following presentation and issuance protocols are defined by this specification"  
* John: Pattern from CTAP is that "features are supported" means they can be enabled or disabled.  
* Tim: …Which is the purpose of this API. It allows you to detect whether the browser allows this protocol or not  
* Tim: We still have unresolved comments and cannot resolve this  
* Marcos: Let’s set a deadline and try to resolve this by say the next 2 days. And review the new proposals  
* Heather: Proposed the deadline as next Monday. On Monday’s call, latest, we have to conclude this.  
* Wendy: \+1. Try to get async consensus as early as we can.  
* Matt: There’s a few new enums. Marcos wants to remove some notes around how enum is not referenced. Do we have another section of the spec where the enums are located?  
* Marcos: The Compatibility texts are going to be moved. But we are going to be explicitly using these enum values otherwise. Don’t think we need the enums — they are implementation details and not exposed to JS developers.  
* Matt: Clarify: they are not used in a way to restrict user agents ability to support values that are not in that list?  
* Marcos: No. Run through when there’s an unknown value. But also it only operates on DOM strings. It’s just a convenience.  
* Tim: My opinion is that it doesn’t hurt to add it as it adds a bit of value to the reader.  
* Marcos: It’s used and a real thing. It’s called differently  
* Tim: There’s an exact reason that we put this into webauthn. It’s fine, you can take it out, and add what you want to close the PR  
* Tim: I didn’t understand your comment around moving it to the API section. It already is?  
* Marcos: I thought it was in the protocol section. If it’s already in the API section it’s all good  
* Tim: It is  
* Tim: On Monday, can we merge it as we agree on the supported protocol name and fix this text?  
* Marcos: Agreed  
* Heather: Hearing no objections, that’s the plan

### [Security Considerations: Structure and Introduction](https://github.com/w3c-fedid/digital-credentials/pull/424) \#424

* Heather: Discussed in the series A call. Any new comments? Marcos?  
* Marcos: Been very heavily involved. Was helping Mohamed.   
* Heather: Tagging them as draft and not bringing them back until past the draft stage.  
* Marcos: Should ideally be shorter. Like one paragraph each at most.  
* 

### [Security Considerations: Secure Context](https://github.com/w3c-fedid/digital-credentials/pull/426) \#426

* 

## [https://github.com/w3c-fedid/digital-credentials/issues/439](https://github.com/w3c-fedid/digital-credentials/issues/439)

* Tim: Many members of this group think you should process all protocols and at minimum send them over across device  
* Marcos: Thought we had consensus. It’s impossible to require an agent to support all protocols.  
* Tim: Regardless, no reason why we can’t say it will always send it cross-platform. Doesn’t matter whether the other platform supports it.  
* Marcos: Putting the user at risk to process it  
* Tim: Not asking you to process it, but passing it  
* Marcos: we can’t randomly pass it to Android and put the user at risk  
* Matt: Why add the complexity to the spec the protocol preference of both the browser and the platform?  
* Marcos: Limitations put us down to a "should" level. Let’s keep working towards getting everything implemented.  
* Matt: "We" being the user agent or the platform?  
* Marcos: Both  
* Matt: But we are writing a spec for user agent  
* Marcos: User agents often influence the platform.  
* Matt: From a spec text perspective, we can just say pass everything through the platform.  
* Marcos: From a WebKit perspective, the platform doesn’t have the support for it yet, so I just can’t do it.  
* Rick: Implementations like Chrome, the browsers can choose not to use the platform. That’s what Chrome does on macOS. I don’t think it matters too much here. Through some other process we can change this from a should to a must.   
* John: Marcos, does the API that you’re given in Safari assume mdoc even if it’s going to be hybrid? Your interface to hybrid is restricted to mdoc only?  
* Marcos: Yes. It will only pass an mdoc request.   
* John: Acknowledging the reality is fine but concerned with UX. Processing the ux for formats that you don’t understand is going to be challenging.  
* 

## AOB

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting, co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Matthew Miller (Cisco)  
* Rick Byers (Google Chrome)  
* Wendy Seltzer  
* Helen Qin (Google Android)  
* Brian Campbell  
* Tim Cappalli  
* Bjorn Hjelm (Yubico)  
* John Bradley (Yubico)