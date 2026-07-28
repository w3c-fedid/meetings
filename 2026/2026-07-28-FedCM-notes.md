# FedID WG/CG Telecon, 2026-07-28

* Moderators:  Heather Flanagan

* Scribe: Sam Goto

* Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

* Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * [FedID CG/WG process](https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md)  
* Ecosystem Update (40 minutes)  
  * FedCM and the Meta IdP deployment  
* Discussion (10 minutes)  
* AOB

# Notes

## Administrivia

* 

## Ecosystem Updates (45 minutes)

### FedCM and the Meta IdP deployment

- MIchael Jasper, Meta  
- Facebook \<3 FedCM presentation  
- Software Engineer  
- [mdjasper@meta.com](mailto:mdjasper@meta.com)  
- Background in frontend development  
- Very Brief History  
  - 2008 first “Login with Facebook” (cookies & iframes)  
  - 2010 Migrated to OAuth2 (web/devices), most of the efforts stayed in new thread vectors, security attacks, etc.  
    - Third Parties, businesses, etc.  
  - 2026 (federation, device APIs)  
    - Team responsible for Web, JS SDKs  
- Adding support for FedCM  
  - Recently launched support for FedCM  
  - How it was implemented  
  - Things that we struggled with  
  - Ideas of what could be done  
- “Code wins arguments”  
  - FedCM is extremely easy to demonstrate to people  
  - Sometimes people’s eyes glaze over when you say "I'm going to implement a new standard\!”  
  - It is visual.  
  - Everybody inside Meta has already been using FedCM with Google Login.  
  - Easy to sell to inside stakeholders.  
- Discovery endpoints  
  - Nice  
    - Well documented return values  
    - Easy to customize branding (need to get colors and icons right)  
    - MDN docs are great, Google Chrome Docs were good  
  - Challenges  
    - Privacy/Security features are great but also make it harder to develop.  
    - Feature flagging makes things harder.  
    - “Copy as cURL” to test development setup, e.g., response headers that the browser ignores / fails (sometimes silently) if you don’t get right, different than traditional browser headers  
    - Meta has a lot of infrastructure for “if this header is missing, it gets marked as spam”, so needed to refactor “traditional headers” at the infrastructure level  
- Authenticated Endpoints  
  - Nice  
    - “continue\_on” feature is great\!  
    - Massive help  
- continue\_on API  
  - Enormous existing investment, a lot of it through compliance, user data is not shared inappropriately through Facebook login  
  - “I’m going to make a new way to share data with third parties\!”  
  - Continuation API is just a new endpoint that funnels people to our existing systems  
- MVP  
  - The assertion endpoint always takes the user to an OAuth dialog  
  - Resolves with IdentityProvider.resolve()  
  - Easy to implement it because the OAuth flows have been massively scrutinized  
- continue\_on  
  - Can we remove the disclosure for reauth?  
-  JS SDKs  
  - How do we not surprise RPs?  
  - How do we not break RPs existing Google Login?  
  - FedCM opt-in (would like to make it default in the future)  
  - It wasn't clear to us how to not-break Sign-in with Google with Multi-IdP.  
  - Exposes FedCM config, so RPs can build multi IdP solutions  
    - Not great, exposes internals and adds the burn to relying parties  
    - Would love to call something like navigator.credentials.add(FB.config)   
    - Would love to collaborate on Multi IdP support  
- Documentation / Developer support  
  - Docs  
  - Example Repos  
  - Hosted Apps  
- Wins  
  - FedCM internally loved @ meta  
  - Easy “story” to tell  
  - Reasonable API / integrates well with OAuth  
  - Better for UX and privacy  
- Ideas  
  - Customizable scopes: “name, telephone number and birthday”  
  - Pick which of “email”, “username” and “tel” is shown   
    - WhatsApp has username and tel, but tel is more popular  
  - Resize the continue\_on pop-up (min/max width/height flexibility)  
    - Not a traditional window.open where you pass parameters  
