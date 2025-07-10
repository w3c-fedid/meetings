# FedID WG Telecon — DC API Series B, 2025-07-09

* Moderators: Wendy Seltzer

* Scribe: Helen


Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer: Helen Qin  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/participants/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/20240318/)  
    * FPWD is published, editors' drafts will automatically be updated in /TR  
  * Meeting schedule  
    * DC API-related call on 14 July (Series A) is cancelled  
    * Full WG meeting proposed during [IETF 123](https://datatracker.ietf.org/meeting/123/agenda) Tuesday, 22 July, 11:30 \- 13:30 CEST  
* Ecosystem Updates (5 minutes)


* DC API Issues, PRs  
  * [Add guidance on how to handle multiple presentation request entries \#249](https://github.com/w3c-fedid/digital-credentials/pull/249)  
  * [Horizontal Review \- Architecture \#230](https://github.com/w3c-fedid/digital-credentials/issues/230)  
* Any Other Business (AOB)


# Notes

## Administrivia

See above.

## Ecosystem Updates

* Marcos: implemented and landed the JSON checks and the user agent allowed protocol — landed in WebKit last week.  
  * Matt: When will it be released?  
    * Marcos: That’s on the Safari team. I can’t comment. Highly likely the next release.  
  * Lee: OpenID4VP 1.0 went final. The main spec link now points to the final version. Everyone can go review it. It refers back to our first working draft.   
    * [https://openid.net/specs/openid-4-verifiable-presentations-1\_0.html](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html#name-introduction)

## DC API PRs and Issues

[Add guidance on how to handle multiple presentation request entries \#249](https://github.com/w3c-fedid/digital-credentials/pull/249)  
Matt: Suggested wordings for preferred ordering of the requests. Do we want to handle this? If so, how?

Marcos: Switching types on the return seems bad. WebKit checks and rejects if things do that. If you request a 1 and get back a 2, that’s not allowed.

Matt: Not what I meant. What happens when you specify both v2 and v1 requests in the request array? Or OID4VP first and AnnexC second? Should the order convey preference?

Marcos: it only makes sense to get back 1 thing. 

Matt: Right, this is not intended to get back multiple things. It’s about multiple requests and getting 1 response back matching a particular request. Have suggested wordings and welcome people to look at it.

Lee: Sounds like all you are saying is to have some priority in the request array. For example, there could be a request for mdl over openid4vp and a request for mdl over annex C. Are you suggesting to mandate or recommend what the wallet should do to make that choice.

Matt: I said should for now.

Nick: We should tell the verifier what they should do and leave it up to the wallet. I’m more concerned about not just the user experience. What if the verifier asks for drastically different documents?

Matt: This didn’t intend to tackle that. In the past, we did discuss this scenario and the possibility of it.

Lee: You can already do that with a single request. For example, you can request a passport or something very different in a single oid4vp request,

Matt: Can we tackle that separately?

Nick: We should warn the verifier that it would be confusing to request for very different things. Don’t think it’s feasible to do more unless a browser get real hardcore about introspecting the request.

Matt: should we have something non-normative about this?

Ted: The idea of multiple requests and one response works great if you have a way to signal this is my last. Because otherwise the responder has no idea when to make a single reply. It doesn’t seem to work to have one reply to multiple requests.

Lee: They are not multiple requests. They are \`OR\`s. So for example you can request a driver's license (req 1\) OR a passport (req 2), so you only get 1 response back.

Ted: If I can make request 1 for dl, req 2 for passport, req 3 for library card. How does the responder know that I’ve made all 3 requests? Seems to be multiple calls.

Matt: The goal is to capture the behavior of a single DC call. Only 1 response corresponding to one of those requests in the single call should come through.

Ted: It feels like multiple GETs. I now know that’s not what’s intended but it reads to me like that.

Matt: I’ll take another look with the text then.

Marcos: Be mindful you can’t impose any requirements on the holders / wallets.

Matt: One interpretation is that you shouldn’t add this. Alternatively we do put this and could it influence the future/next protocol level.

Lee: True that this won’t be implemented by the browser. I think we can put something there. Similarly there are things in the WebAuth spec that are not implemented and read only by the browser.

Matt: Just want to suggest that verifiers order the protocols in their preference  order when they make the DC API call.

Lee: Seems reasonable.

Marcos: Yeah, that should be OK. Just be mindful that at any moment in the flow, this might become an unordered list.

Tobias: There’s a risk that we might duplicate at protocol levels, e.g., claim\_sets & credential\_sets exist in OpenID4VP and there’s a preferential order for those. Wondering if they will interfere with each other?

… clarified the use case of request level array …

Agreed the request level array isn’t intended to always represent logical equivalent requests.

Lee: In the long term, the reason this exists hopefully should be just for versioning the same protocol, e.g., if v2 of a request comes out. However, today it is indeed used for handling different protocols because wallets don’t handle all protocols. Hopefully that will go away.

For now there will be situations where you have to ask for a passport w/ OID4VP OR an mdl w/ annexC, where it’s not just about protocol versioning and the requests are not logically equivalent.

Matt: Not hearing anything that changes the major direction. Will incorporate the feedback above. In terms of process, is this meeting the only place to flag people for comments?

Wendy: You can flag people for review on github. Editors eventually approve. 

Marcos: The editors meet twice weekly as well. I meet with Mohamed and Tim. If you want to jump on those calls to do working sessions for PRs, you can ping me.

Nick (from chat): Are the editors now trying to merge what they believe has consensus of the WG? As opposed to just what they think is the best?

Marcos: Yes. 

[Horizontal Review \- Architecture \#230](https://github.com/w3c-fedid/digital-credentials/issues/230)  
Wendy: invite everyone to add into the TAG. If I don’t see more edits in a couple of days, I will submit that for TAG design review. 

Nick: Looks like the explainer might be out of date. It says that issuance is out of scope. It is in scope now. 

Marcos: We should kill the explainer. It will keep getting out of date and will confuse people. 

Wendy: In the interest of getting an overview should we point to something in the spec?

Marcos: Some specs are difficult to read. However, this spec and TAG shouldn’t be an issue anymore with clear examples and additional details. The requirement for an explainer is not a hard requirement. If the spec is actually clear, you don’t need an explainer.

Nick: I’m happy to take it offline but don’t think the spec is clear. Many people will read the examples and have no idea what goes on with the data / parameters. I’ll file issues.

Wendy: Also, if others have more things that could help with the review to list there, such as user research, please share or add to the issue.

Matt: Are we working on a timeline with the horizontal review? I’m working on an accessibility one, and I want to know how to prioritize it.

Wendy: The process deadline is at CR.  Sooner the better to get input.

## AOB

Contributor topic

Matt: [PR314](https://github.com/w3c-fedid/digital-credentials/pull/314)

Marcos: Don’t think we should do this now. We should do this when we are done. Might miss people and cause political issues. Not an important thing to have in the spec. Pretty firmly against doing this at this particular time.

Wendy: if it’s not too difficult, having names there is motivating to some people

Lee: If we get to the end it might be quite a long line. One thing that may be helpful is to help people point to this list and justify their contributions at work. I’m not against it.

Nick (from chat): I think it's nice to do as we go, but if the editors don't want to manage it, I don't think we can force them to

Matt: Don’t have to have editors manage it. We can figure out the process.

Marcos: Sure, as long as it doesn’t waste too much time.

Matt: Yes, I can massage the process to do that. I feel it’s important to recognize people's work. As to Lee’s point, this can go a long way.

Lee: The list could also be pretty static for the majority of the list.

Matt: Agree the list can get long, can do a paragraph of names. Please let me know if anyone is missing or just add yourself to the PR.

Marcos: Regarding the IPR concern, there’s nothing in the history that’s from someone not in the working group

People agreed to make a static list of names.

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Wendy Seltzer (independent)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Helen Qin (Google Android)  
* Lee Campbell (Google Android)  
* Matthew Miller (Cisco)  
* David Waite (Ping Identity)   
* Marcos Caceres (Apple)  
* Mike Jones (Self-Issued Consulting)  
* Bjorn Hjelm (Yubico)  
* Rene Leveille (1Password)  
* Nick Doty  
* Tobias Looker  
* Ryan  
* Brian 
