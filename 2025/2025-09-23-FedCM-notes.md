# FedID WG/CG Telecon, 2025-09-23

* Moderators:  Wendy

* Scribe: Phil

* Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* 

  Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (5 minutes) \*  
* Issues & PRs  
  * [Authentication methods on id assertion endpoint too limited (only cookies, which are bearer tokens) \- service-worker mode \= "all"? \#80](https://github.com/w3c-fedid/FedCM/issues/80)  
  * [Lock subframes to same identity as parent frames \#782](https://github.com/w3c-fedid/FedCM/issues/782)  
  * [Say something about caching \#781](https://github.com/w3c-fedid/FedCM/issues/781)  
  * [Lack of generic params on login\_url is limiting, unclear privacy value \#778](https://github.com/w3c-fedid/FedCM/issues/778)  
* Any Other Business (AOB)

# Notes

## Administrivia

* Wendy:  
  * Reminders. This is the Federated Identity WG and Community Group. W3C code of conduct.  
  * 

## Ecosystem Updates 

* Any ecosystem updates. None.

## Issues & PRs

### [Authentication methods on id assertion endpoint too limited (only cookies, which are bearer tokens) \- service-worker mode \= "all"? \#80](https://github.com/w3c-fedid/FedCM/issues/80)

* Emily:  
  * Long running issue. Off and on conversations.   
  * Will will give the latest  
* Will:  
  * MS is looking for FedCM extension points for the IdP portion. The service worker seems the best place.  
  * Use POP tokens, use proof from the OS about cookies.  
  * Need a hook to add their POP header.  
  * A service worker can also do throttling and caching.   
* Wend:  
  * Comments?  
* Sam:  
  * Driving…thanks for the feedback so far  
  * I agree this would be constructive, and I understand the extensions use case, but do not understand service workers enough to understand that use case.  
  * How does the browser find the service worker?  
* Will:  
  * IdP registers the service worker  
  * (PS, did not catch all of that)  
* Sam:  
  * Maybe another alternative is to expose an extension API for FedCM?  
  * Do not understand the need from the protocol perspective, but Aaron was finding other alternatives.  
* Will:  
  * This is for the IdP cookies, not the RP cookies.  
* Aaron:  
  * Can do this with DPOP for RP cookies.  
  * But this is for IdP cookies, which is a different story, and using the service worker makes sense to me.  
* Sam:  
  * OK, that is validation, this is a useful proposal. Let me have a few weeks to understand this issue.  
* Will:  
  * Sounds good.  
* Emily:  
  * Suresh is not on the call. No other browser engineers on the call.  
* Sam:  
  * It will be a big chunk of work to use service workers, but another engineer working on this would be good to provide this feature.  
* Emily:  
  * Any concerns about adding this to the spec?  
* Nicolás:  
  * Implementation for this might be simple: modify the Fetch to allow service workers. In the spec, we do not currently allow service workers. But we need to talk to someone about the privacy and security of the change. Adding service workers might introduce potential concerns from that side.   
  * The other thing, will this be backwards compatible? Probably, but worth thinking about. But even if not, it seems a reasonable request.  
  * I need to talk to someone who understands service workers better.  
* Wendy:  
  * Way forward: open to including service workers, the problem that needs solving is understanding. We need to investigate how that works in practice.   
* Will:  
  * Service workers are a local JS proxy that operates in the context of an IdP domain. The proxy enables the IdP to cut off the request, reply with cached data, or augment the request with additional params.  
* Nicolás:  
  * Can it also change the domain of a request?  
* Will:  
  * Can issue requests to other domains, but those would not be credentialled (unless enabled).

  ### [Lock subframes to same identity as parent frames \#782](https://github.com/w3c-fedid/FedCM/issues/782)

* Emily:  
  * This relates to a conversation last week: when showing permission, which origin do you show, the iframe or the parent?  
* Will:  
  * This is about ‘super-apps’, i.e., apps that contain other apps (like Teams or Copilot). The inner app needs to use the same Identity as the outer app.   
  * Users still get the opportunity to consent. Do not want different identities on the outer app and the inner app  
* Nicolás:  
  * You could do this, you send the login\_hint from the top level to the iframe.  
* Will:  
  * Requires you to share the login\_hint, and disclose this to the iframe before the user has consented.  
* Nicolás:  
  * Undesirable for the sub frame to know the user before the user has logged in to that sub frame.  
  * Param on iframes that only shows accounts used in the top level.   
* Will:  
  * Could be a permission policy.  
* Peter:  
  * Top level parent locks to that sign-in for the sub frames.  
* Nicolás:  
  * How do you ensure the top level shows FedCM first?  
  * Only load the iframe after the user has logged-in?  
* Will:  
  * Co-pilot will only render the document when you're already speaking to it, so only then shows the iframe.  
* Peter:  
  * We force this on nested applications, only use the sign-in from the parent.  
* Nicolás:  
  * Multiple accounts: do we only show the last used account, even though it might not be the same as the logged in account using a different sign in method?  
  * Many edge cases to get this feature right.  
  * We do not know the account of the logged-in user, hence the use of the login\_hint.  
* Will:  
  * The login\_hint is used before the identity credential is obtained.   
* Nicolás:  
  * Yes, login\_hint is used before obtaining the identity credential. But talking about the iframe.  
  * Needs more thought about whether it would work. Log me in with the parent ID.   
* Yi:  
  * What user journey do we want to support here?  
  * User using [a.com](http://a.com), sign in to [idp.com](http://idp.com) or other credentials?  
* Will:  
  * Signed into [a.com](http://a.com) from [idp.com](http://idp.com). [a.com](http://a.com) has plugins, so the user enables [b.com](http://b.com). When [b.com](http://b.com) wants to log in with [idp.com](http://idp.com), it shows all the accounts. But I want to restrict that to what [a.com](http://a.com) used or no account.  
* Yi:  
  * If IdP only supports single session, this is solved.  
* Will:  
  * Assuming IdP supports multi-sessions.  
* Yi:  
* Will:  
  * Still need some prompts for privacy, but make it a yes/no rather than select your user.  
* Yi:  
  * If the user selects ‘bar’ from the inner iframe, and a and b are cross-site. The IdP will learn the iframe origin and the top-level origin after account selection. IdP can then make a decision, the user is using account ‘bar’ and then can use continue\_on to allow them to select account ‘foo’.  
  * Adds user friction.  
  * Does that make sense?  
* Will:  
  * Want to eliminate the friction.  
* Yi:  
  * So you want to add a string to the policy?  
* Will:  
  * Yes, allow FedCM but no account selection.  
* Yi:  
  * [b.com](http://b.com) is totally new to the browser, so needs to show some consent.  
* Will:  
  * Yeah, but could be a reduced UI prompt.  
* Sam:  
  * What do you do today, without FedCM?  
  * And, what is the desirable user experience, prompt or no prompt?  
    * Not sure there is a privacy concern here.  
    * The inner frame can know what the identity already was  
* Will:  
  * We use post messages to share login\_hint between frames  
* Sam:  
* Will:  
  * We keep a refresh token in the top frame. The inner frame asks outer frame to make request on its behalf  
  * FedCM we would like inner frame to talk directly to the IdP  
* Sam:  
  * But the post messages are OK?  
* Will:  
  * entraId token for Office flows through CoPilot to Office.   
  * We want Office to talk directly to Entra  
  * With FedCM, want to improve security by preventing the token flowing across the threat/security boundary   
* Sam:  
  * This seems like a reasonable feature request. No privacy boundary broken.  
  * Maybe we can auto-grant.  
  * Assume the user is already logged-in to the top frame. (Will, yes). So once that is done, we are not extending the privacy boundary by allowing the sub frames to use it.  
* Nicolás:  
  * Does the top-level want the plugins (in sub frames) to be automatically logged in?  
* Will:  
  * Yes  
* Nicolás:  
  * You could transmit the information you need…already. Need to find out Chrome’s privacy standpoint on this.  
* Sam:  
  * I think this does not break any privacy boundaries.  
  * And if this is a usable API, this could be a feature  
* Will:  
  * FedCM gives us a security improvement; this gives us a usability improvement.   
* Sam:  
  * My assumption is that you are already signed in to the IdP on the top level. If so, this seems reasonable.  
* Will:  
  * Make that explicit in the issue

  ### [Say something about caching \#781](https://github.com/w3c-fedid/FedCM/issues/781)

* Will:  
  * Work out how caching works in the spec. I think because it uses Fetch it implies cache-control works as normal. If the accounts or id\_assertion endpoint adds a cache-control, the browser would honour it, and the browser would return the same assertion without making more requests to the IdP. Is this correct?  
* Nicolás:  
  * Can you repeat  
* Will:  
  * Spec uses Fetch, if the IdP returns a 1 hour token and a cache-control max-age of 1 hour, if the next FedCM request, would it use the cached token or not.  
* Nicolás  
  * Not sure. Would an IdP do that?  
* Nicolás:  
  * Would it cache the token response?  
* Will:  
  * Yes in MS land.  
  * We want to do this in FedCM.  
  * As the IdP, I want those to be served from cache.   
* Nicolás:  
  * Opposite of what I was thinking.  
  * I think it would work, if it was the same request. I am wondering…the clientId would need to be the same, etc. If all things are the same, I think the cache is enabled.  
* Yi:  
  * I tested the accounts endpoint. Max-age, there is a cache. But not tried the id\_assertion endpoint, but assume it works the same way.  
  * Only the accounts and id\_assertion endpoints are cached in Chrome today. Not support caching client metadata fetch.  
* Sam:  
  * Why?  
* Yi:  
  * Not sure why.  
* Sam:  
  * Intention was the cache. But not all things are cached. Intention is to respect caching headers, but perhaps in implementation we are not right now. Need to revisit.   
* Yi:  
  * Christian added a patch to support this.  
* Will:  
  * Add a few examples to the spec to show the IdP how to do that.  
* Sam:  
  * Will, please add a PR for the spec on that.  
* Nicolás:  
  * Just an example, not changing how Fetch works  
* George:  
  * From a spec perspective, FedCM follows the standard HTTP caching semantics. Not sure whether we should say how we should do it.  
  * If the user has logged out but FedCM uses a cache response, this is not great.  
  * So hesitant to allow this.  
* Will:  
  * Accounts endpoint and some uncontroversial endpoints make sense.   
* George:  
  * What the spec says and what goes into an implementation guide can be different.  
* Phil  
  * Not to take away from these use cases, but setting cache-control no-store is, I thought, common for IdPs. 

  ### [Lack of generic params on login\_url is limiting, unclear privacy value \#778](https://github.com/w3c-fedid/FedCM/issues/778)

* Wendy:  
  * Thanks, Will, for the issues  
* Will:  
  * Maybe the implementation already addresses this  
  * If you are logging into a high-assurance RP, you might need appropriate authentication on the IdP.  
  * We might need to send somebody through continue\_on to perform higher assurance authentication, for example.  
  * Is this allowed for adding another account?  
* Nicolás:  
  * We are supposed to be doing…if the user has clicked on the browser UI, there are cases where we open the login URL without meaningful user interaction.  
  * Make sure spec and implementation align  
  * Could be weird that the login\_url has the params they need and sometimes not.  
* Will:  
  * Would be nice to add the params all the time  
  * This is what happens today for other protocols.  
  * Be nice if an RP could allow this, and they would always be sent  
* Sam:  
  * Held FedCM to a higher privacy bar.  
  * We need to make it work without 3PC.   
* Will:  
  * Even in Safari I can window.open  
* Sam:  
  * Yeah. But held the bar higher than the link decoration.  
  * Needs meaningful user consent. Held that bar other than add another account UI  
  * Single factor in account choosing and second factor in continue\_on  
* Will:  
  * Company admin can say only use FIDO credentials to access email  
  * User can end up having multiple logins  
  * Just want the FIDO key the first time and just use that in the first prompt.  
* Sam:  
  * Yeah, this is not ideal UX.   
* Will:  
  * It would be nice if there was a permission policy that specified which privacy bar you want FedCM to operate under.  
* Nicolás:  
  * It could be a tracking mechanism that is used. Careful about adding this.  
  * First, align the spec.  
* Emily:  
  * \+1 on the friction on this. I would like an IdP-focused design group. Which identity protocol methods and how they could or could not work with FedCM.  
* Wendy:  
  * Happy to help IdPs with this.  
  * Thanks

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Wendy Seltzer (co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* Phil Smart (Shibboleth/Jisc)  
* Chris Needham (BBC)  
* Aaron Parecki (Okta)  
* Gorman Ho (Okta)  
* Alex B Chalmers (self)  
* Nicolás Peña Moreno (Google Chrome)  
* Yi Gu (Google Chrome)  
* Peter Zenzerovich (Microsoft)  
* Will Bartlett (Microsoft)  
* Emily Lauber (Microsoft)   
* Michael Jones  
* Sam Goto  
* George Fletcher (Practical Identity LLC)  
  