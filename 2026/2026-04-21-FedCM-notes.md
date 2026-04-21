# FedID WG/CG Telecon, 2026-04-21

* Moderators:  Heather

* Scribe: Sam, Nick

* Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

* Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * [FedID CG/WG process](https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md)  
* Ecosystem Updates (10 minutes)  
* Discussion (30 minutes)  
  * [Enabling IDP Interception in FedCM Request \#815](https://github.com/w3c-fedid/FedCM/pull/815)  
* Any Other Business (AOB)

# Notes

## Administrivia

* 

## 

## Ecosystem Updates (10 minutes)

* FedCM Ambient UX experiment  
  * [https://bsky.app/profile/sgo.to/post/3mhbjelwdl22d](https://bsky.app/profile/sgo.to/post/3mhbjelwdl22d)  
  * To be experimented with x% of users on Chrome  
  * Trying to solve intrusiveness. The hypothesis is that the current UX is too heavy. This is an experiment to collect data on that hypothesis by providing alternate UX.   
  * This is currently being tested for single IDPs/users, but this might change.  
  * This should augment the login credential flow as well, providing the means to login with passwords, passkeys, etc.  
* Autocomplete conditional mediation:   
  * [https://github.com/w3c-fedid/FedCM/issues/694](https://github.com/w3c-fedid/FedCM/issues/694)   
    * [https://bsky.app/profile/thisismissem.social/post/3mjwrob3iqs2p](https://bsky.app/profile/thisismissem.social/post/3mjwrob3iqs2p)   
* Federated Agentic Login  
  * [https://groups.google.com/a/chromium.org/g/blink-dev/c/FLaenhru3zo](https://groups.google.com/a/chromium.org/g/blink-dev/c/FLaenhru3zo)  
  * Nicolás Peña Moreno to give a presentation on this at BlinkOn on Apr 21, 2026  
  * Many users in Chrome are beginning to use agents for web applications, and many of the login walls for these are behind federated accounts; the goal is to help facilitate agent login for this modality.  
* 

## Discussion (30 minutes)

### [Enabling IDP Interception in FedCM Request \#815](https://github.com/w3c-fedid/FedCM/pull/815)

* Suresh  
  * enabling service worker interception for the FedCM request  
  * Service worker reviewers seem to be good with the PR.  
  * Nicolas has been reviewing the PR and also seems to be converging.  
  * Id assertion endpoint.  
  * Request signing, DPoP  
  * The initial proposal was to use a service worker. Initial feedback from the service worker group we adapted to a slightly different variation, still using service workers, but closer to how payment handlers do it.  
  * The idea is: you have the service worker path defined somewhere, either in the config file or the well known. The browser reads the path, and for all of the credentialed requests, it reaches out to the service worker and gets a response from it and carries on from there.  
  *   
* Emilia  
  * Main concern I had was “something else” (like a malicious browser extension) intercepting the request.  
* Suresh  
  * We started to prototype and we sent the I2P.  
  * CLs are under review now.  
  * Code gets merged behind a feature flag.  
  * We could start the devtrials and the origin trials.  
  * They can run a prototype on their end and see how the feature works.  
* Will  
  * The first reason that we want this for our token binding technology.  
  * The Edge browser / Chrome extension auto-attaches a token to HTTP requests with a device specific key.  
  * So, without this, we wouldn’t be able to …  
  * The second thing that we wanted is caching. We haven’t explored this much, but we need to keep the caching somewhere …  
  * DPoP and application and token binding, you either need a library to the token binding dance …. We modelled this as a “token” request …  
  * It is a series of use cases ..  
  * “Everything that is in our SDK we would like to move to the SW.”  
  * The browser extension gets installed automatically by the enterprise manager.  
  * Users can also manually install the extension.  
* Nicolas: Is there a difference between the configURL and the well-known file for the declaration of the SW?  
* Emilia: by putting the SW in the well-known file rather than in the configURL, you prevent the service worker from knowing who the RP is  
* Christian: I thought that this presupposed the user having visited the IdP in the first place …  
* Will: I think there is something about reliable activation … being in the well-known file enabled for payment handler better guarantees that it is going to be loaded …  
* 

## AOB

* Well-known and DNS  
  * [https://github.com/w3c-fedid/FedCM/pull/821](https://github.com/w3c-fedid/FedCM/pull/821)   
  * Heather: I bring up the question to the TAG, in queue (https://github.com/w3ctag/design-reviews/issues/1217), mnot aware  
  * Will: learned a couple of things: Chrome uses a cloud DNS resolver (for TXT records), no performance advantage … i started leaning towards having a reserved well known subdomain …  
  * Something like \_web-identity.well-known.\<hostname\>  
  * Sam: we should ask the IETF folks, who would be a better judge (than me at least) to evaluate this proposal. Eye-balling, this feels right to me, and I think it is more broadly available.  
  * Nicolas: What's the sequencing here?   
  * Will:   my preference would be “new than old” long term, short term we could maybe have them run in parallel for a few releases  
  * Emelia: I can help with coordinating with the IETF. You might also find that IdPs already have .well-known file.  
  * Heather: would be useful to bring the OAuth WG too.   
  * Tim: I’m still a bit skeptical that this is necessary for IdPs  
  * Will: FedCM already makes something unusual in that it uses the apex domain  
  * Tim: WebAuthn uses the apex domain  
  * Everybody: somewhat not entirely clear how other specs use the apex and .well-known files ….   
  * Heather: seems like we need more time to digest the information that we have revealed in this discussion and regroup  
*  Emilia: what kinds of cookies get sent in the FedCM request (only HTTP cookies or JS cookies too)? Use case: SPA with JS. 

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Christian Biesinger (Google Chrome)  
* Phil Smart (Shibboleth/Jisc)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Tim Cappalli (Okta)  
* Aaron Parecki (Okta)  
* Sam Goto (Google Chrome)  
* Nick Steele (OpenAI)  
* Suresh (Microsoft Edge)  
* Emelia Smith (she/her)  
* Nicolás Peña Moreno (Google Chrome)  
* Isaiah Inuwa (Bitwarden)  
* Will Bartlett (Microsoft Entra)  
* Bjorn Hjelm (Yubico)  
* Wendy Seltzer (co-chair)