# FedID WG/CG Telecon, 2026-10-20

* Moderators:  Wendy Seltzer

* Scribe: 

* Call-in details: see [https\://www\.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

* Charter: [https\://www\.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

## Logistics

## The FedID WG call will be held at 15:00 UTC.

* ## We are using Zoom for the meeting.

  * ## Please log in to see the [W3C FedID WG Events Calendar](https://www.w3.org/groups/wg/fedid/calendar/) for dial-in details.

  * ## Participation is restricted to [FedID WG participants](https://www.w3.org/groups/wg/fedid/participants/) and [FedID CG participants](https://www.w3.org/groups/cg/fed-id/participants/).

## Agenda

* ## Administrivia

  * ## Scribe volunteer(s)?

  * ## Reminders:

    * ## [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)

    * ## [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)

    * ## [FedID CG/WG process](https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md)

  * ## TPAC Schedule

    * ## [Breakout Schedule](https://www.w3.org/calendar/tpac2026/breakout-sessions/grid/)

    * ## Tuesday, 27 October, 13:15–15:00 GMT: [Web Authentication WG, Web Payment Security Interest Group, Federated Identity Working Group, Verifiable Credentials Working Group Joint Meeting](https://www.w3.org/events/meetings/7f5ffe2d-c418-47f1-880a-36710212b347/)

    * ## Thursday, 29 October, 09:00–12:30 GMT, [Federated Identity Working Group, Federated Identity CG Joint Meeting](https://www.w3.org/events/meetings/64b54806-62fd-44fc-a3b0-345706c0a184/)

    * ## Thursday, 29 October, 13:45–16:45 GMT, [Federated Identity WG](https://www.w3.org/events/meetings/0c6307c0-0cd8-4308-9343-b61e2042d15f/)

  * ## Identifying new spec editor(s)

* ## Ecosystem Updates (10 minutes)

* ## Discussion (40 minutes)

  * ## [Strictly Editorial Refactoring to make merging/extending the Registration, Delegation and Accounts Push spec easier \- \#848](https://github.com/w3c-fedid/FedCM/pull/848)

  * ## [TPAC Planning](https://docs.google.com/document/d/1h5dtGQgf68-0FC-M4XPWmzSDCrjVJPHJT56WVrUh5gw/edit?usp=sharing)

* ## Any Other Business (AOB)

## 

# Notes

## Admin

* TPAC Breakouts:  
  * Sam: There’s a conflict on Monday between sessions that Evan and I recommended. Maybe I can work with Evan to de-conflict. Report and open discussion on how browsers can help with decentralized social networks. Would be good to reconcile with ActivityPub and Solid Community. There are a couple I’d think relevant to this group: email verification, phone number verification.   
  * Evan: My topic was different, so I’ll talk with Ian to see if we can de-conflict.   
  * Sam: In terms of how browsers can help with identity, do you have other thoughts?   
  * Evan: Let me focus on the schedule conflict, then will think about that. We have Social WG, breakouts on private groups and end-to-end encryption. We also have a Fediverse onboarding. We’ll also have a Fediverse meetup with local community. 

* ## TPAC Schedule

  * ## [Breakout Schedule](https://www.w3.org/calendar/tpac2026/breakout-sessions/grid/)

    * ## Tuesday, 27 October, 13:15–15:00 GMT: [Web Authentication WG, Web Payment Security Interest Group, Federated Identity Working Group, Verifiable Credentials Working Group Joint Meeting](https://www.w3.org/events/meetings/7f5ffe2d-c418-47f1-880a-36710212b347/)

    * ## Thursday, 29 October, 09:00–12:30 GMT, [Federated Identity Working Group, Federated Identity CG Joint Meeting](https://www.w3.org/events/meetings/64b54806-62fd-44fc-a3b0-345706c0a184/)

    * ## Thursday, 29 October, 13:45–16:45 GMT, [Federated Identity WG](https://www.w3.org/events/meetings/0c6307c0-0cd8-4308-9343-b61e2042d15f/)

* ## Identifying new spec editor(s)

  * Wendy: Thanks to both Nicolas and Emily. As they have moved on to other things, we need some new editors.   
  * Sam: I can pick up from Nicolas in the interim  
  * Scott: (from comments) I’d love to help contribute 

### Ecosystem Updates (10 minutes)

## Discussion

* ### [Strictly Editorial Refactoring to make merging/extending the Registration, Delegation and Accounts Push spec easier \- \#848](https://github.com/w3c-fedid/FedCM/pull/848)

  * Sam: Last time we met, Bumblefudge, Emelia, Heather and I talked after the meeting about the state of the specs and core. So far, we’ve been working with spec following implementation, so everything in the spec is implemented. Then Stage 1 proposals are earlier, not stable. To get to a Candidate Recommendation from this WG, guessing at what other browser implementers are interested in, e.g., Mozilla registration; WebKit delegation. Things we’ve heard informally. How do we handle the gap between formal specification and informal interest? I want to run a proposed change by the group.   
  * …: Proposal: have the spec be ahead of implementation, with a note where that’s the case. If that’s a good end-state, what steps should we take? We have proposals for registration, delegation, accounts push, idp-initiated. They have written specs under development. Proposal to take a pass at the baseline FedCM spec, purely editorial, to make it easier to patch in from the other repos. This PR is no normative changes, purely editorial to make it easier to merge the others in, if we choose to do so.   
  * …: To run by the group: whether that change in development mode is good, and whether these editorial changes are an appropriate way to do it. I would also like group input on how references should work. Christian, would welcome your input from working with specs in other groups.   
  * Christian: That’s a common pattern to include unstable parts, e.g., in HTML, CSS.  
  * Sam: Do they have annotations?  
  * Christian: Sometimes  
  * Sam: Take registration, for example. Would you see taking the spec and merging it into the baseline as a single file?  
  * Christian: Sure.  
  * Sam: Delegation, idp-initiated?  
  * Christian: Maybe. I don’t have the latest status on delegation.  
  * Sam: Agree, registration is more stable than delegation, but I’d probably put it in the spec.  
  * Christian: Sure, and could add idp-initiated. I think accounts push has to go into login status.  
  * Sam: If this seems reasonable, I’ll start sending PRs.  
  * … I’ve gotten some reviews already of the editorial PR, so will plan to merge by end of day, if no objections.   
  * … There will be lots of spec text flowing from repos to baseline spec. The result will be one spec that shows the entirety of what we want in the API.  
  * Wendy: Hearing no objections, we’ll merge 848 tomorrow.  
  * Sam: I might be able to write most of the PRs by TPAC, so the group can get a sense of what it looks like. Use TPAC for high-bandwidth conversation on… 

* ### [TPAC Planning](https://docs.google.com/document/d/1h5dtGQgf68-0FC-M4XPWmzSDCrjVJPHJT56WVrUh5gw/edit?usp=sharing)

  * Sam: I would appreciate some time to work on the spec itself. Emelia, Bumblefudge, and I can probably go through lots of spec PR as a subgroup; others welcome. If we had a goal to merge at TPAC, that would be great.  
  * Wendy: If that’s an editorial merge of text and issues already decided, we can review in real-time at TPAC. I’ll look at the schedule to make time for that work. 

AOB

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Wendy Seltzer (co-chair)  
* Brandon Maslen (Microsoft Edge)  
* Christian Biesinger (Igalia)  
* Yi Gu (Google Chrome)  
* Scott Lanoue  
* Sam Goto  
* Evan Prodromou  
* Bumblefudge

# Regrets

* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* 


