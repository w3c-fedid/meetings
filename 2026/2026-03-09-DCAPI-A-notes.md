# FedID WG Telecon — DC API Series A, 2026-03-09

* Moderators: Wendy

* Scribe: Isaiah Inuwa

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)? Isaiah  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * Warning: DST Clock skew is here\! 8 March through 5 April 2026  
* Ecosystem Updates (5 minutes)  
* DC API Issues & PRs (45 minutes)  
  * [Addressing Request Tampering \#426](https://github.com/w3c-fedid/digital-credentials/pull/426)  
  * [EUDI Wallet functional conformance testing \#471](https://github.com/w3c-fedid/digital-credentials/issues/471)  
  * Privacy status or issues  
* Any Other Business (AOB)

# Notes

Admin: usual reminders

### Ecosystem Updates (5 minutes)

* Cf. previous meeting [notes](https://github.com/w3c-fedid/meetings/blob/main/2026/2026-03-04-DCAPI-B-notes.md#ecosystem-updates) about Mozilla’s progress on implementation

## DC API Issues & PRs

* [Addressing Request Tampering \#426](https://github.com/w3c-fedid/digital-credentials/pull/426)  
* [EUDI Wallet functional conformance testing \#471](https://github.com/w3c-fedid/digital-credentials/issues/471)  
* Privacy status or issues

## [Addressing Request Tampering \#426](https://github.com/w3c-fedid/digital-credentials/pull/426)

* **Simone:** Idea: to address tampering, we use Secure Context to have protection from network-level attacks. Perhaps to sign the request so that it is protected from the integrity point-of-view. Discussion about evaluating encryption, but this is just discussion on the privacy side for confidentiality. Also discussed whether we should also force RPs to use signing. In general, the idea is, if possible, to merge this. I’ve also seen some discussion using TLS, this is addressed by Secure Context. This PR is adding more on a different layer of communication.  
* **Christian:** Discussion in the comments about signing, but it’s not in the PR text. Is this intended?  
* **Simone:** We’ll work on the signing in another issue. We’ll also need to discuss sign-and-encrypt. This is probably a longer discussion for this PR.  
* **Christian:** We’re only talking about response encryption, not request encryption, right?  
* **Simone:** Yes.  
* **Simone:** We’ll discuss more about the signature on another issue.  
* **Wendy:** Does this make sense to everyone? Primarily a question to Christian.  
* **Christian:** Yes, I just approved; I was just waiting for the procedure to proceed.  
    
* **Wendy:** Did you address Dave Longley’s request?  
* **Simone:** Yes, I’m working on it.  
* **Wendy:** This sounds like a good approach. Thank you to everyone who reviewed and provided input. We’re good to merge.

## [EUDI Wallet functional conformance testing \#471](https://github.com/w3c-fedid/digital-credentials/issues/471)

* **Simone:** Context: we have a timely call with the European Commission. They are working on functional conformance testing for end-to-end functional testing. They are asking if W3C is interested in providing test cases, or something like WPT for functional testing. You can see the test format inside the link I added on the issue.   
* **Simone:** They are different ways: 1\) there are web platform tests that they can use, or we can draft specific test cases for them. Another thing to consider is long-term maintenance of these tests. We can ask for more information from them, but we need  
* **Mohamed:** I expect the tests to be mostly in the wallet behavior, rather than the DC API. Even Marcos’s comments are mostly about the WebDrive tests which would shortcut the Wallet anyway. I’m not sure what in the DC API would be worth testing.  
* **Simone:** As with WebAuthn, we are able to test the API in WPT, but not the full end-to-end flow.   
* **Christian:** In general, similar requests have been sent to other SDOs. “Formal conformance descriptions” is a text document.   
* … In the scope of the DC API, it’s probably fine to make sure this is working only within the DC API. The only question is how to facilitate these automated tests. For example, how do we test ISO credentials over the DC API.  
    
* **Christian:** It would make sense to have common tooling for DC API tests, so there’s one set of tools for testing. I think Joseph is working on OpenID to make sure that whatever he’s building aligns with the DC API.  
* **Simone:** In the end, it’s a web server with some automation on a driver/preconditions to check. We can’t really assert the specific state of the wallet, so it might not make sense to do this.  
* **Wendy:** Are there places where it’s helpful for W3C to play a role in testing efforts? Or is it more helpful to focus on our spec and WPT and leave the broader effort to others? How can we be most helpful?  
* **Wendy:** What sort of timeline do we have?  
* **Simone:** As soon as possible, but I can follow up.  
* **Christian:** I don’t think they have a documented timeline.   
* **Wendy:** We can think about the timeline and what to respond to.

## Privacy status or issues

* **Wendy**: We have some issues pinned on the registry and the review, how to improve the issue capture and get to a new and clearer approach to discuss the privacy considerations that we have for the underlying ecosystem. It is to encourage you to signal privacy concerns, discussions on how to address them. I expect we may not be able to satisfy all of them, so we need to document our discussions.

# AOB

* **Christian:** Tim wrote a PR about cross-device [474](https://github.com/w3c-fedid/digital-credentials/pull/474) It makes sense to me to require that. A UA should support it  
* **Mohamed:** You mean cross-device should be an option even if the platform supports?  
* **Christian:** From a UX perspective the user should be able to choose to go cross device  
* **Tim:** This is also an implementation detail. The challenge is then dictacting/assuming that cross device is handled by the platforms, that should offer this as an experience, so that you must send to the module/component responsible for it.  
* **Mohamed:** This is how it is working now; both platforms support it, when they support the request.  
* **Christian:** This is why it is important to be explicit.  
* **Lee**: Can we write it as, you should always send the request, then used as an option, we can write as it is the reality? Can we just say you’re responsible for passing through the platform?  
* **Mohamed:** Safari is not working like this?  
* **Lee:** Forcing the browser to do the right thing, it was explicit, to make both browsers and the platform with the same behaviour. Then if the platform is not supporting it….  
* **Mohamed:** So mandate platforms to use CTAP?  
* **Lee:** I would love to, but there are some dependencies such as Bluetooth. We should be clear on what  the browser should do.  
* **Simone:** A question about cross-platform compatibility: this should be useful for Mozilla, too.  
* **Christian:** We should be very clear on what our expectations are for the browser to be compliant. In my opinion, you should always give choice to the user.  
* **Tim:** I would like to be conservative as the first round, but ok to change the text.  
* **Emelia:** I am not familiar with DC, but it sounds a similar problem like with OAuth, an API needs to say that from a Browser perspective: I want to handle this on the same or a different device.  
* **Tim:** It is a similar pattern that we have on Passkeys, handled by the platform. Even though WebAuthn is more intelligent than the DC API.  
* **Emelia:** It is like to have the handoff from the browser?  
* **Tim:** The platform, like WebAuthn, there is a small detail on when the platform is incapable.  
* **Wendy**: Call ended… next DC API call is a B call.  
*  More discussion on FedCM follows.  
* **Emelia**: maybe oos, but bluesky has a lot of interest in FedCM, announcement is going to arrive in a few\!  
* **Wendy:** You can also bring in the FedCM call.  
* **Emelia**: I am also working on understanding how FedCM can work in a Decentralized fashion, also for social login e.g., on my Desktop, can i complete the login on my Phone. It is essentially a cold start problem e.g., on the accounts manager of the device.  
* **Isaiah**: it depends on the integration on the platform level e.g., with WebAuthn, used by the RP.  
* **Emelia**: a scenario is also the Internet Accounts on Mac, using a similar concept of FedCM like it happens with DC API. “cold start problem” Scenario is also on new devices, when you activate the oAuth flows.  
* **Wendy:** This is a good question for the FedCM call. It is a good idea how similar patterns can be used in different APIs.  
* **Wendy:** Thanks to everyone, we have the next one as the B call\!

# 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Wendy Seltzer  
* George Fletcher  
* Isaiah Inuwa  
* Simone Onofri  
* Mohamed Amir Yosef (Google Chrome)  
* Christian Bormann (SPRIND)  
* Ryan Watkins (Mastercard)  
* Bjorn Hjelm (Yubico)  
* Helen Qin (Google Android)  
* David Waite (Ping Identity)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Lee Campbell  
* Tim Cappalli  
* 