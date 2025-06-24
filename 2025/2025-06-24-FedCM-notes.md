# FedID WG/CG Telecon, 2025-06-24

* Moderators: Heather Flanagan

* Scribe: Sam

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * Meeting schedule  
    * FedCM-related calls on 1 and 15 July are cancelled  
    * Full WG meeting proposed during [IETF 123](https://datatracker.ietf.org/meeting/123/agenda) Tuesday, 22 July, 11:30–13:30 CEST  
    * Request to restart Pacific-friendly calls  
* Ecosystem Updates (5 minutes)  
* FedCM issues  
  * [Tracking through IDP with individualized account and client\_metadata endpoints \#700](https://github.com/w3c-fedid/FedCM/pull/700)  
  * [Support showing iframe origins in the UI, when they are third-party \#725](https://github.com/w3c-fedid/FedCM/issues/725)  
  * [Accessibility Review \#741](https://github.com/w3c-fedid/FedCM/issues/741)  
* FedCM PRs  
  * [Add API to show error messages from failed token fetches \#498](https://github.com/w3c-fedid/FedCM/pull/498)  
  * [Fix spec bugs reported by togamid \#737](https://github.com/w3c-fedid/FedCM/pull/737)  
* Any Other Business (AOB)

# 

# Notes

## Administrivia

* Heather: Welcome, reminders  
* Meeting schedule  
* \[Heather\] FedCM-related calls on 1 and 15 July are cancelled  
* \[Heather\] IETF Meeting  
  * Couldn’t find host, will make it online  
* \[Heather\] Edge team interested in participating but calls not very timezone friendly  
  * Editor historically unavailable at that time  
  * We could try to find a co-chair  
  * We could try to have a design team that meets outside of the larger group  
  * Open to ideas

## Ecosystem Updates 

* \[Sam\] Chrome is starting to see Multi-IdP API in use organically. Axel Springer \+ NetID already deployed, Seznam \+ Google IdP starting to show up organically.

## FedCM Issues / PRs

### [Tracking through IDP with individualized account and client\_metadata endpoints \#700](https://github.com/w3c-fedid/FedCM/pull/700) and [Fix spec bugs reported by togamid \#737](https://github.com/w3c-fedid/FedCM/pull/737)

* \[Nicolas\] small update, initial proposal was slightly modified, to perform the checks (with the accounts endpoint and login URL in the \`.well-known\` file) only if the \`client\_metadata\` is being used (which is only useful for core-only browsers).  
* \[Ben\] Yeah, that sounds right, because that way an IdP that doesn’t use the \`client\_metadata\` doesn’t have to pay the price of announcing it in the \`.well-known\` file.  
* \[Nicolas\] Yeah, that sounds right.  
* \[Heather\] Any objections?  
* \[Heather\] Ok, sounds like you are good to go.  
* \[Nicolas\] SGTM, will pick this up after coming back from vacations.  
* \[Phil\] Does that mean that the accounts endpoint and login URL will be in the \`.well-known\` file?  
* \[Nicolas\] They don’t have to be. That’s the change: if you don’t use the client metadata, you don’t have to declare them in the well-known file.

### [Support showing iframe origins in the UI, when they are third-party \#725](https://github.com/w3c-fedid/FedCM/issues/725)

* \[Christian\] The proposal was to add the parameter to the client metadata endpoint. Ben brought up that it is not ideal to require the client metadata and add it to core, just for this. The proposal that Ben suggested is to add an extra request parameter in the JS call. One of the downsides that Yi/Nicolas raised was that the parent origin is not available to the code in the iframe (in some browsers, e.g., Firefox does not implement it). There would have to be some kind of communication between the iframe and the top level frame.  
* \[Ben\] The browser is the one who would be using origin and has access to the information in all browsers. Can’t we pass a boolean?  
* \[Christian\] Yeah, but how would you know what is the value of the boolean?  
* \[Nicolas\] The computation of the boolean requires both the top level origin and the iframe origin  
* \[Ben\] Clarification question: is the concrete example here …  
* \[Christian\] Example: some RPs may call from the same site, some RPs who do want to expose to the user. Some RPs have a static website. In other cases, you are an image editor, embedded into websites, they do want to show their full editor in the iframe.  
* \[Ben\] What about \`document.referral\`?  
* \[Christian\] Maybe we could use \`document.referral\`, but I think that would involve more work for the RPs.  
* \[Ben\] Couldn’t this be on the accounts endpoint?  
* \[Christian\] The accounts endpoint can’t have access to the RP’s name, by design.  
* \[Yi\] How would an RP know whether to show or not?  
* \[Christian\] The RP would know ahead of time whether it is the first case or not?  
* \[Yi\] Basically, the RP can choose to hide itself or not?  
* \[Nicolas\] Yeah, that’s true, but that’s the status quo?  
* \[Yi\] Wouldn’t the iframe be able to be embedded anywhere?  
* \[Christian\] The iframe can always check for Content Security Policies and check where it is at?  
* \[Ben\] The iframe “knows” if it is intelligible to the user. If so, “show it”. If not, opt-into “hide it”.  
* \[Heather\] Seems like we still have an open question, maybe we can follow up on the issue?  
* \[Yi\] I did leave a note in the issue .. how can the IdP trust that it is doing the right thing? The IdP knows if the top level frame and the inner frame are from the same entity …  
* 

### [Accessibility Review \#741](https://github.com/w3c-fedid/FedCM/issues/741)

* \[Heather\] Are we OK to include the proposed text in the spec?  
* \[Heather\] Any objections?  
* (all) none heard  
* \[Heather\] OK, seems like we can merge that in the spec then. I’ll report back on the issue that we are good to move forward. 

### [Add API to show error messages from failed token fetches \#498](https://github.com/w3c-fedid/FedCM/pull/498)

* \[Nicolas\] Hoping to get it merged. Code switch we are currently using to show a distinct message. From “code” to “error” so that it doesn’t collide with “exception code”. Any additional feedback?  
* \[Brian D\] \<3  
* \[Nicolas\] we considered putting an enum .. but would get out of sync … we leave it as an arbitrary string … just do not expose any sensitive information there … that is there …since it is exposed to the RP.  
* \[Ben\] yeah, that sounds like the right balance … i’ll hit the approve button 🙂  
* 

[https://github.com/w3c-fedid/FedCM/pull/737](https://github.com/w3c-fedid/FedCM/pull/737)

* \[Nicolas\] Small spec bug fixes  
* \[Ben\] Yep, implementing parts of this now, so  …

## Any Other Business (AOB)

* [https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-(Consensus-Blockers-for-CR)](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-\(Consensus-Blockers-for-CR\))  
  * Things that need discussion/eyeballs.  
* \[Sam\] Remind me what our Charter says about CRs?  
  * \[Heather\] We were originally aiming at CR by the summer, which is obviously unrealistic based on where things are now.  
  * \[Heather\] here is the list of blocking issues — [https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-(Consensus-Blockers-for-CR)](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-\(Consensus-Blockers-for-CR\))  
  * \[Heather\]   
  * \[Sam\] This list seems unrealistic to tackle before the end of the year, too.  
  * \[Sam\] Registration seems to be a big item blocking the CR that we don’t have a great answer for yet. \#618 seems like an open design question too.

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting, co-chair)  
* George Fletcher (Practical Identity LLC)  
* Nicolás Peña Moreno (Google Chrome)  
* Christian Biesinger (Google Chrome)  
* Phil Smart (Shibboleth/Jisc)  
* Parth Bhatt (An Independent)  
* Dan Moore (FusionAuth)  
* Sam Goto (Google Chrome)  
* [TallTed // Ted Thibodeau Jr](https://github.com/TallTed) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* Brian Daugherty (Google Identity)  
* Ben Kelly (Meta)  
* Emily Lauber (Microsoft Identity)  
* Simone Onofri (W3C)

# Regrets

*  