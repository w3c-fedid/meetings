# FedID WG/CG Telecon, 2026-03-24

* Moderators:  Wendy

* Scribe: Phil

* Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

* Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
    * Reminder: DST clock skew is tormenting us all from 8 March through 5 April  
* Ecosystem Updates (10 minutes)  
* Discussion (45 minutes)  
  * [Enabling IDP Interception in FedCM Request PR \#815](https://github.com/w3c-fedid/FedCM/pull/815/changes)  
  * [Cross-device/System-level FedCM Flows? \#817](https://github.com/w3c-fedid/FedCM/issues/817)  
  * Agentic Toolkit Update  
    * [IdP-Initiated Proposal](https://github.com/fedidcg/idp-initiated)  
    * [Federated Login for Agentic AI](https://github.com/samuelgoto/proposal-potentially-approved-sites)  
  * Intrusion Mitigation  
* Any Other Business (AOB)

# Notes

## Administrivia

* Wendy  
  * Code of conduct. Timezones

## 

## Ecosystem Updates (10 minutes)

* Wendy:  
  * Any updates to share.  
  * None

## Discussion (45 minutes)

### [Enabling IDP Interception in FedCM Request PR \#815](https://github.com/w3c-fedid/FedCM/pull/815/changes)

* Emily:  
  * Main update: talked about the service worker in different contexts. Suresh got feedback from the service worker group. There has been more activity on this service worker PR, so if you have thoughts, check out the PR.   
* Nicolás:  
  * There is an explainer too. Link: [https://github.com/w3c-fedid/FedCM/blob/main/explorations/service\_worker\_interception.md](https://github.com/w3c-fedid/FedCM/blob/main/explorations/service_worker_interception.md)   
* Sam:  
  * Good news. One of the big challenges was that it did not fit the service worker mental model, but now it sounds like it does? Nicolás, how did we do that?  
* Nicolás:  
  * Difference in the new proposal: instead of routing the request directly to the service worker, we surface a fetch event which the IdP service worker can listen to and respond to. Can generate a different response based on that (event).   
  * Not sure why this makes specifying it easier. But from the developer perspective, it is fairly similar.   
  * If service worker people are happy from the spec side, this unblocks us, and we can start experimenting.  
  * Interested IdPs can try it out and provide feedback.  
* Sam:  
  * Implementation cost?  
  * Does the API satisfy Microsoft’s needs?  
* Emily:  
  * Believe so, but there is a refactor which needs to be checked.   
  * The explainer goes into more detail. Proof of possession, and MS uses some different IdP routing mechanisms, which this enables.    
* Sam:  
  * Review from privacy and security reviewers would be that we can support this in Chrome, too?  
* Nicolás:  
  * This was not much different than the first, and they did not find issues with the first, so this should be good.  
* Emily:  
  * This was only on the authenticated endpoints?  
* Nicolás:  
  * Yes, it is.   
  * Not needed on the client\_metadata endpoint, because that exposes the RP. But the other ones are fine.  
  * So this is only for the credentialed endpoints.  
* Sam:  
  * Work with Wendy and Heather to add a repo for the explainer, so we can dig into it deeper  
* Emily:  
  * Does it need that?  
* Sam:  
  * OK, can it go straight into the spec?  
* Wendy:  
  * Looking at a PR right now, and if the work can go into the PR (inc. discussion).   
* Emelia:  
  * Looking at the explainer. Looking at the "request signing for DPoP". Would it be a better idea to adopt DPoP into FedCM core, so it's part of FedCM by default, and not a thing that you require service worker interception for?  
* Emily:  
  * Open to DPoP being part of FedCM itself. But there are other places where it is useful for service workers. But not as a requirement of using FedCM.  
* Sam:  
  * Rather than in the browser spec — which becomes slower to evolve — this might be better in the underlying spec  
* Emelia:  
  * Using DPoP for FedCM endpoints, then use that for signing credentials  
  * The resource server can reject the request if it does not have a DPoP header signing the credential when the resource server requires DPoP bound credentials.  
  * DPoP-Nonce is sent back from the authorisation or resource server.  
  * Could be a good extension to the protocol, and then remove some of that security aspect from needing a service worker.  
    * Service Worker Interception is still useful for other use-cases.  
* Sam:  
  * Add an issue for that.  
* Emily:  
  * Thought Aaron’s OAuth profile for FedCM mentioned DPoP, but can not see it after a quick skim.  
  * So, we need an issue to explore it.  
* Emelia:  
  * Will open up an issue: [https://github.com/w3c-fedid/FedCM/issues/820](https://github.com/w3c-fedid/FedCM/issues/820)   
* Brian (from Chat)  
  * ‘DPoP is not request signing fwiw’  
  * ‘And the nonce doesn’t work that way afaik’  
* 

### [Cross-device/System-level FedCM Flows? \#817](https://github.com/w3c-fedid/FedCM/issues/817)

* Emelia:  
  * (no initial comment, as she didn't add the issue to today's meeting, issue contained all her thoughts so far)  
* Emily:  
  * I added the agenda item and there was activity on the issue itself.  
  * Continue the discussion with a larger group about what mechanisms are possible here.   
  * In past discussions, privacy issues around which accounts are shown  
* Aram:  
  * Useful to have for our (Washington Post) use cases.   
  * Issues with users having to sign in again across different browsers and devices.  
  * Support this.  
* Nicolás:  
  * For user experience, how would this look?  
  * You can scan a QR code with your phone?  
  * How would people like to see this?  
* Emily:  
  * \+1 Will Bartlet gave an example of QR code signing.   
  * Less familiar with WebAuthn specifics  
  * But do not use device code flow (OAuth). Rather do QR code / proximity  and passkey-based.  
* Aram:  
  * The most valuable thing is presenting a standard UI so the user understands how to log in.   
  * The lack of easy user login and login-retention on the web pushes people to apps and apps do not usually provide as much value to media companies. We would prefer users to have successful web experiences with their login retained.   
  * Number one complaint we hear from users: I do not stay logged in and I don’t want to log in again. Often they log in with a webview, then try to use their browser or another webview, etc.  
* Achim:  
  * Second that, something similar to the experience that users are getting accustomed to e.g. passkeys.   
  * Very interested in cross-device.  
  * Apply more standardised and modern mechanics. Most people do the QR code thing.   
* Emily:  
  * Do browsers show up on Smart TVs?  
* Achim:  
  * No, not that  
  * Device-code flow is deployed in a number of places today  
* Emelia:  
  * Cold start problem: you are logged in on one device, but not another, e.g., mobile device but not desktop browser. I’ve not used my IdP on this device before, so the browser does not know about it, so escalating this to another device provides me a way to complete authentication on that new device with a device that already knows about my account. Somebody coming to a new app and not being able to login because they do not have an account set up on this browser is a UX problem.  
  * Reuse the login from one device to another.  
  * This could be one part of the solution to solving the cold start problem.  
* George:  
  * Getting good UX and not confusing users: Is this orthogonal, or a layer above the core bits? We do not have a shared view of what the optimal experience is; once we figure that out, we can see about making changes to the underlying protocol or mechanisms.  
* Emelia:  
  * Sam and I have been working on UX considerations for decentralised web apps with FedCM.   
  * Ongoing piece of work, not able to share anything yet.  
* George:  
  * We should not come up with different solutions to solve this problem across different devices, etc.  
* Wendy:  
  * Not yet a PR or spec change, but good to be thinking about common ideas that could go into a spec change, or is it a different layer, or passed to a different group.  
  * This is a common web problem people are having across different web experiences.  
* Emily:  
  * Possible next step: Should this be an explainer or proposal? Better to document the pain points.  
  * (Nodding has occurred)  
* Aram:  
  * Cross-device and cross-browser (same device) might have different experiences. One need not block the other.   
  * 

### Agentic Toolkit Update

[https://groups.google.com/a/chromium.org/g/blink-dev/c/FLaenhru3zo](https://groups.google.com/a/chromium.org/g/blink-dev/c/FLaenhru3zo) 

Christian:

* Extensions to FedCM to make it easier for browsers to log in using FedCM.  
* (Showing video on page: [https://github.com/samuelgoto/agentic-federated-login](https://github.com/samuelgoto/agentic-federated-login))  
  * (PS. Did not work)  
* (Explaining what is in the explainer)  
* Let the IdP tell FedCM what sites the user has signed into before  
* If a web site uses FedCM in passive mode, the dialog is there, the data is loaded, we can use the Agent, and the Agent can use the data from the passive mode call.   
* The agent can fake a click to the dialog.  
* Lots of users do not use FedCM passive mode, or FedCM at all.  
* For that we need IdP-initiated FedCM. See below.  
* The IdP sends a hash of the sites the user has logged into, and the browser can work out if it is appropriate for the current web site.   
  * Hashing is needed for…(PS. Did not catch)  
* Point of this feature is that the agent can log into the site with an existing account  
* Agent has the data, present the account chooser to the user  
* Do not want to change the RP, not easy to do.  
* (George) does the site know it is an agent or a human?  
* Those discussions are happening


George:

* Agents are non-deterministic, so who owns the liability if the agent does something they did not want them to do?  
* We should not hide these; we should be transparent.  
* We are adding a third player to the security mix.  
* Not being able to tell whether you are interacting with a human is a big deal.  
  * Otherwise, you are going to increase your checks to determine if it is a user or not.

Wendy:

* Can not solve the liability here, but we can bring the requirements up

Emelia

* The client\_id is provided by the FedCM call that is pending. Does the client\_id need to be known ahead of time?  
* That could be fetched from a remote resource using the CIMD spec: [https://client.dev/](https://client.dev/) and [https://datatracker.ietf.org/doc/draft-ietf-oauth-client-id-metadata-document/](https://datatracker.ietf.org/doc/draft-ietf-oauth-client-id-metadata-document/)   
* Client\_id can be fetched from a metadata document at a .well-known endpoint

George:

* In vanilla OIDC and OAuth, all relationships are known ahead of time.  
* Or you fetch metadata, which is in some kind of trust framework.  
* Not all client\_ids are predetermined. 

Christian:

* The proposal was not about client\_ids  
* Not this not a 1:1 relationship; this is a many-to-many relationship. This is an implementation detail.  
* The agent wants to know if an agent has an account with this website.  
* If the user chooses an account and the agent does not have an account, what do you do now?  
* If you are on [example.com](http://example.com) and the origin registered with the IdP is [auth.example.com](http://auth.example.com), how does it know? So we went with eTLD+1.   
* Challenge: RP’s do not have an SDK from the IdP included. Trying to avoid RP changes.   
* Look at the IdP-initiated offline

Emelia:

* Share link to GitHub repo with client\_id on it: [https://github.com/samuelgoto/proposal-potentially-approved-sites](https://github.com/samuelgoto/proposal-potentially-approved-sites)  
* On the topic of Agentic access, the IETF is also quite interested in this, with Cloudflare leading some of that work: [https://www.ietf.org/blog/agentic-ai-standards/](https://www.ietf.org/blog/agentic-ai-standards/) 

#### [IdP-Initiated Proposal](https://github.com/fedidcg/idp-initiated)

* 

#### [Federated Login for Agentic AI](https://github.com/samuelgoto/proposal-potentially-approved-sites)

* 

### Intrusion Mitigation

* 

## AOB

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Nicolás Peña Moreno (Google Chrome)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Joel Antoci (Shopify)  
* Bjorn Hjelm (Yubico)  
* [Aram Zucker-Scharff](mailto:aram.zucker-scharff@washpost.com) (The Washington Post)  
* Emily Lauber (Microsoft)  
* Christian Biesinger  
* Emelia Smith  
* Achim Schlosser  
* Robert Pemberton  
* Sam Goto  
* Yi Gu  
* Bumblefudge  
* Evan Prodomou  
* Brian Campbell  
* George Fletcher  
* Wendy Seltzer  
* Phil Smart (Shibboleth/Jisc)

