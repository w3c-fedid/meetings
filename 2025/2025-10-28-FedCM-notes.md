# FedID WG/CG Telecon, 2025-10-28

* Moderators:  Heather

* Scribe: Wendy

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
  * [Allow IdP registration and RPs to match on a "type" \#1](https://github.com/w3c-fedid/idp-registration/issues/1)  
  * [Make it easier to deploy this at the eTLD+1 for registered IdPs \#10](https://github.com/w3c-fedid/idp-registration/issues/10)  
  * [Why must SameSite=none? \#587](https://github.com/w3c-fedid/FedCM/issues/587)  
  * [globalObjects should be the top level window, rather than the cross site iframe when Permissions Policy is used \#729](https://github.com/w3c-fedid/FedCM/issues/729)  
* TPAC Planning  
  * [Draft agenda](https://docs.google.com/document/d/1KWzykDBBfD67fQrJXFPlQGe6tWSblY6VDK3jmyMMfYY/edit?usp=sharing)  
* Any Other Business (AOB)

# Notes

## Administrivia

* We rejected the help of the “AI Companion”  
* Heather: Reminders: WG/CG membership, code of conduct

## Ecosystem Updates 

* \[none\]

## Issues & PRs

Heather: 4 issues from our blocker list. [https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-(Consensus-Blockers-for-CR)](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-\(Consensus-Blockers-for-CR\)) What do we need to do to make progress? 

### [Allow IdP registration and RPs to match on a "type" \#1](https://github.com/w3c-fedid/idp-registration/issues/1)

* Nicolas: What is the CR blocker?   
* Heather: Aaron submitted as a concern in 2024 before FPWD.   
* Nicolas: This requires IDP registration, which is not yet specified. Don’t think it’s controversial in itself, but haven’t in Chrome fully aligned on API shape. Happy to hear thoughts.  
* Phil: On the type, you can say “my IdP supports this type”, a protocol or variant, and FedCM would filter on those types depending on what RP supported. Does the type get sent to IdP when a request is made? FedCM has one endpoint that may support multiple protocols. I’d be more familiar with scenarios with multiple endpoints for diff protocols. Is it sent in the request? If not, would it make sense to send in the request?  
* Nicolas: I don't think it’s sent in the request today, but don’t see a reason why we can’t. Please add a comment to the issue.  
* Phil: Thanks, can do.   
* Sam: Re: type, open question is whether that’s something that gets written at registration time or pulled dynamically at request time. Leaning toward the latter (request time). Could go either way but different properties at write or read time. Whether it lives in .well-known or .config URL, or registration parameter  
*  George: Those are pretty wide extremes. IdP could do more than when it first registered somebody. If you go to a more dynamic pull, there should be a caching model. Every time seems like overkill.   
* Sam: Caching matches my intuition. If you want to add a new type that you support, you don’t need to have the user come to your site to update. Leaning toward not having a user prompt at registration. Dynamic loading comes with performance cost while loading API.  
* Sam: Another open design question on type is whether string is sufficient. Some IdPs might want something more granular. Starting with a string seems reasonable.   
* Phil: String for now seems OK.  
* Sam: One action we can take is sending type to assertion endpoint. Everything else we’ve discussed is implemented, I think. 

### [Make it easier to deploy this at the eTLD+1 for registered IdPs \#10](https://github.com/w3c-fedid/idp-registration/issues/10)

* Nicolas: I think Sam has been looking at DNS for other reasons, there are a lot of edge cases. Not much precedent for platform APIs to use DNS. And if there’s no configURL …  The latest thinking is that neither of the two proposed ways to deploy works.   
* Sam: Still gathering info on DNS for another feature, but not lots of precedent. We haven’t reached major roadblock. Could still explore it as an option  
* Heather, chair hat off: if you put something like this in DNS and DNS fails, what happens?  
* Nicolas: You’ve got other problems. More about the design choice, do you put a high-level concept in such a low-level place? I would need a compelling reason.  
* George: We had this issue with WebFinger as well. There, allowed for redirects. If you hit one, it could redirect you to the correct endpoint. Still brittle, but configurable in networking gear. Tricky at AOL because the identity team didn’t own the .well-known at a key domain. Redirect worked if we could keep it there (sometimes people deleted it without understanding).   
* Sam: I think we do allow redirects for .well-known. Might have to be the same-site, eTLD+1.  
* Christian: We allow redirects for .well-known.  
* Sam: I think we allow them arbitrarily.  
* George: Curious why that’s insufficient?  
* Sam: Sometimes difficult to do, e.g., apex domain on GitHub pages, doesn’t allow me to set redirect rules, nor set media types for JSON. Catering to small developers. Apex domain as a static site.   
* Christian: What does a typical small site use? Do they allow redirects, etc?  
* Tim Capelli in Zoom Chat: Cloudflare Pages support specifying media types and redirects.  
* Sam: Wordpress might be another, with a bit more flexibility. Let’s get more info from Aaron.  
* Nicolas: We need to hear more from people who use the API. We need the devs who consider these blockers to be part of the discussion. 

### [Why must SameSite=none? \#587](https://github.com/w3c-fedid/FedCM/issues/587)

* Christian: An update. There’s been a bit of discussion on the issue. I’ve been pointed to the correct place in the spec, and Anne seems open to the change. No one seems opposed. I’m working on prototyping in chrome. Hope to have it done in the next couple days so people can test in canary. Then we can work on specifying it, and review by Fetch spec owners.   
* Sam: For clarity, we’d also allow same-site=lax.   
* Christian: Yes.

### [globalObjects should be the top level window, rather than the cross site iframe when Permissions Policy is used \#729](https://github.com/w3c-fedid/FedCM/issues/729)

* Christian: we wanted to close as won’tfix.  
* Nicolas: Emily made a recent comment.   
* Nicolas: Login hint should work?   
* Emily: E.g., top frame has SharePoint, with embedded frame for Word. It would be confusing if the two had different accounts logged in. More than hinting, it would be useful to lock them together. E.g., the tooling for Sharepoint doesn’t have user-friendly URLs, the user doesn’t meaningfully differentiate. Don’t want them logged into different accounts.   
* Christian: Why not have backend communication for the login?   
* Emily: They often have different domains, even different owners. E.g., SalesForce can embed Word.   
* George: Interesting use case, distinct from the one I’d commented on in the issue. My concern: the IdP, when it gets to the request, wants to know the originator, since it may have different policies per-RP. Both are important. Could also imagine places where they can’t be locked, e.g., you don’t have 1:1 match between your SharePoint and Salesforce IDs.   
* Christian: Three different questions: what gets sent; what domain is shown; what accounts can the user choose? How do you lock the iframe to the same identity without FedCM?  
* Emily: I’ll continue talking about Office. We have a feature called nested app authentication, inside the MS auth library for JS, forces brokered relationships. Office add-ins are required to use the MS plugins so we handle the locking.   
* Christian: Do you exchange a token?   
* Emily: Parent fetches a token for the child, knows what child requested it, and passes info to IdP. If there’s a built-in browser API, rather than us forcing use of SDK, that simplifies the developer experience.    
* Nicolas: Today, do you show the account chooser twice?  
* Emily: Depends on scenario, setup.   
* Sam: It would be useful to see some screenshots of this.  
* Emily: To be clear, we’ve tried to avoid having to show multiple permission dialogs.  
* Heather: Maybe we can get this shown on-screen at TPAC?  
* Emily: Yes, I’ll pull some examples together.

## TPAC Planning

* Heather shares: [TPAC 2025](https://docs.google.com/document/d/1KWzykDBBfD67fQrJXFPlQGe6tWSblY6VDK3jmyMMfYY/edit?tab=t.0#heading=h.zmolg8b23oo)  
* Heather: Thursday is FedCM focused. \[reviews draft agenda\]  
* Member-visible TPAC registration list: [https://www.w3.org/register/tpac2025/registrants\#meeting-455](https://www.w3.org/register/tpac2025/registrants#meeting-455)  
* Sam: 3.5 hours sounds like a lot of time.   
* Heather: Please make suggestions in the doc\!

## AOB

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan  
* Wendy Seltzer  
* Joel Antoci  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Sam Goto (Google Chrome)  
* George Fletcher (Practical Identity LLC)  
* Emily Lauber (Microsoft Identity)   
* Phil Smart (Shibboleth/Jisc)  
* Nicolás Peña Moreno (Google Chrome)  
* Christian Biesinger (Google Chrome)  
* Tim Cappalli (Okta)  
* Mike Jones  
* Bjorn Hjelm (Yubico)