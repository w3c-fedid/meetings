# FedID WG Telecon — DC API Series B, 2026-05-13

* Moderators: Heather Flanagan

* Scribe: Wendy

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/participants/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/20240318/)  
* Ecosystem Updates (10 minutes)  
* DC API Issues & PRs (45 minutes)  
  * [Relax transient activation requirement for DC API requests\#486](https://github.com/w3c-fedid/digital-credentials/pull/486)  
  * Issue Triage (starting with issue 198, oldest to newest)  
* Any Other Business (AOB)

# Notes 

## Administrivia

* Reminders Administered

## Ecosystem Updates

* Lee: I know more users of the API. Amazon has just launched it for account recovery; Intuit Turbotax, Uber using MDL to validate drivers. YouTube age verification, I think.   
* Heather: Hearing about concerns from European governments?  
* Lee: Vote has been pushed back, maybe end of May/June. I’m still hoping it’s DC API and not custom schemes. It got trickier when both protocols were mandated. Issues I’ve heard: PXP hybrid and offline, I think we’ve given good answers; Wallets having to implement both Annex C and OpenID; they’ve inferred that platforms are locking down further, not permitting European IDs. I don’t think it’s an architectural dig at the API. All this is secondhand knowledge.

## 

## DC API PRs and Issues

### [Relax transient activation requirement for DC API requests \#486](https://github.com/w3c-fedid/digital-credentials/pull/486)

* Heather: Has anyone been thinking about this?  
* Lee: We still need it. I think Mohamed will implement it behind a flag in chrome for testing. Expect you’ll get one freebie before interaction required. 

### [Issue Triage](https://github.com/w3c-fedid/digital-credentials/issues/) (starting with [issue 198](https://github.com/w3c-fedid/digital-credentials/issues/198), oldest to newest)

* Heather: We started from the oldest and worked our way up, skipping those marked *pending closure*. I’ve been following up with people in the issues to see if they’re good to close.   
* [https://github.com/w3c-fedid/digital-credentials/issues/200](https://github.com/w3c-fedid/digital-credentials/issues/200)	  
  * Tim: I still think we need this but I was overruled.   
  * Heather: OK to close?  
  * Tim: Sure  
* [https://github.com/w3c-fedid/digital-credentials/issues/208](https://github.com/w3c-fedid/digital-credentials/issues/208)   
  * Tim: That depends on [PEPC](https://github.com/WICG/PEPC/blob/main/explainer.md), which is still exploratory  
  * Heather: without normative reference to a draft, we close?  
* [https://github.com/w3c-fedid/digital-credentials/issues/209](https://github.com/w3c-fedid/digital-credentials/issues/209)   
  * Tim: It’s at the protocol layer, e.g. VP has verifier info  
* [https://github.com/w3c-fedid/digital-credentials/issues/222](https://github.com/w3c-fedid/digital-credentials/issues/222)   
  * Lee: This was a big one we talked about at IIW, a breaking change. We could do a v2 breaking change, or return array.  
  * Tim: If only we had a static method to call capabilities\!  
  * Lee: Native API will start returning an array of results.   
  * Heather: Is this V2 or V1  
  * Lee: Use of the API is still small, but growing fast. Small developer annoyance to return an array when most of the time it’s just one result. In Android, we have an accessor (\`.credential\`) that returns the first member of the array.   
  * John: I have concerns about doing this at all. How would the UX work? Multiplex inputs and responses introduces new linkability concerns  
  * Lee: It’s already supported for a single call to return multiple credentials, just constrained to come from a single wallet. The change here is to make results come from multiple wallets.   
  * John: That’s my concern  
  * Lee: In Android, actual flow looks the same as for a single wallet. Wallets have to agree to delegate consent to Android to participate in this.  
  * Heather: We’ll have to expect multiple wallets. I’m going to bump this up for conversation priority.   
* Issue 223 was closed as an artifact  
* Horizontal review issues  
  * Wendy: As we are making our plans for CR more imminent, we need to be asking each of the HR groups for their reviews. We have started on some (e.g., TAG) and work is in progress for privacy and security but haven’t made the formal requests yet. We had some work Matt Miller began on accessibility, but he’s on leave. Wendy will ping him to see if he has someone in mind to take this forward. i18n has not had any activity. We need someone to go through the review page to start identifying what we have that’s relevant to their concerns. A bit of our work will be explaining what our API does/doesn’t do in i18n-relevant ways. Do we have any volunteers for i18n?  
  * Tim: I will take security. In WebAuthn, we created parent issues for each HR and then issues for each one.  
  * Wendy: We have [issue 231](https://github.com/w3c-fedid/digital-credentials/issues/231) as the parent issue for i18n. [Issue 233 for Security](https://github.com/w3c-fedid/digital-credentials/issues/233).   
  * Tim: Where do we want to put the questionnaires? Wiki or somewhere else? Wiki gets unwieldy after a while. This might be small enough where it won’t matter.   
  * Wendy: Happy to let you do whatever makes sense to you. Any place where things can be posted, commented on, and publicly linked works.   
  * Heather: Due date June 1\.   
  * Wendy: The Process hasn’t added new HR areas yet (e.g., sustainability), so we don’t have to worry about anything like that at this time. If we end up having to discuss anything that comes up as part of the responses from the HR groups to our material, we can add that to the agenda at TPAC.  
* [https://github.com/w3c-fedid/digital-credentials/issues/246](https://github.com/w3c-fedid/digital-credentials/issues/246)   
  * John: Not sure what to do with this. Is there any way for the browser to know what different types of wallets a user has, to do anything with the information?   
  * Tim: Propose it for closing?  
* [https://github.com/w3c-fedid/digital-credentials/issues/252](https://github.com/w3c-fedid/digital-credentials/issues/252)   
  * Tim: Permission prompt isn’t required, so it would be weird to normatively define something there.   
  * John: Or guidance on what should be in a permission prompt?   
  * Tim: Most of these bullets (at least 3 and 4\) can’t be known, anyhow, and it would be odd to have yet another permission prompt  
  * Helen: Don’t want to add too much friction, and encourage people to upload their driver license instead, which is worse  
  * Tim: The request, do you want to allow this request to leave your browser  
  * John: A thought that the browser might have more information if it inspected the request or assessed the origin. This prompt helps to differentiate from custom schemes  
  * Helen: Chrome asks “do you want to share information with this site?” That’s better than custom schemes.   
  * Tim: to answer the issue, I’d say “no”   
* [https://github.com/w3c-fedid/digital-credentials/issues/255](https://github.com/w3c-fedid/digital-credentials/issues/255)   
  * Heather: This issue remains open as: Where do we say how additional protocols could be added in the future? Please add comments in the issue if you or privacy colleagues have thoughts. 

## AOB

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* Wendy Seltzer (co-chair)  
* John Schanck (Mozilla)

* Tim Cappalli (Okta)

* Helen Qin (Google)

* Lee Campbell (Google)

* Bjorn Hjelm

* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* 