# FedID WG/CG Telecon, 2025-06-10

* Moderators: Wendy Seltzer

* Scribe: Dan Moore

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * Upcoming meeting schedule  
    * summer meetings  
    * meeting during IETF 123  
* Ecosystem Updates (10 minutes)  
* FedCM issues  
  * [Make connected accounts set a quadruple \#732](https://github.com/w3c-fedid/FedCM/pull/732)  
  * [Add API to show error messages from failed token fetches \#498](https://github.com/w3c-fedid/FedCM/pull/498)  
* Any Other Business (AOB)

# 

# Notes

## Administrivia

All-remote, longer meeting during IETF 123 planned (Madrid timezone).

## Ecosystem Updates 

No ecosystem updates

## FedCM issues

* [Make connected accounts set a quadruple \#732](https://github.com/w3c-fedid/FedCM/pull/732)  
  * Nicolas spoke to this; spec bug: does not include both embedder and caller. PR addresses that.   
* [Add API to show error messages from failed token fetches \#498](https://github.com/w3c-fedid/FedCM/pull/498)  
  * Resurfacing seeking comments.  
  * Overview (Yi)  
    * Errors happen when a user signs in, at idp id assertion endpoint, idp can’t get a token (variety of reasons for this). What can idp return to end users (code, url)? Browser renders different things based on errors.  
    * If idp doesn’t return anything, show generic error.  
  * George: easy to leak security. Might be better to define core errors for browser to take action on, possibly send user back to idp.  
    * Yi: Errors are pre-defined in this API, idp can’t return any error. What kinds of security issues do you foresee?  
    * George: could leak info about, for ex, user’s password needs to be reset. OAuth errors probably okay, but constantly evolving.   
  * Ben: Ditto to what George said. Is this something you want the RP to reason about or just browser UI feedback.  
    * Yi: Question is who should render error UI, RP or browser. Browser pros: consistent experience, RP doesn’t offer that, but IDPs might want it. We want to let IDPs to let the users know about errors.   
    * Ben: only reason to make this a DOM exception is to expose to the RP.  
    * ??: This is exposed to the RP: that is the proposal.  
    * Ben: need to tighten it down, not have it be an open-ended string which is an invitation to security issue possibly in future.  
    * Christian: If an idp wants to send arbitrary error message to the RP, can use the token field (undesirable). Maybe better to have it be specific. Could happen if we don’t allow arbitrary errors.  
    * Ben: would prefer forcing people to hack.  
    * Nicolas: Why does this allow arbitrary errors (code is arbitrary  string)? Why?  
    * Yi: I don’t remember.  
    * Nicolas: we allow returning arbitrary string in this PR.  
    * George: if idp is returning stuff the browser is going to show, you run into i18n issues.  
    * Nicolas: we don’t show arbitrary string to the end user, it’s just passed to the RP.  
    * George: arb strings when crossing trust domains need to be useful to developer; need to think carefully about what data is not leaking internal info and is useful to developer. Suggest looking at this as “don’t return more data than specs should share between RP and IDP”, just another way to share info as compared to redirect. Don’t include deeper data unless we think deeply about why, including from UX perspective.  
    * Nicolas: can’t you pass arbitrary string in redirect today  
    * George: idps shouldn’t be passing arbitrary string in the error\_field parameter (from certification perspective). We now have a third trusted component in the flow–what is browser’s expectation in this context? If browser is to take some action, what is it doing and what does it need that is different? Guidance of “don’t return anything you wouldn’t have returned already” is good. Is this a different behavior with fedCM flows vs redirect flows?  
    * Ben: tradeoff be aware that extra stuff from FedCM is extra work for the IDP. What would we add if we could?  
    * George: proposal for extending step-up for OAuth2 incoming. Adding a new error code. Juggle complexity. Could add security considerations to spec, don’t use errors other than standard defined ones unless you’ve thought through (indicate level of concern).   
    * Nicolas: keeping a static fixed list has a downside of constant updates. Allowing passthrough means the browser doesn’t have to keep in sync with error types. Could add note to PR so that idps are aware of the fact this is passed to the RP so don’t pass any user info you don’t want it to have.  
    * George: makes sense to me, need to make clear where browser will act on error codes.  
    * Ben: As written, only showing message from errors.  
    * Nicolas: Only strange behavior is that if we get error messages we know how to parse we show slightly different error messages. Promise is rejected and the error code is delivered. RP can then know what to do next.  
    * George: do we show message in every case?  
    * Nicolas: if we don’t recognize the error, we show a generic message. If we do, we show a slightly less generic message.  
    * George: Are there cases where error/message is transient, and the RP could reformat things and re-send (RP could resolve it directly). Want to avoid that if this friction is unnecessary. Need to look at OAuth errors are transient.  
    * Nicolas: this is for final errors, RP cannot go back to the flow after. If transient, would use continuation API to try to fix it.  
    * George: this gets into IDPs authorization model and how it implements. If I called IDP with resource indicator without scope, some IDP may say invalid request without scope, but others may say “I know you need that” so request will succeed. Normally insufficient scope happens from API endpoint, you get the scope that is needed, so you could resubmit request with correct scope. This is the scenario he is considering. Don’t know if there’d be value in the idps being able to suppress interstitial.   
    * Wendy: add security considerations in text, there were some other things to think about. Please think about other things to tag for discussion with agenda+ label

## Any Other Business (AOB)

* [https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-(Consensus-Blockers-for-CR)](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-\(Consensus-Blockers-for-CR\))  
  * Things that need discussion/eyeballs.

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Wendy Seltzer (co-chair)  
* Dan Moore \- FusionAuth  
* George Fletcher \- Practical Identity LLC  
* Brian Daugherty (Google Identity)  
* Alex B Chalmers (self)  
* Christian Biesinger (Google Chrome)  
* Zachary Tan (Google Chrome)  
* Alex Miller (Strawberry)  
* Nicolás Peña Moreno (Google Chrome)  
* Bjorn Hjelm (Yubico)  
* Ben Kelly (Meta)  
* Ketan Mehta (NIST)  
* Emily Lauber (Microsoft Identity)  
* Achim Schlosser (Bertelsmann)  
* Yi Gu (Google Chrome)  
* Benjamin VanderSloot (Mozilla)  
* Simone Onofri (W3C)

# Regrets

* [TallTed // Ted Thibodeau Jr](https://github.com/TallTed) (he/him) ([OpenLink Software](https://openlinksw.com/)) 

