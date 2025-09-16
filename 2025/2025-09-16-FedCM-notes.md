# FedID WG/CG Telecon, 2025-09-16

* Moderators: Heather Flanagan

* Scribe: George Fletcher

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * Note: IIW dates have changed\!  
  * [2025 TPAC](https://www.w3.org/2025/11/TPAC/schedule.html) FedID WG meeting dates:  
    * Thursday, 13 November, @ 09:00-12:30 UTC+9  
    * Friday, 14 November, @ 09:00-12:30 UTC+9  
* Ecosystem Updates (5 minutes)  
* Issues & PRs  
* [CR status and blocking issues](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-\(Consensus-Blockers-for-CR\))  
* [Support chained authentication flows before reducing heuristics and classifications/lists in navigational tracking mitigations \#618](https://github.com/w3c-fedid/FedCM/issues/618)  
* [Allow multiple IDPs to be used \#2](https://github.com/w3c-fedid/multi-idp/issues/2)  
* Any Other Business (AOB)  
  * [https://github.com/w3c-fedid/FedCM/issues/80](https://github.com/w3c-fedid/FedCM/issues/80)   
  * [https://github.com/w3c-fedid/FedCM/issues/782](https://github.com/w3c-fedid/FedCM/issues/782)   
  * [https://github.com/w3c-fedid/FedCM/issues/781](https://github.com/w3c-fedid/FedCM/issues/781)   
  * [https://github.com/w3c-fedid/FedCM/issues/778](https://github.com/w3c-fedid/FedCM/issues/778)

# Notes

## Administrivia

* IIW dates are the week of Oct 20  
  * Separate event on Friday Oct 24, on agentic AI \- [http://agenticinternetworkshop.org/](http://agenticinternetworkshop.org/)   
* TPAC coming up Nov 10 \- 14 Japan time  
* 

## Ecosystem Updates 

* Dan: had an article on FedCM published by InfoQ: [https://www.infoq.com/articles/federated-credentials-management-w3c-proposal/](https://www.infoq.com/articles/federated-credentials-management-w3c-proposal/) 

## Issues & PRs

### [CR status and blocking issues](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-\(Consensus-Blockers-for-CR\))

* Heather: have a list of issues to be resolved for candidate recommendations  
  * Can we get to CR if we don’t have multiple independent implementations?  
  * To get to CR, you don’t need multiple independent implementations, but you do for full recommendation status  
  * There is good IP protection that comes from getting to CR  
  * Need to scrub the current list to determine what is absolutely necessary to get to CR  
* Wendy: CR is the call for multiple implementations  
  * Met the goals for charter and feature set, expect the final recommendation to look roughly like this. Also an IP gate.  
  * People need to make the IP declarations to get to CR \[Patent policy call for exclusions; if they don’t exclude, are committing relevant patents to royalty-free licensing at Recommendation\]  
* Sam: Can the working group produce multiple candidate recommendations?   
* Wendy: Yes, the group can iterate on the CRs. W3C supports both snapshots and drafts allowing interaction on the CR  
* Sam: What are the benefits of working toward CR? Understand the value of IPR protection?  
* Wendy:  
  * Signals stability of the recommendation.   
  * May drive others that are currently just watching the outputs to review. A call for input and review.  
* Sam: From a scoping perspective, it’s setting a direction and not a final scope? How to balance the core framework from features that may come later?  
* Heather: Working through the list to define what is core and what isn’t is a good start. Identifying the features that are necessary to implement to be useful.  
* Sam: Last week’s discussion on chained identity flows that scoped it out for now as the recommendation isn’t ready to support that. However, registration is also an important feature but is still early in its development.  
* Wendy: P[rocess Document](https://www.w3.org/policies/process/#transition-cr) 6.3.7. for transitioning to candidate recommendation, “must show that the specification has met all Working Group requirements, or explain why the requirements have changed or been deferred,”  
  * It’s the group's responsibility to define the list of features for this CR  
  * The group is permitted to add features to a given CR and to create a new CR based on the new features  
* Heather: There are over 200 people in the CG and just under 100 in the WG. We need more of the people who haven’t been actively engaged to review the doc, and the CR milestone is a good way to do this  
* Sam: Lightweight, registration, and account push are all features that are under development and not quite ready for CR. Do we cut a CR now and then add these later?  
* Dan: A number of key stakeholders — browsers, IdPs, and developers. Is the IdP still non-normative? There are a lot of IdPs that need to support this.  
* ???: The protocol is normative  
* Dan: Section 3 says it’s non-normative. There is some confusion on this.  
* Sam: Is this a layering question? A lot of the IdP implementation is non-normative from a browser perspective. Maybe something links Aaron’s proposal for OAuth for FedCM?  
* Dan: Is definitely aware of this initial work. Will look at whether that is enough guidance for how the IDP can implement this.  
* Nicolas: W3C is about web standards. Not in favor of an OAuth specific artifact. Would like to enhance the existing ancillary docs   
* Tim: This WG should not be defining an OpenID Connect profile; the OpenID Foundation should do that. The new group Tim is working on can develop   
  * There should not be a rush to get to CR unless there is a strong need for IP protection.   
  * Doesn’t believe not being at CR will affect adoption of browsers or IDPs  
* Heather: Rushing doesn’t make sense but we should have a clearly defined goal. We have over 100 issues open. Focusing on the ones that are needed for “CR blocker list”.  
  * Need to work through the CR blocker list. Please review.

### [Support chained authentication flows before reducing heuristics and classifications/lists in navigational tracking mitigations \#618](https://github.com/w3c-fedid/FedCM/issues/618)

* Wendy: Added to the agenda because last week it was proposed as “won’t fix”. Open for discussion.  
  * Otherwise, this issue will be closed as “won’t fix” at this time.  
  * Github issue as the thoughts on why it should be closed.  
* Heather: no objections so the issue will be closed

### [Allow multiple IDPs to be used \#2](https://github.com/w3c-fedid/multi-idp/issues/2)

* Heather: Same situation here.  
* Wendy: Proposed to close the CR blocker tag for issue \#2  
* Wendy: Hearing no objections, this issue will also be closed as “won’t fix”

## Any Other Business (AOB)

* Sam: Scoping question. If you look at the blockers list, most are addressable except for maybe registration. Account push/lightweight credentials are also of interest to many.  
  * Do we need to keep these as CR blockers or not?  
* Heather: Previously, registration and lightweight were in core  
* Sam: Didn’t believe that registration and lightweight were slated for core  
  * Doesn’t believe these need to be core features  
  * Chrome & Mozilla both believe these are valuable features  
  * Is it useful to produce a CR sooner without these features and then add them later, or wait to add them for the first CR?  
* Heather: Keep hearing that these are useful features and so should keep them in core  
* Tim: IdP registration is one of the features that removes the optics that this is just a Google thing. Believes this is very important for core.  
* Emily: IdP registration is a critical component to include  
* Nicolas: With the proposed solution, we will need to include both.  
* Emily: If they need to go together, then we need both  
* Nicolas: Account push is a prerequisite for IdP registration  
* Sam: Would like to keep registration, it goes toward enhancement rather than preservation. Also possibly multiple IdP.  
  * To follow up with Wendy on IP protections.  
  * What are the differences between the IP agreements already?  
* Wendy: By joining the W3C working group you agree to follow the W3C patent policy  
  * Every member is committing their patents unless they explicitly exclude them  
  * You get an opportunity to exclude a patent at first public working draft and at candidate recommendation approval  
* Heather: Requests IP diagram.  
* Wendy: Not sure Heather really wants to see this.

## Authentication methods on ID assertion endpoint

* Emily: Would like to push this (and the others) to next week when Will will be available.  
* Heather: Will move these to next week.

CR Blockers

* Nicolas: Can we close [729](https://github.com/w3c-fedid/FedCM/issues/729) since Ben didn’t respond?  
* George: Not sure exactly how 729 works. Concerned that it’s important for an IDP to know the origin-requesting entity; they are used for authorization decisions. Haven’t dug into all the details to see if all the proposed solutions would or wouldn’t work.   
* Christian: From your perspective, if the request is made from the iFrame, you get the iFrame origin only, is that what you would expect to get or would you also want to know the top-level origin?  
* George: That’s what was confusing to me. It sounds like it’s possible that the iFrame could be not from the requesting RP but instead from something else.  
* Christian: It depends on how you define “requesting”  
* George: Example: if Yahoo had a non-Yahoo domain, authenticated by a Yahoo IdP, would the only thing the IdP sees be that it’s from Yahoo or not-Yahoo?  
* Christian: We think that’s the less common case. What we think is more common is that they would load an SDK Javascript file. That code would make the FedCM request. Alternatively, [example.com](http://example.com) would embed [other.rp.com](http://other.rp.com) which would make their own FedCM request.   
* Nicolas: The one who gives the token is the iFrame caller. Nothing stops an iFrame from looking at its parent and deciding who it’s going to send its token to. The fact that we include the iFrame origin in the assertion doesn’t mean George’s example isn’t possible.   
* Christian: The top-level isn’t necessarily solving that issue because if [example.com](http://example.com) embeds [rp.com](http://rp.com), then what you probably want is the parent of the iFrame not the top level.   
* George: The iFrame code itself could ask for its parent; not sure how doable that is from a third-party perspective.  
* Christian: You can always get the referrer. Chrome has “ancestor origins”.  
* George: There are probably some security things here, even if it's doable. Feels like we should open an issue on the developer guides that goes into how you do this. If we don’t need a spec mechanism to do this, then we should have something that explains how to do this.  
* Christian: Agreed.  
* Emily: This conversation also relates to one of the issues I want to talk about next week, the idea that the iFrame identity is locked to the parent origin’s identity. 

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting)  
* George Fletcher (Practical Identity LLC)  
* Nicolás Peña Moreno (Google Chrome)  
* Phil Smart (Shibboleth/Jisc)  
* Yi Gu (Google Chrome)  
* Wendy Seltzer (co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* Dan Moore (FusionAuth)  
* Tim Cappalli (Okta)  
* Emily Lauber (Microsoft Identity)  
* Bjorn Hjelm (Yubico)  
* Sam Goto (Google Chrome)