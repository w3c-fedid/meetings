# FedID WG/CG Telecon, 2025-12-02

* Moderators:  Wendy

* Scribe: Emily

* Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

* Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (5 minutes)  
* Issues and PRs  
  * [Augment autofill with a conditional gett · Issue \#694](https://github.com/w3c-fedid/FedCM/issues/694)  
  * [Why must SameSite=none? \#587](https://github.com/w3c-fedid/FedCM/issues/587#issuecomment-3474372176)  
  * Recharter discussion: [https://github.com/WICG/email-verification-protocol](https://github.com/WICG/email-verification-protocol)  
  * The Road to REC:  
    * Finding/aiding additional implementers (REC requirement)  
    * Resolving Issues  
* Any Other Business (AOB)  
* 

# Notes

- ## Ecosystem Updates (5 minutes)

  - Joel’s presentation at TPAC was appreciated 

- ## Issues and PRs

  - [Augment autofill with a conditional get · Issue \#694](https://github.com/w3c-fedid/FedCM/issues/694)  
    - Sam: interested in a long time, looking for other people that may find it useful, there is prototype in canary  
    - Joel: still interested in this. Haven’t tried it yet but could develop a prototype. Implementer update looking for developer metrics and in shipping conditional get looking to quantify the experience for our users   
    - Wendy: how would feedback be the most useful?  
    - Sam: try the conditional get in canary. Will create instructions. Already sent an intent to prototype. Joel can try on his personal computer. Once Joel tries, could move to origin trials and have to real users  
    - Sam: other developers have also said metrics is important  
    - Yi: separate issue about metrics endpoint. Any requests on data wanting to be gathered from browser, please comment on [Issue \#352](https://github.com/w3c-fedid/FedCM/issues/352) with any details you’d like  
    - Sam: Is there any implementation on those metrics?   
    - Yi: there is a flag for IDP to receive timing related metrics on the server side. Could add more things as possible, but right now it’s just timing related metrics  
    - Sam: let’s see if we can get someone testing that the endpoint is working.   
    - Yi: there are instructions in the issue   
    - Sam: Does that work for you Joel? Test the plumbing of the metrics endpoint and then could add on it with the other metrics you’re looking for   
    - Joel: The ask is to test the plumbing and current metrics, and then we could build on top of it? Sounds like something we could do   
    - Sam: one of the hard things is testing the aggregation instead of individual users. Will have to go through security reviews to see if the mechanism works itself   
    - Sam: AI to write instructions for both conditional get and metrics endpoint so that Joel can test. If it works, then move to origin trials   
    - Tim: Support autofill, only concern is please make sure you’re testing with a WebAuthn (PublicKeyCredential) and a FedCM request because I don’t think two mediated requests are allowed today. Developer ergonomics will be challenging unless we change that. Test also the timing issues cause there are many dependencies   
    - Sam: Timing has been an issue. No good answer yet, two things tried: 1\) show whatever is available at a specific point at time 2\) push model with lightweight credential so that things are computed ahead of time   
    - Tim: maybe we should holistically look at this because we’re going to include a challenge URL with WebAuthN so might be worth a bigger conversation on this one   
    - Sam: Any recommendations on where to have this conversation?   
    - Tim: I’ll ping you offline. May be worth a design meeting with WebAuthn and then bring it back here   
    - Sam: Yes, we’re struggling with this issue   
  - [Why must SameSite=none? \#587](https://github.com/w3c-fedid/FedCM/issues/587#issuecomment-3474372176)  
    - Nic: Christian is not on the call   
    - Sam: We have gathered internally in Chrome that samesite lax cookies so that samesite none isn’t required. Think it's implemented behind a flag, need to review with Anne that it is consistent with Firefox and other people. Lax is more restrictive than samesite=none, so hopefully that works for people   
  - Recharter discussion: [https://github.com/WICG/email-verification-protocol](https://github.com/WICG/email-verification-protocol)  
    - Wendy: Sam did a breakout session at TPAC on this with a conclusion of “what's next”, is it something that should come to the CG or WG for further development? And if so, what steps need to happen to move that. Sam, what are you thinking?  
    - Sam: currently in WICG for lack of a better place. WICG can take us pretty far but not quite far enough. Personally thinks it could be FedID, but could also be in HTML rendering group. An intersection with passkeys too because passkeys creation can happen with this too. Its early, would love to see if people are interested. Big part of it that could fit into IETF suggested by Mark Nottingham. I am not familiar with IETF, but Dick Hardt is involved and hoping he can rely on him more there for IETF engagement. Interest from people on verifying emails. Some intersection with the use case of FedCM as IDPs as email providers  
    - Simone: under the radar of IETF, talked with Mark and Martin, thinking that IETF is the venue for it. If there are some contacts you need over there, can offer  
    - Tim: observation and opinion. Would require rechartering for FedID, It’s not wallet and not directly federation. Another home is WebSec, which is meant for these kinds of things. Open to splitting protocols to IETF and the javascript part being in W3C. Very supportive of the split. Quickest path is WebAppSec.   
    - Wendy: question for Sam is where will you find the best audience for discussion of the features and problem area. WICG repo is a fine place to keep it while you think about where to call for synchronous discussions. WICG can make calls. DC API came from WICG incubation and calls. In FedID venue, at min would need to look at CG charter. WG charter is more limiting. CG could take incubation items for discussion.  
    - Tim: to the right people, don’t think anyone here is an email expert. This group cares about the string that comes back and how it’s verified. Less concerned about the W3C audience and more concerned that email infrastructure people are involved, which is IETF  
    - Wendy: building the API for browser communication needs to coordinate with what it is verifying and coordinate with the backend infrastructure. Worth an early conversation for a Birds of a Feather session where incubation style ideas are discussed or a Dispatch item where a discussion is prepared for where in IETF it fits. It’s good to raise the flag early, this is something we’re thinking about are others thinking similarly to move this forward or have similar concerns. Sam and Dick can rely on many folks in the community on how to navigate the IETF   
    - Tim: plenty of people here that could help with IETF. The next one tho is in March in China so many people will likely not be there in person.   
    - Sam: yes many of the hard parts are in IETF such as DNS, DNS text records, SD-JWTs, and SMTP and POP. \+1 to Tim of many parts rely on IETF. \+1 to how does it relate to the API using the protocols. Two different APIs (autofill and passkey creation APIs) currently leverages it, but could expand to DC API and FedCM API. Went to OAuth workshop, but didn’t seem like the right place to go. Didn’t make it to the IETF meeting this year, could use guidance tho  
    - Tim: yes please reach out   
    - Sam: WebAppSec could also be a good location  
    - Tim: we can recharter, it does tho require going through legal processes again and charter has DC API so   
      Sam: it could intersect with FedCM and DC API, so worried it won’t have the right eyes if not discussed here some. For example the conditional get with autofill could have three in there: passkey, verified email and FedCM. re: charter. Don’t know how people think about federation, but think email is one of the most successful federations that exist. Many applications with universities who are mostly using email verification   
    - Sam: some of the largest IDPs are email providers and it’s the same use case for the verified email. Passkeys conditional get also shows up in autofill. It’s possible the DC API also shows up in the autofill. WebAppSec has fewer of those people compared to FedID   
    - Tim: be careful that just because an IDP also provides email services, there is a fundamental difference between a defined federation protocol and a verified email string.  This could spiral into being very confusing and spiral into bad decisions. If you are an IDP that uses email, then just use FedCM with a well defined federated protocol using email. But if you are an email provider, just use the verified string for email.   
    - George: generally when it comes to auth, email is the user mnemonic for how the user identifies their account. The verification of the email address in the flow is used to verify that the user presenting that mnemonic is the actual owner of it. Do we expect that model to continue to be used when we have digital credentials and other models? When people start trusting emails, some bad things start happening. Verified email shouldn’t be used as the identifier of the account. We have to be very careful in understanding the semantic: it’s the user way to identify their account at the RP.   
    - Plus and Thumbs Up in Zoom  
    - Wendy: once you start talking DNS, there are lots of strong Opinions on that subject at IETF, so underscores that it’s probably worth having conversations or a workshop. Mark Nottingham is a good guide to those processes   
    - Tim: what could also be helpful is a side by side comparison of this vs OpenID Connect. All the way from semantics of the response and expectations to infrastructure requirements. Offered to work with Sam on that  
    - Sam: that would be wonderful  
  - The Road to REC:  
    - Finding/aiding additional implementers (REC requirement)  
    - Resolving Issues  
      - Wendy: 130 issues in open state\! One piece of the task is help us triage those issues and figure out which ones can and should be resolved in current phase of work and which ones are things that might already have been resolved and which ones need further discussion. Anyone is welcome to review issues and make some notes in issues comments or tags. If difficult tagging issues, let the editors/chairs know and we can help with that. A series of pull requests that we can look at. If there are things you are able to review and leave a comment, that is also a good way to help the editors with progress. Looking at Nic if there is anything more we can be doing to help you  
      - Npm: nothing at the moment. Looking at open PRs, one about interop which is fine. One about service workers   
      - Suresh: service worker PR, npm you mentioned that Chrome security side has given the pass?   
      - Npm: waiting for Will to update the PR with any changes to the privacy or security section based on that. There is a suggestion in the pull request. The PR itself is not updated. Non-trivial why it’s okay since it’s not okay to allow service workers in every fetch. Need some explanation of why it’s needed in some cases. Would also need to be implemented in Chrome at some point  
      - Suresh: has a draft implementation ready, could need some polishing   
      - Npm: no other recent PRs. Other question about the registration. Has Heather heard back about the concerns with that one? Were going to ask how critical registration is for recommendation. Since we’re not making progress, we need more feedback on registration. Heather was meant to ping people on that but not sure if she heard back   
      - Wendy: we’ll wait for Heather to discuss that  
      - Wendy: process steps are when we think we have the complete set of features proposed in core, make sure we get all of our horizontal reviews and ordered, and then propose the transition to candidate recommendation. CR to recommendation the next critical step is diversity of implementation experience. As we move forward, where we do see those multiple parties implementing the spec interoperably   
      - Chat: registration means IDP registration   
      - Wendy: thank you for the discussion and look forward to seeing you but we are getting to the end of the year so may see calendar invites drop off as people take holidays. 

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Wendy Seltzer  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Theo \- @[thhc](https://github.com/thhck)k  
* Joel Antoci \- Shopify  
* George Fletcher (Practical Identity LLC)  
* Tim Cappalli (Okta)  
* Suresh Potti (Microsoft)  
* Emily Lauber (Microsoft Identity)  
* Isaiah Inuwa (Bitwarden)  
* Yi Gu (Google Chrome)  
* Mike Jones   
* Gorman Ho  
* Bjorn Helm  
* Sam Goto  
* Nicolas Pena Moreno  
* Alan Buxey

