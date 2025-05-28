# FedID WG Telecon — DC API Series B, 2025-05-28

* Moderators: Heather Flanagan, Wendy Seltzer

* Scribe: Wendy, Heather

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?   
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * Upcoming meeting schedule  
    * summer meetings  
    * meeting during IETF 123  
* Ecosystem Updates (5 minutes)  
* DC API PRs (10 minutes each)  
  * [Link to registery inclusion criteria definitions \#236](https://github.com/w3c-fedid/digital-credentials/pull/236)  
  * [Fix links to request field to use the new format in the register inclusion criteria \#235](https://github.com/w3c-fedid/digital-credentials/pull/235)  
  * [Add isProtocolSupportedByClient static method \#221](https://github.com/w3c-fedid/digital-credentials/pull/221)  
* DC API Issues (10 minutes each)  
  * [\[spec\] write privacy considerations \#183](https://github.com/w3c-fedid/digital-credentials/issues/183)  
  * [Add isProtocolSupportedByClient static method \#219](https://github.com/w3c-fedid/digital-credentials/issues/219)  
* Any Other Business (AOB)

# Notes

* 

## Administrivia

* Heather: Reminders, group membership, code of conduct  
* Upcoming meeting schedule. Calendar shows upcoming cancellations for n. Hemisphere summer. We’re still looking for a host in Madrid alongside IETF, otherwise we’ll hold a longer virtual meeting without the f2f option. 

## Ecosystem Updates

\[none\]

## DC API PRs (10 minutes each)

### [Link to registry inclusion criteria definitions \#236](https://github.com/w3c-fedid/digital-credentials/pull/236)

* Marcos: This looks like editorial, respec changes. We should mark it as such.   
* Tim: We didn’t’ discuss whether we can merge editorial changes without call  
* Marcos: I’d think that’s ok  
* Marcos: I can fix and merge

### [Fix links to request field to use the new format in the register inclusion criteria \#235](https://github.com/w3c-fedid/digital-credentials/pull/235)

* Tim: adds links, splits the text for presentation and issuance.   
* Marcos: ok

### [Add isProtocolSupportedByClient static method \#221](https://github.com/w3c-fedid/digital-credentials/pull/221)

* Heather: combo issue 219, PR 221\. We spent a long time discussing the last call. Anything that’s changed?   
* Tim: Nick’s concern should be resolved because he wrote the text. But still debate over core structure.   
* Tim: bulk of the discussion was at F2F.   
* Marcos; I still have the same concerns about supported  
* Tim: if it’s the method name, we can change that  
* Marcos: Also whether it should be a static list.   
* PLH: return method is boolean. Does it guarantee that options will be supported? In HTML, re video format support, there’s a 3-state answer: yes, no, may \- support. Is this case similar?  
* Tim: all this means is that the user agent understands the request enough to pass it on  
* Marcos: unclear why it’s promise-based then  
* Matt: Intent behind this, so UA can make an implementation choice, e.g. always return yes, or introspect and then return true or false. Thinking about how a developer may wish to discover which protocol to use. Versus trying to understand what asterisk means. I support a method, and think the semantics are more developer-friendly.   
* Marcos: That's different from the original intent of this list, which was to ask “does the browser know about this registry entry”.  Poking around is a privacy leak. This can only answer, e.g. “do I know about mdoc”  
* Tim: That's all this does. We can change away from promise if that helps  
* Marcos: then why do we need a method, just make it a list  
* Matt: Adding a list introduces a magic value that’s not seen in other APIs.   
* Johann: What does a developer do, they search for the protocol they’re trying to use  
* Marcos: It’s answering “I know about this registry types”  
* Tim: This proposal doesn’t talk about the registry. The original intent was “the user agent understands the request enough to pass it on”  
* Helen: I thought the point was what is allowed to pass through, not a registry method  
* Marcos: if it’s not in the registry, it’s not in the list  
* Helen: there will be protocols not in the registry. Devs want this so they know if it will work, and can fall back early on  
* Heather: We’re talking about 2 separate things, can we separate them to talk about? If chrome can’t do a list, and we’re trying to get something all browsers can use, can all use a method?   
* Marcos: Given that webkit knows ahead of time what protocols it supports, I can say that. Also question how we do filtering.   
* Matt: question whether it’s promise-based, and name are details. Can we agree that this method can satisfy greatest number of verifiers, browsers,   
* Tim: “Can requests with this protocol reach wallets,” is the purpose of this issue/PR. That’s the intent. That’s all you can disclose safely   
* Marcos: Can potentially reach wallet  
* Marcos: if it’s going to be promise-based, I need a really good reason. Start with it not being promise-based, then see if that works.   
* Heather: so not promise-based, using a method, as that would work for most browser engines  
* Tim: make it static.  
* Matt: I want to say that in JS-land, it’s easier to go from async to sync than vice versa. I suggest we start async, so as not to need messy changes later.   
* Marcos: couldn’t that apply to any method?  
* Matt: We could ask the UAs to take that on, and make it easier for a larger group. Or force changes later  
* Marcos: we’ll get that feedback soon, as browser engines work to implement. As the webkit implementer, it doesn’t appear to me to need to be promise-based. I look forward to hearing from the chrome team. Give us a week to experiment  
* Tim: at the end, we’re creating such a specific method name and if it needs to change, we need a new method.   
* Heather, that covers issue 219 as well. Let’s move on to privacy

## DC API Issues (10 minutes each)

### [\[spec\] write privacy considerations \#183](https://github.com/w3c-fedid/digital-credentials/issues/183)

* \[scribe switch\]  
* (Johann) Still fairly new to this work and coming into this as something of an outside observer to consider the privacy considerations. There’s still a lot to learn\! Have been having some useful conversations to structure the privacy considerations for this space. Has created a handful of issues so far. I want to call out in particular the scope of privacy considerations. When we talk about the general topic of Digital Credentials, it tends to be a very, very broad picture, which isn’t really what we want to cover for the specifics of this spec. There does need to be that broad discussion, but we have to have a balance between what’s useful for the spec and is a full consideration of privacy issues relevant to the API, and also having an outlook towards what we can do in the future (e.g., eIDAS verifier certificate methods as they get more defined). That latter thing we can’t produce in four weeks, but we can probably get the immediate issues documented.   
* (Wendy) to help set the stage on this, we sent out a call for consensus to publish the FPWD and we heard strong objections to publish as-is because people want to see more published on the privacy considerations first. Appreciate Johann’s willingness to help. The four-week timeline is not a timeline for the final privacy considerations; it’s what’s to be enough for the FPWD.  
* (Johann) talking to the people who raised the objections, they want a genuine attempt to get the issues specific to this API and not the issues with the whole space. If they see more direct guidance and less generic input, that’s ideal. So, please look at the issues and comments (see GitHub tag “[privacyconsiderations](https://github.com/w3c-fedid/digital-credentials/issues?q=state%3Aopen%20label%3A%22privacy-considerations%22)”). The particular issue of discouraging inappropriate uses of the API is interesting; people have different criteria for what is “good” or “bad” uses for this API. We should allow frameworks created that would be mediated by the API to let entities define what are and are not valid use cases. Some people say the browser should have an opinion from the start on that, others are saying it should be the responsibility of the wallet.  
* (Tim) This is why I’m frustrated. The API decisions were based on consensus, and now we’re revisiting all those decisions because of the privacy consideration blocker. The browser gets the user consent and the wallet decides whether to handle the request is what we’ve been building on so far.  
* (Johann) Elaborate, please  
* (Tim) Half the people want it one way, the other half wants it like how WebAuthn is designed. It’s a dumb pipe that allows requests to flow down to the platform; the user agent can collect permission, but the wallet is the second user agent and that’s what’s takes over. So much of what’s going in the spec can’t be enforced by the API and probably can’t be enforced by the web platform either.   
* (Johann) There are several people who will disagree and possibly formally object to the concept of treating this like a dumb pipe. If we want to write that down, that’s fine and will bring that perspective to the conversations again. What is the deadline in question?  
* (Tim) OpenID4VP needs to reference this by June 30; that’s when the EU implementing acts will point to this. If we’re not able to meet that date, we’re going to lose several years and see many worse implementations using things like custom schemes.  
* (Johann) The idea of immediately delegating any request to the wallet, I don’t think there’s consensus with the participants in the group about that (based on the conversations on that).   
* (Marcos) Disagree with Johann on that. Arbitrary deadlines from random organizations shouldn’t influence this so much; we can push back on the deadlines. Better to get it right.  
* (Tim) None of the text changes the ergonomics of the API; it’s informative.  
* (Marcos) That’s not necessarily true. We’re supposed to learn from the privacy considerations and potentially change the API as a result.  
* (Johann) if we put anything in the privacy considerations, people will think we’re not taking it seriously. If we’re so sure that doing this as a dumb pipe is right, then we should have a reasonable explanation in the privacy considerations.   
* (Brian) We’re not in a position to tell the EU to move their deadline. They may seem arbitrary, but they are very real and we’re trying to put something forward that’s better than the status quo and what will be written into the laws.  
* (Johann) I’m not trying to block the FPWD publication. I’m just trying to help improve the privacy considerations section. If publishing is worth more than a privacy consideration section that’s in better shape, then do it.  
* (Wendy) What inspired the W3C team to join today? If you have thoughts on how to proceed through the strong objections to publishing a FPWD and the strong time pressures, would love to hear it.  
* (Philippe) Main goal is to listen today. We are not going to go around the requirements of the W3C process for the sake of an EU deadline.  
* (Tim) Not asking the W3C to change its policy. Where I am very nervous, if we finish this by June 25, people who weren’t participating in the discussion will block it at the last minute again. Worried Johann will do three weeks of work and we’ll still end up in the same situation for the next 3-5 years.  
* (Johann) I get the position; it would be more defendable if we had a privacy consideration section written at this point.   
* (Tim) what is in the spec now was considered good enough for FPWD according to the community group.  
* (Marcos) It’s important to take the larger perspective; we’re not in a mess. It’s a larger 10-year project, and this is a bump along the way. A few weeks won’t buy us much in the grand scheme of things. This is a different group now, and so the WICG consensus doesn’t really apply.   
* (Wendy) So we can help Johann by making sure has feedback ASAP.

### [Add isProtocolSupportedByClient static method \#219](https://github.com/w3c-fedid/digital-credentials/issues/219)

* Covered under discussion of PR 221

## 

## Any Other Business (AOB)

# 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting)  
* Matthew Miller (Cisco)  
* Philippe Le Hegaret (W3C)  
* Simone Onofri (W3C)  
* Wendy Seltzer  
* Ketan Mehta  
* Tim Cappalli  
* Marcos Caceres  
* Johann Hoffmann  
* Helen Qin  
* Ketan Mehta  
* Hannah Gould (GitHub)  
* Brian Campbell