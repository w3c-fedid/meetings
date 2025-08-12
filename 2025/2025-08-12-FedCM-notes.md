# FedID WG/CG Telecon, 2025-08-12

* Moderators: Heather Flanagan

* Scribe: Phil

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
    * Meeting schedule  
      * IIW Dates have Changed  
* Ecosystem Updates (5 minutes)  
* Issues  
  * [Do we need a prompt for registration? \#21](https://github.com/w3c-fedid/idp-registration/issues/21)  
* PRs  
  * n/a  
* Any Other Business (AOB)

# Notes

## Administrivia

* Heather: Looking for feedback around October meetings  
* Heather  
  * W3C code of conduct  
  * IIW dates have changed, again\! But they have changed back to the original dates?\!    
  * Does the WG and CG want to meet around IIW? If so we need a location and time.  
  * Simone…we are going to have two sessions at TPAC in November. Also, conversations are IIW, but let Heather know.

## Ecosystem Updates (5 minutes)

* Ben:  
  * Bad news on the Mozilla front, shifting priorities means FedCM has to go on the less urgent pile. Dealing with 3PC planning decisions. This is a pause, but not sure for how long.  
  * Progress was being made, but was trailing at a slow enough pace that leadership decided to pause it.  
* Sam:  
  * Thanks for bringing that up, we’ve been through this in Chrome (PS: not for FedCM, but in general). To what extent can we count on your contribution? We do not want to corner ourselves. Implementation is a lot of work, but can we get some of your time for PR reviews, directional guidance, etc?  
* Ben:  
  * This is a prioritisation issue, but it’s not on fire, although I need to cut back on overall involvement. If the thing (issue) is not controversial, please go ahead; otherwise, ask on Slack, etc.  
* Sam:  
  * How do we assess whether something is controversial or not?  
* Ben:  
  * That is a tough one. If you think something will block your implementation, please ask.  
* Christian:  
  * The [iframe issue](https://github.com/w3c-fedid/FedCM/issues/725) — can you respond to the latest comment?  
* Ben  
  * Yes.  
* Sam:  
  * Question to W3C staff: for CR, we need implementation experience, Will this block CR?  
* Simone:  
  * We need two implementations to move to CR.  
* Heather:  
  * Microsoft implementation? Based on the Chromium implementation  
* Sam:  
  * Notice some issues with FedCM in browsers even if Chromium based.Edge has their own settings.  
* Wendy:  
  * My W3C experience is that it's a fact-based question whether implementation experience demonstrates that the spec-as-written provides enough information for interoperability.  
  * If other evidence can be brought forward to show interoperability, and the spec is implementable by other folk who did not write it, that might be sufficient.  
* Heather:  
  * Any questions?  
  * Sam?  
* Sam:  
  * As a group, we have always found benefit in other browsers reviewing spec PRs. We have Suresh on the call, and MS/Edge has made significant progress on FedCM. Would Suresh take on some of the responsibility of reviewing spec PRs so we have another browser vendor review them?  
* Suresh:  
  * Yes.  
* Heather:  
  * That is good news.

## Issues

### [Do we need a prompt for registration? \#21](https://github.com/w3c-fedid/idp-registration/issues/21)

* Sam:  
  * We have been getting feedback across the board from many reviewers. Had some TAG reviews on it, Martin T. for example. Consistent feedback: users are not sure about the permissions prompt… We wanted to put a permissions prompt in front of the user so the user is asked if they wanted to register their IdP.  
  * After a round of UX discussions, we have an alternative to the prompt — because users might not know what the prompt means.  
  * Looking to prototype a registration prompt, and have the user be able to control the registered IdPs after the fact, rather than before. This decreases the friction as users do not need to accept the prompt. But opens up the possibility for abuse (PS, random sites registering themselves as IdPs)  
  * In the current flow, the browser shows a permissions prompt when an IdP wants to register.  
  * Alternatively, no permissions prompt, use some other heuristics (PS I did not catch)  
    * Also allow the user to see the registered IdPs and manage them  
  * Similar to browser search engine discovery  
  * Similar to Wifi router discovery — proximity-based, but each router doesn’t ask permission to be on the list  
  * Hard to explain without Mocks.   
* George:  
  * When a user goes to a site and invokes FedCM, and all those registered IdPs show, are they going to be able to find the ones they want?   
  * The user needs to have logged in to the IdP before the browser can register itself. (It is currently not required.)  
  * If I’ve a Disney IdP in the list, but go to Yahoo and it cannot use that IdP, how do we manage that?  
* Sam:  
  * Also concerned about that.  
  * Do we have enough controls to deal with abuse?  
  * We can possibly expose enough controls to deal with what you describe, George.  
  * We can detect if the user is logged in, passkeys, FedCM, etc.  
  * We can expose controls to the RP to describe the TYPE of IdP they are looking for. There is a ‘type’ string that describes the type of IdP requested. For example, IndieAuth, or Solid. Maybe one for edu. Having a control that allows the RP to express this is easy.  
  * But IdPs could still abuse this. Would they? This worries me about this proposal.  
  * Not sure of the answers yet, but feels solvable  
* George:  
  * I think controls are fine, but if all the sites register themselves as an IdP, and we have a huge list…(PS, maybe something they could track?)...but not efficient. But this list should be reduced to a list of the ones the user has seen in the past.  
* Tim:  
  * Difference between Wifi and IdP: You do not have the credentials for 99% of Wifi hotspots.   
  * OpenRoaming is the closest to IdP registration.   
  * Financial sites (and others) have many different sites.  
  * IdP registration is to make the user experience easier  
  * Context for the users is important, but you can give this context to users to make an informed decision to allow IdP registration  
  * Nervous about dropping the prompt…other cases where it seems too confusing to users and it gets dropped, but we should sort the text and not drop it.  
* Sam:  
  * Would rather start with a prompt.  
  * Perhaps we start with power users, rather than the general user.   
  * If we start without the prompt, we can still add it later  
* Tim:  
  * Think easier to remove prompt, rather than add them  
* Sam:  
  * Chrome UX is finding it hard to create such a prompt  
* Tim:  
  * Recommendation: the Google UX person on passkey research might be useful here.  
* Nicolás:  
  * Seems reasonable to only register logged-in IdPs.   
  * On the prompt, registering an IdP is not immediately useful.   
* Sam:  
  * RegisterProtocol handler is an existing API, and it requires user permission. So you can register OID4VP, etc., different schemes. But that was not successful.   
* George:  
  * What is the user value we are providing?   
  * If the consumer IdP is registered (Google, etc.), and they all give me a prompt. Could we use the registration API to reduce the confusion around which to use per site?  
* Sam:  
  * My use case, Mastodon server, IndieAuth (for personal website), plenty of RPs that allow my website to login.    
  * Not really useful for large identity providers.  
* George:  
  * If I do Mastodon, IndieAuth, etc., but I actually use Google for a given RP, it gets confusing. Which IdP works for each RP — how would I know that?  
* Sam:  
  * The protocol filter will help filter the list here.   
  * I only accept IndieAuth IdPs, or WebID, etc.  
* George:  
  * Usually more restrictions on what will work than just type, e.g., not all OIDC IdPs will be accepted.   
  * What do multiple tags really mean? We need to think through what we provide to users and how it will work and get that better understood, and then prompt or no prompt may fall out  
* Tim:  
  * Wondering about something in the middle — the IdP is in an interim state until the user logs in.  
  * So you can log in with an IdP which you’ve not previously used.  
* Mike:  
  * George, only show the Google IdP. But my Uni login is a Google IdP, but what you mean might not be what you said.  
  * Sam’s description of the Mastodon use case, reminds me of OpenID 2.0…  
  * (PS, cut out a bit, sorry)  
* Sam:  
  * None of this is coming out of nowhere. Taking ideas from Aaron P. and Dick H.   
* Mike:  
  * UX resulted in the NASCAR experience.  
  * Two points from before:  
    * "What is a Google IdP?" is not a simple question. It maybe [login.google.com](http://login.google.com) or [login.cmu.com](http://login.cmu.com) or various other sites that use Google as an IdP  
    * IndieAuth, etc., reminds me of what we achieved in OpenID 2.0 but without UI to make it accessible to the normal people.   
* Sam:  
  * FedCM adds to this a way to build an account chooser  
  * FedCM is a tool we did not have 15 years ago.  
  * We already have the permission prompt in Chrome Canary  
  * The original prompt framing was not necessarily the best, so we are looking to prototype removing the prompt.   
  * Trying things and seeing what sticks  
* Nicolás:  
  * Idea about forcing registration to require accounts push (lightweight) .   
* Sam:  
  * We can have that in a different discussion.  
    

## PRs

n/a

## Any Other Business (AOB)

* No AOB.   
* Next call in a week's time.  
* Add Agenda+ tag to items you want to discuss

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting, co-chair)  
* Dan Moore (FusionAuth)  
* George Fletcher (Practical Identity LLC)  
* Christian Biesinger (Google Chrome)  
* Alex B Chalmers (self)  
* Nicolás Peña Moreno (Google Chrome)  
* Wendy Seltzer (co-chair)  
* Phil Smart (Shibboleth/Jisc)  
* Bjorn Hjelm (Yubico)  
* Ben VanderSloot (Mozilla)  
* Sam Goto (Google Chrome)  
* Mike Jones (Self-Issued Consulting)  
* Ryan Galluzzo (NIST)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* Tim Cappalli (Okta)  
* Simone Onofri (W3C)  
* Alan Buxey (MyUNiDAYS Ltd.)  
* Yi Gu (Google Chrome)  
  