# FedID WG/CG Telecon, 2025-07-29

* Moderators: Heather Flanagan

* Scribe: Heather

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
    * Meeting schedule  
      * Options:  
        * FedID Hybrid Meeting on Monday, 27 October  
        * No FedID Hybrid Meeting the week of 27 October  
        * FedID Hybrid Meeting on Thursday, 30 October  
        * Some other option   
* Ecosystem Updates (5 minutes)  
* Issues  
  * [Status of CR Blockers](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-\(Consensus-Blockers-for-CR\))  
  * [Specify the border between FedCM and protocols building on it \#764](https://github.com/w3c-fedid/FedCM/issues/764)  
  * [Allow IDPs to block invalid client IDs \#758](https://github.com/w3c-fedid/FedCM/issues/758)  
  * [Support showing iframe origins in the UI, when they are third-party \#725](https://github.com/w3c-fedid/FedCM/issues/725)  
* PRs  
  * [FedCM nonce Parameter Deprecation Specification \#762](https://github.com/w3c-fedid/FedCM/pull/762)  
  * [FedCM Object Token Enhancement Proposal \#761](https://github.com/w3c-fedid/FedCM/pull/761)  
* Any Other Business (AOB)

# Notes

## Administrivia

* Meeting schedule  
  * (Mike) don’t stomp on IIW on Thursday  
  * (Heather) And of course OIDF/DCP will be meeting on Monday

## Ecosystem Updates (5 minutes)

* (Aaron) Nothing concrete yet, but are starting some experiments with FedCM at Okta. Hope to share more soon.

## Issues

### [Status of CR Blockers](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-\(Consensus-Blockers-for-CR\))

* Suresh: I have two issues I’ve added proposals on. Starting with Issue 616\. Have a PR suggesting a resolution — [https://github.com/w3c-fedid/FedCM/pull/762](https://github.com/w3c-fedid/FedCM/pull/762)  
* Nicolas: Not sure all my comments have been addressed, but generally supportive. Not sure if we need a full doc for this or if we should modify the spec. People using FedCM will need time to migrate the nonce to the params.  
* Aaron: Looked over the PR, also onboard to dropping the nonce, it should be done in params if the protocol layer you’re using needs it (which not all do). In the PR, there is still language about the nonce in params which needs to be removed. I would rather drop it completely.  
* Christian: Agreed, the nonce should be dropped completely.  
* Nicolas: Not sure about the impact and if it counts as normative. Will need to modify the actual spec; don’t need a whole new file for this. Suggest sending a PR to modify the spec instead. Moving the nonce into params takes it out of what the browser can inspect, so it shouldn’t be in the spec.  
* Aaron: Agree with that.   
* Suresh: Next want to talk about [https://github.com/w3c-fedid/idp-registration/issues/13](https://github.com/w3c-fedid/idp-registration/issues/13) and its associated PR [https://github.com/w3c-fedid/FedCM/pull/761](https://github.com/w3c-fedid/FedCM/pull/761).  
* Nicolas: Let’s talk about the objections: first, that the proposal assumes the response is JSON but the IdP could encrypt the token with other formats like XML, at which point it would have to be passed as a string rather than an object. This also increases the complexity, both in terms of the spec and the implementation because the RP needs to check whether the token received is JSON or a string and then process it. Next, the safety of this — strings are easier to sandbox whereas objects are more tricky. Next, it doesn’t help much — you have to serialize and deserialize at different points in time. But maybe we can hear from IdPs that were originally in favor of this proposal?  
* Aaron: This came up a few times when I was building things. The thing that comes back from the API is not a token in all flows (e.g., OAuth authorization code), so it's odd to see the token property name in the first place. Also, multiple values need to come back in those responses, so I JSON encoded the data I needed, returned it as a string, then used JSON.parse to break it back out into an object. It’s weird but I can live with it. It seems natural to return as an object here because you may need multiple things, though that won’t be the case for XML. If we do go down the path of an object as a response, we shouldn’t have the name “token” in the property.   
* Christian: If we add a new field, we shouldn’t name it token, but I'm not convinced we need a new field.  
* Aaron: Not a huge deal to do json.parse on the client side.  
* Christian: If we use objects and not strings, we can reuse the same field. Javascript is javascript; you can return an object or a string, and JS will detect what it is.   
* Nicolas: If it’s something an IdP might find useful, let’s iterate on it some more. Don’t have strong opinions on this one. If it’s added, it should be in the same field which is unfortunately named token because it feels weird to add an extra field when it’s an “or” unless you get a string and an object as a response.  
* Ben: No strong opinions on this one. Nicolas: If Suresh can respond to the comments in both PRs, that will help.   
* 

### [Specify the border between FedCM and protocols building on it \#764](https://github.com/w3c-fedid/FedCM/issues/764)

* Nicolas: Does anyone have ideas on how to address the feedback? Is it a fuzzy line between where FedCM involvement stops and the protocol begins? It’s not something we’ve defined anywhere, so anyone new might be confused. Should we add text that “FedCM is protocol agnostic; any protocol in theory should be able to use FedCM”? This would just be general helper text. Not sure we want to give preferential treatment to JSON. There could be clarification.  
* Heather: (chair hat off) I think the clarification is useful.  
* Aaron: Been a while since I read the text, but generally think it makes sense to be explicit. If it can carry multiple protocols through it, it should be clear that it does so.   
* Achim: Fully agree. That’s one of the most intense discussions we’ve had, about the protocols and the bindings. Should make the specification easier to understand until there is some well adopted spec about how you’d bind OIDC to FedCM.  
* Aaron: The fact the parameter is called “token” makes the agnosticism super important to call it. Calling it token suggests that it is more of a protocol itself, so make sure we’re explicit that it can convey multiple protocols which may not include tokens in their responses.   
* Nicolas: We are already making some backwards-incompatible changes. If there is a name much better than token, please suggest and we can consider renaming.   
* Aaron: How about “data”? Keep it super generic. 

### [Allow IDPs to block invalid client IDs \#758](https://github.com/w3c-fedid/FedCM/issues/758)

* Christian: have heard requests that IdPs want the ability to block client IDs (e.g., if it’s abusive or completely made up). Because of how FedCM works now, if the user is logged in, it will show that in the account chooser. There’s no way for the IdP to not be shown on the account chooser if they don’t like that client ID. The most obvious way to implement this is to introduce a special response to the client metadata request to which the IdP could respond with “blocked clientID=true”. This request would need to be made before the account chooser request. Questions are: is this an important thing to solve, and if so, is choosing the client metadata endpoint the right way to do it? Mozilla is not a fan of the client metadata endpoint. Is it enough for an IdP to just fail the token request after the account chooser when they know the origin and client ID?  
* Achim: it would be desirable for this to NOT be possible. A login prompt for an RP that is not real would be nice to avoid. Not sure it’s the end of the world, though, as it will fail eventually in the flow.   
* Christian: If it’s a redirect flow, then the user clicks the button, the IdP gets the referrer header and will block it at a different point in time.  
* Aaron: Thinking about the enterprise scenario, it’s slightly more complicated. If a user is assigned to an application, a different user on a different team might not be assigned to that application. If a FedCM prompt shows up in the corner, it’s not necessarily known if it will succeed until they know who the user is. It’s not really an optimization because we already have the scenario where we’ll already see the prompt that will fail.  
* Christian: Can see scenarios like that, but that specific case cannot be solved because it’s a privacy property.  
* Aaron: Not saying we should solve it, saying the solution of not showing the clientID where it’s not relevant isn’t useful.  
* Christian: That’s fair. This is more if there’s a scenario where the IdP wants to avoid adding credibility to certain RPs.   
* Heather: This doesn’t feel like a CR blocker; ok to have it on the list, but perhaps not prioritized.  
* Christian: added it to the agenda because it relates to the next agenda item. 

### [Support showing iframe origins in the UI, when they are third-party \#725](https://github.com/w3c-fedid/FedCM/issues/725)

* Christian: This is on the agenda because there is consensus that we should provide a way to show the iFrame origin in the UI. The discussion is more about what the API should look like. Mozilla doesn’t like the client metadata endpoint version of this because the RP knows for sure whether showing the iFrame is the right way and because Mozilla would only need the client metadata endpoint for this proposal. It might simplify the timing attack because the client metadata endpoint gives information to the IdP before user interaction. Not 100% convinced about this specific attack vector because making a credential request to an IdP is trivial. The biggest argument for using the client metadata endpoint is that it can be done without requiring RP changes. The IdP is the one the user has trusted with their data, so the IdP has the responsibility to safeguard that data. Therefore it should be up to the IdP that the user is correctly informed. One thing proposed in this issue is that the browser indicates in the token endpoint that the origin was shown, and the IdP would reflect that. My concern about that proposal is we’d have to match two booleans. The RP wouldn’t know for certain what boolean the IdP expects. What should the API be doing here?   
* Heather: Seems like people need more time to review all the comments in that issue.  
* Christian: Would like people to dive into this.  
* Ben: Will take a look.

## PRs

### [FedCM nonce Parameter Deprecation Specification \#762](https://github.com/w3c-fedid/FedCM/pull/762)

* See Status of CR discussion above

### [FedCM Object Token Enhancement Proposal \#761](https://github.com/w3c-fedid/FedCM/pull/761)

* See Status of CR discussion above

## Any Other Business (AOB)

# Attendees (sign yourself in)

* Christian Biesinger (Google Chrome)  
* Heather Flanagan (Spherical Cow Consulting, co-chair)  
* Aaron Parecki (Okta)  
* Mike Jones (Self-Issued Consulting)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Nicolás Peña Moreno (Google Chrome)  
* Erica Kovac (Google Chrome)  
* Siddhartha Pandey (Microsoft Edge)  
* Suresh Potti (Microsoft Edge)  
* Alan Buxey (MyUNiDAYS Ltd.)  
* Emily Lauber  
* Alex B Chalmers  
* Ben Kelly  
* Bjorn Hjelm (Tubico)