- Reasonable throughout APIs (what’s going to work for small startups / big companies, how is it going to work for Facebook)  
- Discussion  
  - Christian: Thanks for implementing, great feedback\! Multi IdP questions. Things about the disclosure dialog.   
    - WIth regards to the priority, the dialog only shows those fields that are returned by the accounts\_endpoint, so if you only return a phone number, it would only show a phone number.   
    - Michael: ah, that’s an interesting work around. We could have some business logic.  
    - You should write github issues for things that you’d like.  
  - George: I’m curious about the integration with OAuth, how often is it returning an access\_token for access to more APIs? How often are they just wanting identity vs API access?  
    - Michael: I don’t have any numbers right now, but roughly ⅓ .. a lot of RPs just want identity to login …. ⅓ access tokens for API access … traditionally for Facebook Login is to put a comment, like a page, etc … that behavior is decreasing … Farmville posting on Facebook’s page is not a massive use case anymore … ITP came up a few years ago. We launched “limited login” which was a login via a different domain, just an identity login …   some of the deployment is used for business use cases … the last ⅓ is the limited login Apple DNT login …  
  - Sam: Thank you for the presentation\! Have you run into approved clients?   
    - Michael: Are you talking about in the account endpoint, RPs that the user has already approved? Yes, we support that.  
    - Sam: We don’t show disclosure text for approved clients.  
    - Michael: I would not want to hide the disclosure text. From a compliance point of view, we want to always show it. What we want is to add additional fields to the disclosure text so we don’t have to show custom pops.   
    - Sam: It replaces the continuation API.   
  - Sam: On the topic of adding more attributes, that makes sense. We would like to work with you on that. So far, we’ve picked a non-extensible set. Would that be sufficient? We expect the subset we’ve picked to converge with OIDC standard claims union with HTML autocomplete taxonomy.  
    - Michael: That would be awesome. There are other FB-specific things that we might want to consider.  
    - Sam: Would they fit into HTML autocomplete?   
    - Michael: Probably. Need to think about it.  
  - Sam: The multi-IdP question is something we’d like to work with you on. We haven’t found an idea that works for everyone. There are a lot of variations and ways we can go about it. The navigator.credentials.add might be useful, but we aren’t sure how to make the account chooser dynamically change its UI as new accounts are discovered. The other option is to have the RP use another method. Another idea is to pick a browser event (e.g., all browser SDKs have to pick their config on load)  
  - Emelia: the flow that facebook is using that RP is opting-in.   
  - Sam: You might be interested in [https://github.com/fedidcg/idp-initiated](https://github.com/fedidcg/idp-initiated) also (it is not yet in origin trials, but the utility may be of interest).  
  - Nicolas: super cool facebook implemented FedCM. Customizable scopes … is that something that you’d want to show the disclosure text?  
  - Michael: yeah, that was the intention … I'm not sure we’d be allowed to have an arbitrary disclosure text, but we could add “birthday” to the “fields” API and that would do … growing list …  
  - Nicolas: Yeah, the second one is reasonable too, you want that to show in the account chooser?  
  - MIchael: Yeah, per IdP, RP-agnostic … Christian said that we could just omit … with the existing spec …  
  - Nicolas: The third one also seems reasonable … just a matter of implementing something … minimum seems more important … that seems like a very reasonable request … \+1 on the multiple IdPs options … we have been talking to the Sign-in with Google team to figure out options … finding a better path for independent IdPs in a single RP …  
  - Emelia: I noticed that you used passive mode a lot, is that the preferred one? Or are you also using other flows? One of the options that the RP can configure … there are a few configuration options … active vs passive …   
  - Emelia: Other question, are your clients pre-registered, or dynamically registered with CIMDs?  
    - Answer: pre-registered and regulatory requirements there.  
  - 

## Discussion (10 minutes)

## Any Other Business (AOB)

* 

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* Christian Biesinger (Google Chrome)  
* Nicolás Peña Moreno (Google Chrome)  
* George Fletcher (Practical Identity LLC)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Sam Goto (Google Chrome)  
* Emelia S  
* Isaiah Inuwa (Bitwarden)  
* Ben Kelly (Meta)  
* Tim Capallii (Auth0)  
* Simone Onofri  
* Michael Jasper (Meta)  
* Phil Smart (Shibboleth/Jisc)

