# FedID WG/CG Telecon, 2026-07-17

* Moderators:  Heather Flanagan

* Scribe: Phil Smart

* Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

* Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * [FedID CG/WG process](https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md)  
  * Next call \- 28 July 2026 \- FedCM and the Meta IdP deployment  
* Ecosystem Update (10 minutes)  
* Discussion (40 minutes)  
  * [FedCM facilitates vendor lock-in \#827](https://github.com/w3c-fedid/FedCM/issues/827) & [Enabling IDP Interception in FedCM Request \#815](https://github.com/w3c-fedid/FedCM/pull/815)  
  * [Defining "Core"](https://github.com/w3c-fedid/FedCM/issues?q=is%3Aissue%20state%3Aopen%20label%3Aagenda%2B%20label%3A%22needs%20resolution%22)  
* AOB

# Notes

## Administrivia

* Meta is going to come on the 28th and talk about their FedCM IdP deployment.  
* Some AOB we want to talk about

## Ecosystem Updates (10 minutes)

* Sam:  
  * Email verification went out in Chrome 150\.   
    * Origin trial went out at the beginning of July.   
    * Similar architecture to FedCM  
      * There are lots of email providers, so a large number of those are starting to use the login status API.  
      * Lightweight push model is coming up now, and more people need that  
* Heather:  
  * Email verification is not in the charter. Should it be part of this group of federated authentication methods?  
  * Side meeting in IETF on email verification (see [https://sidemeetings.ietf.org/](https://sidemeetings.ietf.org/))   
* Sam:  
  * TAG review said a lot of this belongs in the IETF. So broke up into a browser part and a backend part.   
  * But (email verification) uses a lot of the FedCM constructions.   
  * Right now, we can make changes and reach out to the FedCM providers we know to implement them, but if email providers are involved, that is harder.  
  * 

## Discussion (40 minutes)

### [FedCM facilitates vendor lock-in \#827](https://github.com/w3c-fedid/FedCM/issues/827) 

* Heahter:  
  * No MS representation on the call, has anybody got an update?  
  * (none) I will reach out to them

### [Enabling IDP Interception in FedCM Request \#815](https://github.com/w3c-fedid/FedCM/pull/815)

* (Also needs MS folk, and none here right now)

### [Defining "Core"](https://github.com/w3c-fedid/FedCM/issues?q=is%3Aissue%20state%3Aopen%20label%3Aagenda%2B%20label%3A%22needs%20resolution%22)

* Heather:  
  * Defining what is Core…  
  * Mozilla were the main advocate for this, but they are not active right now.  
  * Core is a good idea if we want the spec to be implementable by others.  
  * Sam, any thoughts on the issues tagged as about Core?  
* Emelia:  
  * Question about why Mozilla are no longer in the group, is there a path to get them back?  
* Heather:  
  * Mozilla has one person working on it part-time, whereas Chrome has a team. They have different perspectives on some of the privacy issues.   
* Emelia:  
  * Any further conversations with them?  
* Heather:  
  * Did invite them back to inform them there are other implementations.  
  * Ben is unavailable in the short term.  
  * Safari has indicated they are not going to block the work, but they do not plan to implement the work.   
    * Been hard to get them to re-engage with the group  
* Emelia  
  * Suggests that getting  IdP registration across the line would give a better narrative.  
  * Pushing for support in an open web.  
* Sam:  
  * MS is working on an IdP, Facebook, Google, and Shopify. Maybe Twitter also comes up as an IdP in a NASCAR selector.   
    * Is Twitter the last one?  
* Heather:  
  * Twitter does not show up to meetings any more.   
  * Want to attract enterprise IdPs like MS.   
* Sam:  
  * Consumer is a meaningful market, FedCM has ‘captured’ a good market share in that.   
    * Email providers own part of the Enterprise use case  
  * Registration we should work on and prioritise.   
  * What would be satisfying for this group as the next IdP to support FedCM. Large or small?  
* Heather:  
  * Being able to support R\&E and Fediverse could be an area to support.  
* Tim:  
  * What would make the needle move for WebKit, etc.  
* Sam:  
  * Firefox wrote:  
    * Initially thought a Google IdP thing.  
      * (Sam) Since then, Facebook joining might change that, MS as well.   
      * (Sam) Email providers might change that too.  
    * Was FedCM needed if Chrome no longer deprecates third-party cookies?  
* Heather:  
  * Worth having a conversation with them.  
* Tim:  
  * Once Facebook is live, ask one of the privacy groups to write why FedCM is good for privacy on the web.  
    * Importantly, from a neutral group.  
* Emelia:  
  * A few years ago, Firefox had the Firefox Persona Project. Log in securely with an identity, and that can come from anywhere. Can FedCM link that story for them?  
* Sam:  
  * Good point, we made references to Personas and made contact with the team early on.   
  * EVP (email verification: https://wicg.github.io/email-verification/)  is close to the end-state for FedCM. Also has a presentation component. And has the registration property; does not ask for a specific email provider, just asks for any; and has the delegation component. Constructed on top of FedCM status API.   
    * Maybe EVP can be a path to finding adoption in other browsers.  
  * MS is working on the service worker implementation to get accounts out of their extension or operating system.  
* Tim:  
  * It is possible that it is an MS-biased implementation.  
* Emelia:  
  * Issue to federate from one device to another.   
    * Do people remember that issue?  
* Tim:  
  * Yes, I remember.   
  * Any of these things by themselves might be vendor-biased.   
* Nicolás:  
  * Where do we stand with Core?   
* Heather:  
  * This is largely a question for the group.  
  * Homework for the group, review and comment on : [https://github.com/w3c-fedid/FedCM/issues?q=is%3Aissue%20state%3Aopen%20label%3Aagenda%2B%20label%3A%22needs%20resolution%22](https://github.com/w3c-fedid/FedCM/issues?q=is%3Aissue%20state%3Aopen%20label%3Aagenda%2B%20label%3A%22needs%20resolution%22) (issues 703, 704, 713, and 714\)  
* Emelia:  
  * Some of the issues are missing context, is that intentional?  
* Sam:  
  * It is light because the answer depends on Firefox?  
  * Can try and write down why they (Firefox) were selecting these as Core.   
    * But only captures a small section of … (PS, did not catch)  
* Heather:  
  * Post on how to implement FedCM, want others to take a look at that to make it more palatable.   
    * There has been some criticism about it appearing to be Google-biased.   
* Sam:  
  * Long term, one place to go for instructions, maybe MDN Web Docs.   
  * Should this group be responsible for instructions and live in our repo, or live in MDN?  
* Tim:  
  * There is a group for that, but no output.  
* Sam:  
  * There are technical writers at Google who might be able to help.  
  * What does the group do?  
* Tim:  
  * Single source of information about web technologies such as WebAuthn, etc.  
* Sam:  
  * Lots of the technical docs seem to live at MDN, is my impression.  
* Heather:  
  * Would like to update what we have, which is out of date  
* Sam:  
  * Is the MDN documentation not up to date?  
* Heather:  
  * Asking Nicolás  
* Nicolás  
  * Not sure if fully up to date  
* Sam:  
  * Last time I looked, it was very well written on FedCM and WebAuthn.   
    * Differences and trade-offs between those things  
  * I thought we would delete our documentation on our repo, make Chrome docs go away, and be replaced by something common, maybe MDN, or the repo that Tim is working on.  
* Tim:  
  * Was the hope with passkeys.dev, but that was recreated elsewhere by the Chrome test.  
* Nicolás:  
  * Worthwhile keeping MDN up to date.  
* Tim:  
  * MDN is not where an identity person goes to deploy this stuff  
* Heather:  
  * Check in with Nicolás to see if MDN docs are enough. 

## Any Other Business (AOB)

* [Draft FedCM documentation](https://docs.google.com/document/d/1e3ACl121XhKyUr9ibRXAwOUVPZTbeF6ZwvfzQ0bOOto/edit?tab=t.0#heading=h.a3t3m3j1pnr)  
* [https://github.com/w3c-fedid/FedCM/issues?q=is%3Aissue%20state%3Aopen%20label%3Apending-closure](https://github.com/w3c-fedid/FedCM/issues?q=is%3Aissue%20state%3Aopen%20label%3Apending-closure)   
  * Can we close this backlog of issues?  
  * Take a look at pending closure, and see if we need to talk about them or close them  
* George:  
  * I am good at closing 253\.   
  * Solved by the continue\_on capability.  
* 

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* Christian Biesinger (Google Chrome)  
* Nicolás Peña Moreno (Google Chrome)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Emelia Smith  
* Yi Gu (Google Chrome)  
* Isaiah Inuwa (Bitwarden)  
* Bjorn Hjelm (Yubico)

