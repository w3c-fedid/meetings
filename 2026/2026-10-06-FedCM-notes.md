# FedID WG/CG Telecon, 2026-10-06

* Moderators:  Heather Flanagan

* Scribe: 

* Call-in details: see [https\://www\.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

* Charter: [https\://www\.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * [FedID CG/WG process](https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md)  
  * TPAC Schedule  
    * Tuesday, 27 October, 13:15–15:00 GMT: [Web Authentication WG, Web Payment Security Interest Group, Federated Identity Working Group, Verifiable Credentials Working Group Joint Meeting](https://www.w3.org/events/meetings/7f5ffe2d-c418-47f1-880a-36710212b347/)  
    * Thursday, 29 October, 09:00–12:30 GMT, [Federated Identity WG](https://www.w3.org/events/meetings/0c6307c0-0cd8-4308-9343-b61e2042d15f/)  
    * Thursday, 29 October, 13:45–16:45 GMT, [Federated Identity Working Group, Federated Identity CG Joint Meeting](https://www.w3.org/events/meetings/64b54806-62fd-44fc-a3b0-345706c0a184/)  
* Ecosystem Update (10 minutes)  
  * federated agentic login  
* Discussion (40 minutes)  
  * TPAC planning  
  * [IdP Registration](https://github.com/w3c-fedid/idp-registration)  
  * [Native App IdPs](https://github.com/fedidcg/native-app-idps)  
* AOB

# Ju Notes

## Administrivia

* 

## Ecosystem Updates (10 minutes)

* Sam: Federated Agentic Login update  
  * Origin-trialed a few months ago, 100% of users rolled out  
  * Some quirks; one API has false-positives, so still working on it, likely to stay in o-t phase longer than usual, so hard to bugtrap  
  * IDP-initiated flow for agents:   
    * Phil: Wait, what does IDP-initiated mean here? You mean the app requests info of the agent and IDP intercepts?   
    * Sam: Naming is tricky, we got pushback on “interception” (not to be confused with browser extensions intercepting JS calls in the DOM)  
    * Sam: You’re right, RP-initiated, IDP offers FedCM instead of redirection if RP supports.   
    * Sam: “traveling,” but that’s overloaded too  
    * It's this: [https\://github.com/fedidcg/idp-initiated](https://github.com/fedidcg/idp-initiated)   
    * Phil (from chat) \- Maybe: ‘IdP-Triggered Request API’ is good (might have been said, can’t remember). To avoid overlap with existing SSO terminology, if appetite to change.  
* Emelia: BlueSky FedCM branch pushed last night, but i’m going to implement myself as well; their version seems to return a \`did\`, which requires then doing a full OAuth flow on top of FedCM rather than directly returning a credential.  
  * Sam: I think that’s probably just a rough draft, I’m involved and they haven’t gotten to the /well-known/ endpoints, and we’re thinking of using delegated-Fedcm here (similar to flow in EDP).  
  * Emelia: I worked out how to do DPoP through FedCM; but I think Auth code flow is inappropriate here, and there's no coupling spec, so OAuth authorization code is the best you've got.  
    * Sam: That’s why I’m a fan of delegation, cuz it has its own endpoint that isn’t strictly kosher OAuth tokens  
    * Emelia: Isn’t that more for SD-JWTs?  
  * Emelia: I am working on my own design, will open source if i find a sponsor  
  * Sam: Multiple designs totally fine at this stage, BlueSky is still prototyping my delegation suggestion, we can compare later  
* Sam: [Native IDPs](https://github.com/fedidcg/native-app-idps) — available in Chrome canaries, some IDPs are prototyping  
  * How-to.md in addition to an explainer, so interested parties can prototype with canaries, will be proposed to stage 2 as soon as we’ve talked to enough implementers/evaluators  
  * Joel: This is for authenticated sessions in native-apps being used in 3rd party web view?  
  * Sam: Crucially, android-only for now; we’re experimenting with a more OS-integrated approach medium-term but short-term is more of a mockup/tentative implementation for now  
  * Joel: I’ll read more carefully and get back to you with some questions

## Discussion (40 minutes) 

### TPAC Planning

* Published agenda: joint meeting with WebAuthN, WebAppSec, and VCWG – DC API (web payments is not participating anymore) on Tuesday 9-12.30   
* Our meeting is Thursday — currently afternoon but might get moved to morning. (Email chairs if that’s a problem for you\!)  
  * Call between now and TPAC tbd — should finalize agenda by end of this meeting if possible  
* Agenda for our meeting  
  * Mozilla and WebKit will hopefully attend, to see what they might consider implementing (if they are at 0, maybe we move FedCM back into CG scope)  
  * What else should we allocate to bigger blocks of time?  
    * IDP Registration?  
      * Sam: Will ATP or AP or Solid folks be in attendance? It’s a big CR blocker to not have this component finalized; would benefit from high-bandwidth convo  
      * Emelia: Solid is still WebID; LWS is CID-based now; BF: yup\! elf Pavlik will definitely be there, try to reach out to them?  
    * Native IDPs?  
    * Emelia: I would advocate pinning down what is FedCM \-core-, I think our current document is a little murky on that  
    * Sam: Definitely talk to other browser vendors  
      * Emelia: Does supporting decentralized ecosystems help our case? Wasn’t that a point the Mozilla/Firefox team made?  
      * Sam: Meta implemented, and also in the native IDP stuff; getting Andrew in the room would help; Brandon might be at TPAC, Microsoft also worth inviting (Brandon thumbs up, will participate)  
    * Sam: Intrusion might be a good topic for comparing notes   
      * Yi Gu: The FedCM passive UI is intrusive to users in some cases. So we are exploring options to mitigate that issue.  
    * Joel: Did email verification land? Can we discuss it at TPAC? We’d love to report out on our implementer feedback  
      * Heather: CG hasn’t adopted it, but we could in time for TPAC if we CfC now?  
      * Sam: Great to talk at TPAC regardless, tho; we could put it in a breakout session if CG/WG time is scarce, or WebAppSec, or autocomplete CG  
      * Sam: As for where it landed, half the spec moved to IETF since it’s more of an endpoint for mail servers to stand up;   
        * Emelia: I was reading their draft, but it’s drifting a lot over there, they keep flagging that their changes contradict the current CG draft  
        * Sam: We don’t need to resolve those contradictions before getting them into scope here, we want broader input (it’s just me and Dick on the IETF side)  
        * Sam: Only talked to WebAppSec and [Autofill CG](https://www.w3.org/community/autofill/), this could fit into “verified” autocomplete, but autocomplete has its own event system and form-specific HTML prior art, while we have cryptography and security expertise that they might benefit from; WebAppSec is a bit of a grabbag  
        * Heather: Wendy and I can have a think on it  
        * Wendy: *Where* the proposal goes is far less important than who is participating. We need a first place to be having the incubation conversations, which and when normative working group is a more procedural thing (more related to IP than anything) so better to already have participants invested before that research (or recharter if needed to put it in FedID)  
        * Heather: Our WG charter ends in Feb anyway so we already need to recharter and thus the debate about FedCM in CG and/or WG  
        * Sam: EVP is way too early, no other browser has even sent an intent-to-ship; CG might be safer to avoid an underimplementation issue  
        * Sam: Brandon stepped up to coauthor; Edge doing a slightly different design, so spec might need to be loosened or extended to allow server-side DNS; Meta also interested, but it’s early to ask which WG  
    * Sam: Detailed feedback from TAG reviewers, particularly on the CG/WG division of scope question  
    * Emelia: Work on defining FedCM Core fully as the current documentation is a bit confusing to read through.  
    * Emelia: navigator.login.setStatus is where?   
      * Sam: It’s in FedID i think? It’s a rereq/normref of FedCM  
      * Heather: Link is [here](https://github.com/w3c-fedid/login-status); IIRC it was inherited from WebKit and modified a bit;   
      * Sam: But it was modified a lot, and we should check with WebKit if they want to stay co-editors, it’s a little ambiguous now how involved they will be  
      * Sam: Some of the underlying stuff moved into FedCM spec but should probably move back; I think I had an action item for it but never got back to it  
      * Emelia: We have to clean this up, some OAuth work is using this setStatus() call in different ways; “accounts” in setStatus() API \<\> account \<\> something else in [IdP Registration](https://github.com/w3c-fedid/idp-registration) ; MSFT working on service worker login.status (not FedCM)  
      * Emelia: status can be set by Header or javascript API? But the latter is more expressive so we should figure out how they overlap and how to constrain the latter if they need to be coextensive  
    * Emelia: Lightweight FedCM deprecated entirely?   
      * Sam: I am not sure, I think account-push is a useful capability that people will use for other things, maybe we break that out? Let me do some cleanup and report out at TPAC  
      * Heather: I think we need to do that ASAP to get other browser vendors and Meta in a room with a fresh, clean overview  
      * Emelia: I can chip in to that editorial cleanup  
      * Sam: Awesome, yeah we can chat after the call, i wanted to do a first pass across all the specs and make sure the PRs are consistent with each other  
* [IdP Registration](https://github.com/w3c-fedid/idp-registration)  
  * Sam: Been talking once a month with Devin from BS and iterating on mockups; they’ve been working on a feature branch, I’ve been working on a chrome-side branch of what the browser would have to do to support the flow; still figuring out the funding vehicle if this goes forward, more on that soon when we’re officially at stage 2 and have an e2e we’re both happy with; have a baseline spec  
  * Emelia: Haven’t reviewed the spec yet; I did have a question about the handle-resolution definition, which is redundant to existing ones, I think it should either be RP-side or a service \[worker?\]; i think that will inhibit adoption, feels like an “n+1” standard problem of how to get a handle from a URI;   
  * Sam: I agree, that might get iterated on or alternatives considered  
  * Sam: Someone (?) proposed making \`type\` a URL, and picking an API from the URL  
  * Sam: I want to avoid the browser having to learn all the possible resolution/discovery mechanisms; i’m guessing it can’t be the RP either expected to learn every handle system  
  * Sam: What do we call the federation?   
  * Emelia: IDP Types;   
  * Sam: There’s lots of prior art in educational federations;   
  * Phil: EduGAIN comes to mind  
  * Sam: Delegating to a federation operator would take it off RP’s and browser’s hands to understand resolution  
  * Emelia: RP needs to be able to override resolution mechanisms in some cases, right?

## Any Other Business (AOB)

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* Bjorn Hjelm (Yubico)  
* Brandon Maslen (Microsoft Edge)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Ryan Qin (Google Chrome)  
* Yi Gu (Google Chrome)  
* [bumblefudge.com](http://bumbelfudge.com) (DIF)  
* Abhishek Madan (Google Chrome)  
* Joel Antoci (Shopify)  
* Isaiah Inuwa (Bitwarden)  
* Wendy Seltzer (co-chair)


