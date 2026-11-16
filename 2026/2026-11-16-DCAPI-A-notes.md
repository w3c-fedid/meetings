# FedID WG Telecon — DC API Series A, 2026-11-16

* Moderators: Heather

* Scribe: Granola

Call-in details: see [https\://www\.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https\://www\.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?   
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
* Ecosystem Updates (10 minutes)  
* Discussing [approach](https://docs.google.com/document/d/1H-XVfw_vBwSa_ziPdEtZx4n1UgHwrg2CJW_kJs6jveM/edit?usp=sharing) to the open privacy issues  
* Any Other Business (AOB)

# Notes

## Administrivia

* Heather: Welcome

## Ecosystem Updates

* 

## DC API Issues & PRs (45 minutes)

### Discussing [approach](https://docs.google.com/document/d/1H-XVfw_vBwSa_ziPdEtZx4n1UgHwrg2CJW_kJs6jveM/edit?usp=sharing) to the open privacy issues

# **FedID WG \- DC API \- Series A (2026)**

Mon, 16 Nov 26

## **DC API Ecosystem Update**

* Apple shipped DC API support in Safari  
* Platform wallet onboarding remains “white glove”: vendors want to understand credential type and schema before allowing issuance  
  * Not a technical problem; a business/regulatory one  
  * Path forward: define schema, get global consensus via a standards group (e.g. FIDO)  
  * Third-party wallets are the practical short-term option for developers wanting to test end-to-end flows

## **Privacy Framework: Structure and Feedback**

* Heather drafted a working document (ChatGPT-assisted) to break the logjam on \~26 open privacy issues  
* Organized around 4 questions:  
  * What must the browser guarantee?  
  * What privacy properties are required of supported protocols?  
  * How do we handle linkability?  
  * What role should verifier-provided explanations play?  
* Goal: not just “DC API doesn’t make privacy worse,” but establishing meaningful protections where the group has real leverage  
* Key structural feedback from the group:  
  * Move Decision A (“what must the browser guarantee”) to the end: more fundamental credential questions should be settled first  
  * Move Decision D (verifier-provided explanations) after A: high risk of getting lost in the weeds; defer as long as possible  
  * Surface the proposed outcome more prominently in each section, with discussion questions below it  
* Vague line items flagged by Jim as “beyond actionability”:  
  * “Accommodation of user privacy choices”: likely meant selective disclosure; suggest replacing with “enablement of intended nondisclosure”  
  * “Prevention of unintended disclosure of credential availability”: distinct from deliberate nondisclosure; keep but clarify  
  * “Accurate transparent description of behavior”: interpreted as correct origin/DBA name display to users pre-ceremony  
* Broader architectural tension raised: the “dumb pipe” model (all privacy delegated to protocols) may not survive scrutiny  
  * Options: re-architect the API to do more, demand signals from other layers that required steps were completed, or do nothing (regulatory risk)  
  * Possible approach: require OpenID for VP (and similar) to signal that a consent dialog occurred, without prescribing its form  
  * Browser-side user preference for attribute disclosure (alert when a site requests sensitive attributes) floated but acknowledged as not fully formed  
* Tim’s counterpoint: implementers (browser vendors) bear their own regulatory risk; the WG may be over-indexing on its own accountability  
* European Commission Report B noted as dropping new requirements

## **Workshop Planning**

* Heather to convene a 90-minute+ working session with spec editors, Tara, Simone, and Nick before end of 2026  
* Goal: reach tentative agreement on proposed outcomes, assign spec text homework, then bring back to the full WG  
* Time zone split: \~3 US, 2-3 Europe, 1 Australia; Marcos (Apple) also needs to be looped in  
* No time zone locked yet; scheduling depends on responses

## **Next Steps**

* **Revise privacy framework document**Reorder sections (A last, D after A), promote proposed outcomes, and clarify vague line items per today's feedback.  
* **Schedule 90-min privacy workshop with spec editors, Tara, Simone, and Nick** (Heather)Target before end of 2026; poke Marcos for availability too.  
* **Upload meeting notes and transcript to GitHub** (Heather)To be done during the dispatch meeting later today.

## Any Other Business (AOB)

* **Block calendar for European Commission meeting on 3rd December at 3 PM CET** (Heather)Simone to send a calendar invitation; ensure it is structured as a two-way conversation, not a presentation.


# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* Matthew Miller (OneSpan)  
* Tim Cappalli (Okta)  
* Simone Onofri (W3C)  
* Bjorn Hjelm (Yubico)  
* Ryan Watkins (Mastercard)  
* René Léveillé (1Password)  
* Mohamed Amir Yosef (Google Chrome)  
* 

# Transcript

Meeting Title: FedID WG \- DC API \- Series A (2026)  
Date: Nov 16  
Meeting participants: Hlf

Transcript:  
Them: Really sucked.   
Me: Great. We have permission, we have recording. We have moving on. How fabulous. Okay. So That's sorted out. I don't need the TPACK schedule, we're done with TPACK now. I hope everybody is practicing their Spanish for our next TPACK meeting next year in December in Panama. Um, Do we have any ecosystem updates that we want to cover today? DC API out in the wild.   
Them: Apple shipped, Apple shipped AP support in Safari, so it's   
Me: Okay. Yeah.   
Them: Is there any— Is there any publicly available suggestions that, like, working with default platform wallets is going to become easier or like more generally available as a thing? Because right now, like, you have— it seems very hands-on if you want to try and issue something into one of these platform wallets. The platform vendors want to take like a white glove approach to onboarding you into the thing and like Are we— is anybody trying to move the needle in terms of like automating that to some degree so that anybody could issue, start issuing things into these wallets, or is it like third-party wallets? It's not, but it's not a technical problem, right? It's a business, business thing, right? Yeah. We technically don't officially support issuance, right? On the dSAFA. Officially.   
Me: I think to answer the question, since I don't— Matt, I don't think you're actually asking a technical question really.   
Them: So it's going to take time. Yeah. No.   
Me: I think the platforms are very hesitant right now to make it easier because there's still so many unknowns. The white glove approach, as you described it, I expect is going to be around for a good long time until we have some better Answers to. Questions around, around issuance and how that's going to look and what kind of regulations will be in place saying what has to work together, things like that.   
Them: All right. Still too early. Okay. Well, I mean, I think a slightly non-conflicting but different answer, right, is that the key is making sure the credential type and schema is understood, right? Like even the vendors who seem to be not interested in allowing generic issuance, let's call it, are interested if they understand what it's used for and what the schema is. So like, that's why the FIDO group has schema definition and scope. So if you have a use case Best thing you can do is write it down, get a schema with some kind of global consensus via a group, and that's step one usually.   
Me: Mm-hmm. Okay.   
Them: It's not like just generic, like file storage equivalent, save anything you want to. What is effectively a business app, it's probably a bit of a ways away. Fair enough. I don't necessarily— it's not blocking anything for me of just I'm just more curious, like, always picturing that future end state where, you know, these things are so ubiquitous that everything goes in them, and like, what is the path from here to there? Um, the— where we are right now is very Feels a little heavy-handed in how difficult.   
Me: Mm-hmm.   
Them: More potential use cases, even just like, even just as a solo, if I wanted to tinker around and like practice end-to-end flows for some library I'm writing or whatever, you know, like I cannot do that with platform libraries right now. Because I don't cross the— I don't, you know, I can't cross the bar. That has been set. So I guess, you know, there's third-party wallets or something is probably the answer for that in the short term. But in the long term, I assume kind of to Tim's point, or actually, I'm taking your point, Tim, that it's um, it's well, but, but I, but I think, I mean, in theory, You shouldn't have to cross. Over the platform API line, right? Like any conforming wallet that supports BCI. Well, assuming that they don't have a DOCTYPE filter, we'll accept it, right? So I don't think there's actually a fundamental difference with testing with issuing a multi-pass, for example, running on one of these devices through the same set of APIs. I think that gets you 99.8% of the way there anyway. I think a general purpose issuance library, I think is right. Yeah. But yeah, I mean, I think it's like if all these protocols are going to support the same limited set anyway, whether it's via DC API or not. It doesn't have to be the platform wallets, but okay. All right. Sorry, I didn't mean to turn this into a rabbit hole. So thanks.   
Me: No worries. It's actually a pretty good segue into our main topic of today, which is how we're approaching the privacy issues. One of the biggest challenges, of course, being getting consent, you know, Broad enough consensus on. The way I phrase it is where the liability sits. I think feeds into why can't you just put something in a platform wallet? Well, who ultimately is responsible for the safety of the user in that case? And that's not a totally settled question which gets us to today. Okay, so there's a link to a document I put together in the meeting agenda. And I wanted to really spend most of the time today talking about how we, how we're going to approach the remaining privacy issues, of which I believe there's like 26 still open, rather than going through the issues one by one. We have tried going through the issues one by one. That doesn't seem to work very well for us. The issues that we do have Ultimately cover very different kinds of concerns. Some are very clearly about browser behavior and things that the API can enforce directly. Others depend on presentation protocols and credential formats and wallets and what's happening in the broader ecosystem. And some are about user agency, consent, the potential for credentials to be used in ways that are technically permitted but harmful to users. And if we look at all of that individually, then we will continue to be pretty much where we are now, which is, feels a little bit like we're dead in the water. So here's what I did. I put together a working document to basically organize the conversation. I mean, full disclosure, I used ChatGPT to help with the initial analysis. I am not presenting this as authoritative. I'm just trying to break a logjam. So it's an attempt to identify the common themes, suggest where the different responsibilities might sit. And give us a starting point for deciding what needs to change in the specification and what requires coordination with other groups and what limitations we're going to need to acknowledge. So I've organized this around 4 big questions, right? What the browser needs to guarantee. What privacy properties we require of the supported protocols, how we handle linkability, and what role verifier-provided explanations should play, which is something we talked a bit about at TPAC. The document also proposes some, like, how we dispose of some of these issues. Specific specification language that might cover some of these things and the kinds of requests we might want to send to the OpenID Foundation or the Harmonized Working Group or what have you. I'm not asking us today to work on the proposals. I expect some of this is actually downright wrong or incomplete. What I need for you today before I have a larger workshop is to understand whether this was at all a useful activity for me to do and what needs to maybe change to get us closer to being able to dig in and solve it. Um, A broader question, uh, issue I want to keep in mind is I don't think our goal should simply be to demonstrate that the DC API doesn't make privacy worse. That's, that's such a sad bar to aim for, right? We're introducing a web platform mechanism. That makes digital credential presentation more accessible, which is great, and potentially much more common, which is unavoidable. And that creates an opportunity and a responsibility to establish actual useful privacy protections. Yay, go team\! So the API can't solve every problem in the credential ecosystem. We know this. That's why we have the layered diagram. But we need to be really careful to not use the architectural boundaries as our excuse to avoid addressing risks where we actually have leverage to say if something needs to change. So I think we do need to be really clear about what the browser can enforce what we can require of protocols that use the API and where we can establish expectations that will ultimately improve privacy even when the enforcement happens elsewhere. So our homework assignment for today is, does the framework I put together make sense as a way to organize this privacy work? Where is it incomplete, incorrect, or just missing important privacy concerns? And how do we make sure that the resulting specification that we're building has a meaningful commitment to user privacy? Rather than simply documenting the limits of our responsibility. That's what I want to do today. I don't know if we can get there, but I hope so. Matt Miller.   
Them: Um, so I think this is— this feels like a really good way to sort of break apart this whole privacy topic, which has felt incredibly complex to be like off-putting. But like, if these, you know, these buckets act First glance seem fine. The only thing I might suggest is, do the— are the decisions intended to be Like build on top of each other? Like, is A intended to be discussed first before B, C, D? Because if that's the case, then when I look at some of the later questions like linkability, Verifier provided explanations and privacy properties. Those seem like Those seem like issues that are somewhat independent of DC API, like any Deployment would sort of have to answer these at an individual implementation level as opposed to the more standards level. So do we need to have those discussions first before we go, okay, here's all of the like properties that we are requiring as a working group, and then we ask like how the browser can guarantee some of those things. Because we might come up with a list of things a browser must guarantee that, like, aren't going to have a meaningful impact on the implications of the later decisions. That was just sort of an initial thought I had based on how they were laid out. I haven't actually dove into the specifics beyond that.   
Me: I don't have— I'm not precious about the ordering, and honestly, I think they— all of the big picture ones tend to be so intertwined anyway that you can sort of start anywhere. And you're going to have to potentially iterate a little bit because as you've, you know, if we look at what the browser must guarantee to start, it's like, okay, we can come up with a proposal, but we'll have to stress test that against What privacy properties are required of the protocols, but we'll have to stress test it against linkability. We'll have to stress test it against the verifier-provided explanations. You know, I think we'll have to, to check all of them against each other.   
Them: It's kind of inevitable that you'll touch on all the other ones if you Start with A. I mean, I guess that's fine, but then that almost seems like decision A is like too broad or, or too encompassing, I guess, because like if that's the case, then like we don't need the other decisions. We just need to talk— start with decision A, and at that point we're kind of back to where we were with the beginning of The privacy discussion.   
Me: Mm-hmm. Mm-hmm. Okay. If we moved, if we moved that one down to the bottom of the list, do you think that would make the conversation easier?   
Them: Um, I, I Maybe that's all I'm really dancing around. So maybe that's my proposal. Let's move decision A, what must browser guarantee, down later in the list because there are seemingly more fundamental things about just digital credentials generally that we have to agree upon. Before we then go, okay, well, now how can the browser meaningfully You know, assert these guarantees about these things we've decided in our decisions.   
Me: Okay. Done.   
Them: Well, that was easy.   
Me: Other thoughts, comments, feedback?   
Them: I— so, sorry, no, go ahead. I didn't raise my hand. We need also a collegial team.   
Me: Mohammed, please.   
Them: Yes, sir. Yeah, so I love the split. Specifically because, you know, I cannot think of a better one or there is no alternative. So I mean, like, it's meaningful, I would say, but also the thing that I'm confused about is how to move from here. Like, should we, like, Agree on the proposed outcome for everyone first, and then everything will just fall apart from that part. Like, you know, linkability, that's not there. We should document it and then makes every single issue easy, or we should go through the issues. Like, what, like, what do you have in mind? Like how to go forward from here. This is the part that I'm a bit not clear about.   
Me: Sure, sure. Um, I mean, in Heather's ideal world, everybody is at this point familiar enough with the issues, the relevant issues that are captured there, that we can agree on, you know, the proposed outcome is the one we agree, and if we're not quite sure, we have some questions to chase around until we can say, yes, that proposed outcome is what we want, and then work back from there.   
Them: Because that would be interesting if we can get the whole group to agree on that outcome.   
Me: Yes.   
Them: I'm wondering what kind of discussion we'd have to reach, like, to agree in one line. Like, that's, you know, in   
Me: Mm-hmm.   
Them: But yeah.   
Me: Okay, so what I might do is something like is actually move, move the proposed outcome up. And then questions for discussion if we don't necessarily agree on the proposed outcome. Okay. Matt.   
Them: I guess I'll \+1 that idea of the proposed outcome getting highlighted more.   
Me: Mm-hmm.   
Them: Because, yeah, so the real reason I raised my hand is Decision D, though, what role should verifier-provided explanations play?   
Me: Mm-hmm.   
Them: Like, that I've been in many, in several conversations, including ones outside of this working group, where this whole idea of, like, WebAuthn has had this problem, like, how do you declare intent in a programmatic way without allowing arbitrary text, for example, and like no, I nobody ever really has seen. I have yet to see proposals. On how to get past that. The conversations always seem to kind of peter out, and it feels like the same thing is going to happen here. I don't think I have a solution to that. I just want to highlight that as something that we could end up like getting lost in the weeds and burning a lot of time on that exploration. So maybe we defer that as long as we can because we could maybe do that after, like, what must the browser guarantee? And we try to get most of our progress before that one because that could potentially drag things out.   
Me: Okay.   
Them: So maybe, maybe, maybe we move D after A. Because we know that the browser is going to have to guarantee some way for verifiers to indicate their intentions of using this data. But we move it down because we want to get all the progress on all this up first.   
Me: Mm-hmm. Okay.   
Them: Yeah.   
Me: This is super helpful. Other, other feedback? Jim, I know you actually got to look at some of this, and I agree, some of the statements are pretty darn vague. Are they, are they Big in a blocking way, or, you know, do we— how much do we need to clean that up before we have the, um, the longer meeting?   
Them: I mean, the ones I commented on, I think, were vague beyond actionability, right? Like, I mean, it was kind of like some of the responses we got from not-to-be-named government agencies. They, like, without a little bit more detail, it's just, I don't even know how to approach them.   
Me: Okay. Okay.   
Them: Like, what was one example, right? Like, Um,   
Me: Um, one example was accommodation of user privacy choices.   
Them: Like, yeah. Yeah, like, what does that mean? And I realize these are like some, these are obviously summaries and themes, but like, it's still It almost seems like there's a step missing of like, what should, what should the privacy choice be? Like the privacy choice, I guess back to like, it's already, it's being handled at other layers, right?   
Me: No. Right, I guess given, given the context in which that one is there, what the— you know, for me it's the— I looked at that as the user privacy choices in terms of what they've— what they have configured in their browser, but Because they've got to— I mean, if you say it's a user's choice, then Browser has to guarantee this is— these are your options. Don't know. Matt?   
Them: Was this like a layperson's description of selective disclosure? And like, that's why it seems so vague because Or maybe selective disclosure is too specific a way of accommodating user privacy choices. Uh, hmm, I guess I'm just thinking out loud. Like, it sounds very vague in the sense of like, perhaps in the discussion somebody was trying to talk about something like selective disclosure as a way for a user to indicate what they're comfortable disclosing. And in making it a little bit more broad because they didn't have that terminology, it ended up being this thing that sounds way, way more general purpose than what we need to actually talk about.   
Me: Mm-hmm.   
Them: But I wasn't in the room, so I don't know how the conversation went that might have led to that being added. I guess maybe that's just part of what we have to figure out, and we don't have to answer that right now.   
Me: Right, well, it's interesting that the selective disclosure bit was More captured in the linkability conversation. Than the browser conversation.   
Them: Maybe the— maybe, okay, that's fair. Maybe where I was thinking about like the browser's responsibility in orchestrating the exercising of Unlinkability, if that— I guess that makes sense. Like, what must the browser— since we're in the topic of what must the browser guarantee, the browser must guarantee accommodation of user privacy choices vis-à-vis Or implementing selective disclosure mechanisms that allow the user to indicate what and confirm what they're actually disclosing. Browser platform, maybe. I mean, In the— since we're talking DCI, I understand how we have to keep it limited to the browser, but it does seem like it sort of bleeds into some of the platform stuff as well here.   
Me: Mm-hmm. Mm-hmm. Okay.   
Them: Accurate transparent description of behavior and its attribution. This, this almost seems like this is discussions about show— like, for example, showing the correct origin or the doing business as name, or like identifying the site requesting presentation. In a meaningful way that would help the user understand, oh, you're on instagram.com, but this is actually Instagram DBA Meta. And, or, well, for sake of discussion, let's just say that makes sense, and meaningfully exposing that to the user prior to the user entering the ceremony kind of thing.   
Me: Mm-hmm.   
Them: Am I— maybe I'm already starting to talk about these and this isn't— I know this isn't the time for it, so.   
Me: No, but if we can— if this falls under the, I need to make sure these are clear enough that we can have a discussion, not get hung up on too much of, uh, I don't know what that means. Which is currently a very valid statement. I don't know how necessarily to fix it though, that's all. And you are helping.   
Them: Oh shoot. Well, that first line item actually just talks about what I talked about, correct establishment and conveyance of requesting origin context.   
Me: Okay.   
Them: I, uh, this was all, uh, um, AI output. Like there, there wasn't, nobody's made any editorial passes over this. Okay.   
Me: I mean, other than I did a first pass for sanity, but this isn't my area of expertise, so I didn't fix it beyond You know, did the words make reasonable sense based on what I had heard?   
Them: I only asked that in case there was a person who, who authored these and we could go to them and ask them what they missed. But okay.   
Me: Mm-mm.   
Them: And even, okay, sorry, looking at these again, prevention of unintended disclosure of credential availability. Might also allow us to remove the second to last one, a combination of user privacy choices. Unintended disclosure is, is not the same as deliberate nondisclosure.   
Me: Okay. Yes, that's correct.   
Them: So maybe under prevention of unintended disclosure, it would be enablement of intended nondisclosure. As, as those 2 could be more— less vague than a combination of user privacy choices, and then we could just delete that one, the second to last one, and   
Me: Mm-hmm. Does anyone else have an opinion on doing that? Does that make sense?   
Them: Here, I can propose that text.   
Me: Okay. Yeah, go for it.   
Them: Oh shoot, and even the one above it is availability, so we need— oops, we need like— yeah, exactly. I mean, that's about availability, not the information itself.   
Me: Mm-hmm.   
Them: All right, so there's the second one. Enable, enable, enable. Yep. But Matt, like, what do you have in mind? Like, what do you mean with prevention of unintended disclosure of credit information? Like, um, yeah, okay. So as the human who authored this, my intention here was like, what if like, um, nobody reads anything. They just click okay just to get through to the thing. And in a certain lens, that could be considered unintended disclosure because the user didn't see that the website Just blasted everything out there when the user maybe didn't want their date of birth or something. I don't know, you know, one of those attributes, they didn't want them out there for whatever reason. Um, They sort of know like, hey, I don't know, I feel like I'm building up too much of a straw man for that, but it's, I guess, the idea that if a user is going to If we build this API and mandate browser and platform behaviors assuming that users are just going to click through whatever is shown, put in front of them, how do we prevent websites from requesting everything if we deputize the browser and platforms to specifically to prevent them from doing that. I don't say— I am not suggesting we do. I'm just suggesting that if we did, that might be How we— one way that we talk about solving the problem of unintended disclosure. Because I agree, unintended disclosure is kind of vague. We could have— we could spend hours talking about what unintended disclosure is. I don't— I hope it doesn't turn into that, but that I think is what I mean by unintended disclosure. Okay, just Maybe I'm jumping into the solution. Like, I'm trying to, like, see how we can update the spec to document The person's responsibility in that regard, like, would you call, like, for example, like, requirement to use activation is one way, for example? Is this what you have in mind? Or you didn't even, like, go that far? Uh, this is— this thought is about 5 minutes old, so yeah. Okay, and you didn't go that far in 5 minutes? Okay, so I mean, I, I— what I'm, what I'm kind of hearing you saying is that it might actually like be an unrealistic thing for us to discuss. And so we shouldn't even actually put this in the list because we'll, we'll talk around it, we'll talk about it, but to focus specifically on solutions to that may run into all the problems we've had where the browser can only do so much. I mean, like in the shape of the API today, I'm not sure if we have a solution for that. Like if, for example, if you switch to capability elements, for example, yes, I can see how we can do that. But in the form of the shape of APIs of today, I'm not sure how we can put this as a browser responsibility. I feel it's Well, consider, um, this is not a fully formed idea, but one thought that I had when I was going through this list is unintended disclosure. Or even in the idea of like intentional nondisclosure, what we don't have, what we've never spent any time talking about, because I don't know how feasible it is, it may, it may not be feasible. Something browser side where a user can go when I am asked to disclose credentials. I am okay with requests that ask for these things, like don't make me jump through extra hoops, but these attributes, I am uncomfortable for websites asking me for them and I want Greater— I want to be alerted in some way that a website is requesting this thing so that I can scrutinize more intently, look at some of these— yeah, Tim, and yeah, like, I know exactly that that is a counterargument for this. So that's why I don't think it's probably not a good idea, but That. A way of capturing user comfortability with attribute disclosure and then reconciling that at presentation time as a responsibility of the browser. Maybe that's something that could be a solution. But yeah, those are kind of where my head goes with this, and those are the kinds of things that I might bring up for discussion when we get to talking about these things.   
Me: So a point I want to raise is one of the reasons it, it's so distinctly uncomfortable for me as chair to see all of the open privacy issues. Is because I've had every expectation that resolving some, any, all of them will result in us changing the API in ways we may not have originally designed for.   
Them: Mm-hmm.   
Me: Um, now whether we do it for level 1, level 2, absolutely think we should have that conversation, but We will need to be prepared to change what we've done. As a result of the conversations we're about to have. Math.   
Them: Sorry, I didn't clear my throat. So That is a— that's a very interesting point because the moment you said that, and it almost like requires of us to set aside our desires for the ultimate shape of the DC API because The shape of the DC API where it's sort of a dumb pipe and we say all the privacy stuff is handed off to the protocols, for example, like, isn't gonna pass muster. It raises all these privacy issues that are the ones that we've been spinning our wheels on. So preconceptions like now the browser needs to understand every credential schema with the implication that that's an undesirable thing, like, well, maybe we need to have a conversation and maybe it would be desirable for the browsers to understand You know. It would turn browsers into gatekeepers of what are, for the purposes of being able to allow users to assert stronger privacy at presentation time, or like to assert stronger privacy goals at presentation time, and like Maybe we do actually need to go down that route, or maybe there will be enough of a business case that the browsers are going to go like, well, actually, we thought this was a bad idea. But it turns out we have all these privacy implications that are unsolvable unless browsers do something like this. Like, do we need to go back to the drawing board to that degree for some of these things?   
Me: Uh, I, I mean, ideally I hope not, but I also know that it, it's a possibility. One of the things I've, um, chair hat off, One of the things I've wondered is, you know, a lot of things we've said while the DC API doesn't want to, you know, that's not what we do. We are going to be transporting the following protocols through to the platform. That's our job and figuring out whether the user has consented to this actually belongs to either the presentation layer or to the wallet layer or to someone else. So why don't we Formally request a change in one side or the other that says you have to send us a signal that you asked for a thing, you know, you asked for something and received a response. And that way, if someone comes to us and says, you know, was, was there a consent dialog, we can say we don't let stuff through unless there's a— unless the OpenID for VP has a consent dialog. We don't care what the dialog is, but we have very clearly said they had to signal to us that it was done. I don't know how crazy pants that is, but that's, that's how I thought we would handle the layering. Once we know what, what each layer has to do, make sure each layer signals that it did what we said it has to do.   
Them: Jeez, this almost— this evokes like some of the verifiable intent stuff going on in the agentic. Authentication space or agentic, like shopping space where like you need almost like the browser doesn't trust anything. It executes on. And so like it needs these signed responses going like, here's the actions that were taken by the platform.   
Me: Mm-hmm. Well, thanks to regulators, the browsers can't trust a whole lot because they keep being held accountable for decisions that, you know, traditionally are none of their darn business. But they keep getting taken to court about that these days.   
Them: Do we need it? Is this a similar— are some of these problems similarly shaped? To the whole. You know, agentic thing where not— and I don't want to, I don't want to over-index on like agentic LLM capturing, you know, execution and stuff like that, but it's more like more along the lines of like the platform is going to make some assurances about a part of the ceremony that occurred as brokered by the platform and then pass a verifiable signal around. I guess in our context, it would be back to the browser as like mid-ceremony, and then the browser would verify that the platform signed off on something like I wonder if we got to go down that route for some to achieve some of these.   
Me: I, I'm not a developer. I cannot play one on TV, but I think you, you kind of only have 3 choices, one of which is definitely not great. Um, you can either re-architect the API to be much heavier weight and do more in and of itself.   
Them: As in No, no, no.   
Me: Or you can demand signals from the other APIs that you're dealing with that they have done. Whatever the right thing is supposed to be. Or you can say, we're not going to do any of those things, and that's an exercise best left to the reader, at which point the regulators will kick our ass. Mohammed.   
Them: Or we can be reactive, like you have a mechanism to, let's say, you know, when we spot like something is not going well, we basically have these, have like a block list of wallets or like We can also do that, like, you know, add all the, like, the hooks where we can actually use it in the future when needed, like.   
Me: Mm-hmm. Yep, that's true. Yes. That makes sense. I then have questions of who, who maintains such a list and how do you hook into it, but that's, that's a, that's a future problem. Tim.   
Them: I think we are thinking we are on the hook for way more than we are. Implementers are on the hook, like we are not on the hook, right? Like ultimately every browser vendor needs to meet their own policies and take their regulatory risks. Like, I think we think we are more on the hook than we are. I just want to say that. You have to provide the means to do something, but there's nothing at the API that does that.   
Me: Okay.   
Them: Who would be sort of a backing, like who could tell us if that's true or not? Is that, is it TAG? Is it Because like we are accountable to something that says we have to solve this. I assume it's within the W3C. And like what, like How can we level set expectations of to what degree we solve these problems?   
Me: Well, the accountability part is that's what these 26 issues are. Asking us to figure that out.   
Them: Okay. Fair point. From the regulatory perspective, we also have the Report B from the European Commission, and that also they are dropping some requirements.   
Me: Okay, that's going to be interesting. Though, to be fair, Simone, the requirements that they had were not very useful.   
Them: Yeah, but okay, but they are asking us to say, okay, which is your status regarding these requirements?   
Me: Okay. Well, I'm gonna— I appreciate the European Commission as an important stakeholder. But it is not the only stakeholder. And so for the sake of, of the issues that we, we have under the privacy banner, I, I want to take their input, but their input is not necessarily going to help us. Close these. Okay. Um, does anyone else have thoughts or feedback on how that list is structured, uh, for the conversation, the DC API privacy issue document? Okay. Um, then my next steps is I have a note out to the spec editors. Uh, as well as Tara and Simone from the W3C, um, so that we can sit down for at least 90 minutes, possibly longer than that, and work through this until, you know, we have tentative agreement on proposed outcomes. We have homework assignments assigned for spec text to give us so that we can then bring it all back to the working group and say this is, this is the proposed path forward and see if we have consensus. Nick is also invited to chime in on that, and I very much hope he does. Uh, my goal is to have that meeting before the end of the calendar year. Um, Tim, you had asked, do I have a time zone in mind? No, I want to see what people come back with and if there is any overlap at all, and, um, we'll schedule from there.   
Them: Yeah, I mean, my availability answers will depend on if we're trying to target a time zone because like I told Tara, I'm willing to do like one meeting at 11 PM, but I just need to plan it.   
Me: Yeah, okay.   
Them: Or early, whatever.   
Me: Well, we'll see. I, um, need to poke a stick at Marcos and get him to respond as well. There can occasionally be overlaps if US people are willing to stay up late. Or get up early. Whatever. And I will also adjust accordingly. Nick is what, East Coast?   
Them: Yeah, I think Nick sees those. Where is Tara? I meant to ask her.   
Me: Uh, Portugal.   
Them: I was going to say, I thought we were dominant on the US time zones, but this is a Europe contingent.   
Me: Okay. Nope, nope. Where it's, it's like 3 US, 2, 3 Europe, and 1 Australia. I think is how it splits. Okay. Well, this was very helpful to me. Feel free to read through the rest of that document. We went through the top bits as to what are the priority decisions we're trying to make, but there's more in there regarding like language, which frankly we could potentially toss out. I didn't know which part would be most useful to getting us to progress this, but it's all there. It's not a short document, sorry about that. But your feedback is always welcome. Cool. All right, with that, um, AOB, any other business?   
Them: Yes, it was just that I was discussing with European Commission that we can have a meeting with them on the 3rd of December, which is the one in the poll. We will not have Marcos because of time zone issues and he's looking for someone else from Apple that can join in the call.   
Me: Mm-hmm. Okay.   
Them: But if this can make sense, I can just ask them to generate an invitation or something so we can put in our list.   
Me: That would— yes, that would help. Would you remind me what time? Central European time is fine.   
Them: Yes, it's European evening and US morning.   
Me: Yes, what time?   
Them: Let me check the   
Me: Because I want to, I want to put a hold on my calendar.   
Them: On 3 PM CET.   
Me: Okay. Great.   
Them: Maybe early in the morning, in your morning.   
Me: Uh, it's tag meetings always start at 6 AM anyway. It doesn't— 6 AM is a typical start for me.   
Them: Oh, oh.   
Me: Yeah.   
Them: My, my ask is that this be A conversation though, not them talking at us. Because I'm not going to, I'm not going to just like, I don't want a live version of this document that is completely useless, to be honest. So. As long as it is a conversation and they're open to back and forth disagreement. Otherwise, I don't think it's a good use of time. Yeah, in general, I already forwarded them some points that Mohamed proposed, but if he would like also to define a good agenda, also you can Just send me a message. I can just— we can build together with them to have useful conversation, not like just them asking random questions.   
Me: Okay. Fabulous. All right, um, I am going to copy the meeting notes and the transcript minus the not-for-the-minute stuff, uh, into our notes document. I will upload that to GitHub during the dispatch meeting over the next hour or so. For those of you attending IETF meeting, I suspect you're going to go straight to dispatch from here. I will be online doing the same thing. And with that, I look forward to chatting with you all again soon. Have a great rest of your day.   
Them: Thank you. 