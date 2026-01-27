# FedID WG/CG Telecon, 2026-01-27

* Moderators:  Heather

* Scribe: Isaiah

* Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

* Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (5 minutes)  
* Issues & PRs (15 minutes)  
  * [FedCM Service Worker Interception \#802](https://github.com/w3c-fedid/FedCM/pull/802)  
* Proposals for new Stage 1 items (35 minutes)  
  * [Navigation Interception API](https://github.com/w3c-fedid/FedCM/blob/main/explorations/drafts/interception.md)  
  * [FedCM for Android IdPs](https://github.com/samuelgoto/proposal-android-idps)  
  * [Agentic Login Toolkit](https://github.com/samuelgoto/agentic-login-toolkit)  
* Any Other Business (AOB)

# Notes

## Ecosystem Updates (5 minutes)

* Emelia: Prototype of FedCM integration for ATProto by Willem Dantuma. Needs IdP registration flow in order to work fully.  
  * [https://bsky.app/profile/willem.dobs.nl/post/3mcr73bs3pk2t](https://bsky.app/profile/willem.dobs.nl/post/3mcr73bs3pk2t)  
  * WIP Pull request: [https://github.com/bluesky-social/atproto/pull/4575](https://github.com/bluesky-social/atproto/pull/4575)   
* Theo (from chat): Same as Emelia, I have implemented FedCM for Solid ( Solid community is very exited about FedCM ) but we also need the "idp-registration" feature  
* Heather: Blog article about Digital Credentials WG: https://sphericalcowconsulting.com/2026/01/27/inside-the-dcp-wg/

## Issues & PRs (15 minutes)

### [FedCM Service Worker Interception \#802](https://github.com/w3c-fedid/FedCM/pull/802)

* Christian: IdP Should be able to register service worker (SW) to intercept requests  
  * Want to be able to have device-bound credentials instead of regular cookies  
  * Different from typical SW usage, since normally only the registered SW for the host page would intercept requests, even for third-parties. In this case, we don’t want the RP to be able to intercept requests from the host page.  
  * Similar to ??  
* Suresh: Addressed comments from Nicolas and Sam on the PR  
* Suresh: Nicolás, any security and privacy issues from Google?  
* Nicolás:  
  * Didn’t have any immediate concerns.  
  * Hadn’t done a security review, so we kicked it off yesterday. Security team wanted more time to familiarize themselves with the proposal.  
  * If this is seen as an IdP fetching an RP resource, then …, but with FedCM, we want the IdP to handle the request. Unclear how we would specify this. There is some concern about this aspect.  
  * The Explainer has some incorrect information.  
* Suresh: Q about service worker:  
  * The page or origin should be the one who intercepts. But if the browser is mediating on behalf of the RP, then this is different from the service worker. You have to make it very clear to the service worker…  
  * Nicolas: SW is using the document to determine what the SW client is. The SW client determines what the origin is. I’m not very familiar with SW spec, but it might need a “foreign fetch” that allows you to use a different SW than the document. Could be worth trying to find the PR that added that (it has since been removed) to see if there is more context and whether we can reshape it for FedCM fetches. Doesn’t have to be for arbitrary fetches, but can be reused for FedCM  
* Suresh: What are the next steps then? Security review from Google?  
* Nicolas: Let’s fix the explainer: many are confused about use cases because the explainer isn’t correct or doesn’t make clear why it is important. I think resolving those two would be the best first step, then we can dedicate more work to how we can achieve it.  
* Christian: Good list of use cases would be good.  
* Suresh: I’ll reach out to the Microsoft IDNA team to see if they can add to the Explainer.  
* Emily: Clarification: 2 open PRs (one from Suresh, one from Will Bartlett), another issue (\#80?) was opened that talks  
  * We need more clarity on where we need to clarify the use cases. Which PR/issue?  
  * Nicolas: In Suresh’s PR, since it’s a self-contained document and is easier to share publicly.  
  * Emily: Some use cases are doc’d in the PR (missed Suresh’s PR); I can move some use cases from the issue into that PR.  
* Suresh: We need to move to TAG review  
* Heather: Once the explainer is clear, we can talk more about TAG review  
* Nicolas: We can file a TAG review with an explainer, that should be fine.  
* Heather: Action items:  
  * Suresh: Clean up explainer  
  * Emily: Add use cases to Suresh’s PR  
  * Then Put this back on the agenda to discuss further

## Proposals for new Stage 1 items (35 minutes)

Heather: Sam has proposed 3 items for Stage 1\. We need to discuss which of these items we want to pursue. [Proposal process](https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md)	  
Wendy: Reminder, these are early proposals for transparency. Not seeking consensus at this time.  
Sam: All these are flawed and early. Let’s go from easy to hard. Android may be easiest.

### [FedCM for Android IdPs](https://github.com/samuelgoto/proposal-android-idps)

* [Explainer](https://github.com/samuelgoto/proposal-android-idps)  
* Sam: Does this fit at all in W3C, or is it somewhere else?  
  * Problem statement, many IdPs (e.g. GMX in Germany). FedCM works well on Desktop since they’re logged into the IDP in the browser. This doesn’t transfer well to Android (and mobile in Android). Using mobile apps does not share the account between app and browser. So when they access the RP in the browser, they cannot see their IDPs.  
  * George: The user goes in the browser on the mobile, then visit a page with login using a login where they’re signed in?  
  * Sam: Yes  
  * George: Different from going to an app and getting the user logged in to the app on the phone.  
  * Christian: they want to log in with the account that happens to be logged in, not necessarily logged in to the “app.”  
  * George: Banks have been doing intra-app authentication, where the RP app treats another app as an OAuth authorization server for logging in.  
  * George: But just wanted to clarify that it’s the identity of the app account, and we’re focusing on integrating the IdP into the browser.  
  * Sam: Yes, we’re talking about web RP talking to native IdP app/account  
  * George: Eventually we’ll get native RP app to native IdP, but we’re scoping this smaller for now. Got it.  
* Heather: Is this a generalizable problem? Don’t want to bring in vendor-specific here.  
* Sam: The problem statements seems general. Haven’t gotten to the solution yet. It happens that mobile OSes where this is an issue happen to be Android/iOS  
* Tim: We should do this in Credential Management. If we do this the same way as DC API and WebAuthn, then we should reuse this. It’s just a different credential type  
* Sam: I haven’t discussed the solution yet, but does the problem statement make sense?  
* Heather: I would like to rename it to remove Android to avoid vendor-specific concerns.  
* Wendy: This is good dialog, we should make sure we collect use cases, and then the group discerns the best way forward.  
* Heather/Sam: Rename this from Android and we can move forward to Stage 1

### [Navigation Interception API](https://github.com/w3c-fedid/FedCM/blob/main/explorations/drafts/interception.md)

* Phil (from chat): Need to run, but skimmed the Navigation Interception API and thought the redirect\_to in the IdentityAssertionResponse might be generally useful for FedCM. That is, if the IdP wants to directly return the code to an endpoint on the RP (e.g. a authz code) rather than to the browser, and then more JS in the browser to send it on to that endpoint.  
* Sam: AKA IDP-Interception for FedCM?  
* Sam: Problem statement is less clear:  
  * We have deployed FedCM in many places, but it requires RP client-side code to change. This requires RP to opt-in. It doesn’t always require IdPs to redeploy if the RP uses an IdP SDK that automatically updates with these features. Shopify could do it by publishing to many WP sites, or GMX required RPs to update.  
  * Proposal allows IdPs to initiate FedCM requests for top-level navigations without requiring RPs to change client code (or server side code).  
  * Why it’s useful:  
    * Many federated logins are (server-to-server) S2S flows, when RP redirects to IdP’s site. These have not migrated to FedCM  
    * Expect it to be useful for agentic browsing: if the call is structured, then this will be easier for machine operation.  
  * Mental model: Browser downloads. We click on a link that instead of navigating to the page, it triggers a download without changing the page. The browser fetches the MIME type of the page, and then triggers the download. This is a similar mechanism: an HTTP header that the IdP sends in the response that allows the browser to react as a FedCM flow rather than a navigation. This allows   
    * Emelia raised some questions at TPAC how do we control deployments, can IdPs or RPs opt in or opt out?  
    * Sam: I think these are resolvable, but interested in discussion about this.  
* Tim: I support the discussion. Generally, I think that if we don’t start targeting agentic flows, they’re going to happen anyway, so this is a good thing to discuss.  
* Emelia: At TPAC, I had concerns: especially, does this break user’s expectations about what they’re used to? An IdP can just enable this, and the user gets a browser pop-up that they don’t expect. This could also break applications that weren’t expecting a FedCM response. Perhaps it’s worth going to the User Experience group at W3C (need to find out which one) to see if they have some ideas on whether this could ship.  
* Sam: I agree, UX is a question mark.  
* Sam: If anyone has better names, feel free to suggest. Starting with IDP-initiated  
* Heather: Ok to move to Stage 1\.

### [Agentic Login Toolkit](https://github.com/samuelgoto/agentic-login-toolkit)

* Sam: Problem Statement:  
  * There are many agentic browsers, and they’re all new and unknown, posing novel UX and accountability concerns.  
  * Many of these browser use “UI actuation” (needs a better term), similar to computer vision that views both the DOM structure and the rendered page which it uses as inputs to determine next steps to use accomplish user’s intent. It issues commands (click on this pixel, type this into this input)  
  * Precision and recall for larger LLMs is a challenge.  
  * The problem is that this is statistical, so we need to make this structured rather than unstructured.  
  * The proposal assumes RPs want agentic browsers to be used on their site for satisfying user desires. (Might not be enough incentives, or that the incentives are reversed.)  
  * Main question: How can the website direct the agent to help the user log in for the user.  
* Emelia: We already have the ability for password managers to do autofill, including 2FA. Some password managers can remember which OAuth sign-in method you used. I wonder if making that a generic web standard would be useful.  
* Sam: I think the answer is probably yes. One issue is if you make this specific to agentic, then it will be less maintained, because it has less visibility. The analogy we use is ARIA annotations. ARIA also has issues with maintenance, so we want to make sure that we design this in such a way that this gets maintained.  
* Heather: This is good.  
* Heather: There’s a lot of agentic browser work, and if you frame it this way, then maybe the agentic protocol would be a better fit. I think we should do more research on where other groups at.  
* Isaiah (from chat): Has the W3C Autofill Community Group launched yet?  
* Tim: Repeating previous sentiments: we have credential autofill in Credential Management, but we don’t have “data autofill.” These aren’t widespread or standardized across platforms  
* Emelia: Should we do a joint call with some of the other groups?  
* Tim: I try to follow all the groups; I don’t think too many are looking at this. There’s no place right now to have higher-level conversations since CredMan is relatively unmaintained and is still a draft spec owned by webappsec. We need to have more conversations here though before we start asking other groups. These conversations that need to go beyond TPAC discussions. We have to find a way to do that, since these affect everything from UX to agentic browsers, etc.  
* Emelia: I'm essentially trying to see if there's a way to move this beyond "talk at TPAC and then dies"  
* Sam: We have 5 things in CredMan: webauthn, passwords, webotp, fedcm and digital credentials.  
* Sam: The proposal also talks about this  
* Tim: Can we just have the conversation here since we don’t have to define a deliverable?  
* Sam: We need to resolve this more broadly, but we also have specific FedCM stuff working. Whether we discuss more broadly is more up to the WG.  
* Heather: The WG is broader than just FedCM, so we will see some overlap with others (DC API, for example), so it may be good to talk about this in this WG.  
* Sam: Does this move to Stage 1 as well?  
* Heather: Yes. Wendy and I can work on the GitHub repos for these.

(from chat)

* Emelia: credman seems to be part of https://www.w3.org/groups/wg/webappsec/  ?  
  * Heather: Yes  
  * Tim: just a landing spot; it’s not a traditional wg  
  * Emelia: ah, okay, so it's not the group that's actually championing it?  
  * Tim: credman itself is really just a higher level component  
* Emelia: WebMCP in the machine learning WG seems to also be focusing on this topic (how websites can help agents use tools on them)

## AOB

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Christian Biesinger (Google Chrome)  
* Isaiah Inuwa (Bitwarden)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Mike Jones (Self-Issued Consulting)  
* Phil Smart (Shibboleth/Jisc)  
* Wendy Seltzer  
* Bjorn Hjelm (Yubico)  
* Suresh Potti  
* Emelia Smith  
* Luke Dary (Red Hat/IBM)  
* George Fletcher  
* Nicolás Peña Moreno (Google Chrome)  
* [Joel Antoci](mailto:joel.antoci@shopify.com) (Shopify)  
* Theo @thhck (he/him) ( Solid CG )   
* Emily Lauber (Microsoft Identity)

