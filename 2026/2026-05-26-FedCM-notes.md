# FedID WG/CG Telecon, 2026-05-26

* Moderators:  Heather Flanagan

* Scribe: Heather

* Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

* Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * [FedID CG/WG process](https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md)  
* Ecosystem Updates (0 minutes)  
* Discussion (55 minutes)  
  * [Enabling IDP Interception in FedCM Request \#815](https://github.com/w3c-fedid/FedCM/pull/815)  
    * Continuing the discussion from [19 May 2026](https://github.com/w3c-fedid/meetings/blob/main/2026/2026-05-19-FedCM-notes.md). Please review both the meeting minutes and [https://github.com/w3c-fedid/FedCM/blob/main/explorations/identity\_handler.md](https://github.com/w3c-fedid/FedCM/blob/main/explorations/identity_handler.md)  
* Any Other Business (AOB)

# Notes

## Administrivia

* W3C Code of Conduct

## 

## Ecosystem Updates (0 minutes)

## 

## Discussion (55 minutes)

### [Enabling IDP Interception in FedCM Request \#815](https://github.com/w3c-fedid/FedCM/pull/815)

#### Summary of last meeting:

##### Service Worker Integration (PR815)

* Microsoft customers requesting service worker support for three scenarios:  
  * Proof of presence authentication (similar to DPoP)  
  * IDP outage handling with cached responses  
  * Proxy for servers not yet FedCM-ready  
* Technical challenge: FedCM requests don’t originate from pages, breaking normal service worker flow  
* Three approaches evaluated:  
  * Approach A: Flip service worker mode (doesn’t work \- no controlling client)  
  * Approach B: Browser-layer fetch event creation (rejected by service worker WG)  
  * Approach C: Payment handler-style functional event (current proposal)

##### Security Headers Discussion

* Key concern: preserving sec-fetch-dest: webidentity header through service worker  
* Current fetch spec limitations reset destination/origin properties when requests pass through service workers  
* Resolution: Don’t need to preserve sec-fetch-dest for now  
  * IDPs can check sec-fetch-site: same-origin instead  
  * Existing IDPs already have CSRF protection via double-submit cookies  
  * Can add dedicated FedCM fetch API later if needed

##### Open Design Questions

* Three remaining areas needing group input:  
  * IDP service worker registration process  
  * Event dispatch shape (fetch event vs dedicated event vs reuse existing)  
  * Security properties preservation  
* Microsoft’s DPoP-like implementation requires:  
  * Local OS calls (not network requests)  
  * Multiple fetch calls per handler for nonce retrieval  
  * Retry pattern when nonce expires

#### Meeting notes:

* Suresh: Have some follow up questions re: properties. See issue [https://github.com/w3c-fedid/FedCM/issues/833](https://github.com/w3c-fedid/FedCM/issues/833). Do we need to preserve the cookie scope variant?  
* Christian: Did we decide if SW needs to be partitioned or if it can be the same as used for regular requests? If it can be the same, no security benefit from limiting the cookies.  
* Ben: The main thing pushing us to have a partitioned set of SW registrations is trying go accommodate sec-fetch-dest, which we dropped, so we don’t need partitioned SW. If you’re already in the SW it can make a fetch somewhere else. If you’re in the SW with the origin of the IdP, it can do anything it needs back to itself.  
* Suresh: Follow up questions from Dominic \= why is client metadata request not to be intercepted in the SW workflow? I responded in the issue. Client metadata should not be allowed to intercept.   
* Ben: How is client metadata normally sent? Is it in a header or something else?  
* Christian: Client metadata is a get request with origin header and client id in query part of the URL. You don’t want it intercepted because it would allow the SW to annotate the credential request with the RP information and we don’t want that. We don’t share the RP info until the user has accepted the dialogue.  
* Ben: Is that consistent with the three goals of the SW? That this info will be lost in the offline use case, legacy use cases? It seems like a requirement that we can’t use this mechanism for that.  
* Christian: You lose the privacy policy in terms of service in the dialogue.  
* Sam: Why do we care about the client metadata endpoint? Is that out of scope for SW?  
* Suresh: It is out of scope, but Dominic asked.  
* Sam: We can’t do the client ID metadata because it reveals the client ID which is a privacy violation  
* Ben: So we aren’t losing anything in the goals. Probably use SW None for those requests.  
* Suresh: next question on client restrictions. Currently, all the FedCM requests have redirect=error. We only allow the written types of defaults. Dominic is asking why this restriction is needed.  
* Christian: If you don’t send sec-fetch-dest it is not as important.   
* Suresh: So we don’t have to have any written type checks in the SW?   
* Christian: What does type mean in this context?  
* Suresh: When any response we fetch back, there is a property called “response type” which gets created on the fly. If the response is coming from the IdP, the type is default. If from a third-party URL, then the response will be something else that is opaque. To enforce the redirect error rule, made it specific that only the response of “default” should be allowed.   
* Ben: The options are that it’s a CORS response or an opaque no-CORS response. You can handle those differently. But why is redirect error there at all? What are you trying to protect?   
* Christian: the original reason predates the SW discussion. If you have an attacker IdP and your own account endpoint that returns a fake ID, then your redirect points to Google. The user only sees the fake account but Google is tricked into thinking it’s a legit query. This line of attacks only works if you can consume the sec-fetch-dest, which is why it’s disallowed in regular FedCM. With SW, the attack vector is different. If we don’t keep sec-fetch-dest, then when you make a request of another IdP, the IdP would not treat it it as a FedCM request. So we probably don’t have to worry about this here.  
* Ben: We talked about requiring fetch mode to be same origin, so if it tries to go cross-origin  it would fail anyway. We would allow same-origin redirects.  
* Christian: Same-origin redirects are fine.   
* Ben: if we rely on same-origin request to IdP, that takes cross-origin requests off the table and we don’t need to make special requests for it at the SW level.   
* Suresh: Then we don’t have to have this rule followed any more.   
* Ben: Correct. What Dominic is going for that any special case we can remove would be useful.  
* Suresh: Re: SW restrictions. In the explainer, there are two approaches. One where in .well-known file there would be a handler. Second is like a payment handler \- when an IdP does a restriction.  
* Ben: There is a third option similar to the old approach of foreign fetch which includes a link header. Big question with .well-known file \- when would the browser know to go read it?  
* Christian: When a FedCM request is initiated, it looks for the .well-known file. FedCM only works if you visited the IdP before; the IdP can at that point register the SW. So why does it need to be specified in the FedCM files?  
* Ben: Hypothesizing one scenarios \- how do you persist the ever-visited-IdP rule? The browser can evict the SW if it runs out of resources.  
* Christian: It’s not so much that ever-visited is a rule. You have to be logged into the IdP for any FedCM request to work.   
* Ben: So, the issue is SW are in separate storage than cookies and have different lifecycles. It would probably mostly work if we assume they are in sync, but unless we enforce that you’ll have corner cases.  
* Christian: If you register the SW as part of the FedCM flow, you have to wait for the registration to finish, which is an extra step, and adds to the complexity. Doable, but worth noting.  
* Ben: Also worth noting the issue of onboarding. If visitors have already visited and signed in, you’d have to force them through an SW flow later.   
* Christian: FedCM has a passive mode and an active mode. One gets triggered at page load, the other when the user clicks on login.   
* Suresh: The way MS wants to use FedCM via SW is they’d be using passive mode. The user hasn’t been restricted to an IdP yet so the request would fail. As the user is getting registered, that’s where the SW registration would happen.   
* Ben: I think that’s a good place to start. A backup plan is, since .well-known is already read, include something to install the SW as part of the .well-known.  
* Sam: What happens on fetch when the SW hasn’t been registered before?  
* Ben: You’d get whatever FedCM does without an SW, so however fetch is defined in FedCM is what you’d get.  
* Sam: but would the browser know if it was intercepted by an SW?  
* Ben: The browser will know, but will the service get something different? Since we won’t preserve the destination, the service will know if it came from an SW or not.  
* Sam: Will the IdP need to support an SW and a service endpoint?  
* Christian: It wouldn’t work until you registered the SW.  
* Sam: If we launched this today, there would be a lot of users logged in but who haven’t registered the SW. In that case, we’d be making a fetch request to account endpoint that would not be intercepted by the SW.  
* Christian: That question has assumptions we need to verify. Does the MS IdP require the user to re-login periodically? Do they already have a SW for unrelated purposes? That impacts the answer to Sam’s question. If the answer is “yes” to either, then this will be resolved relatively easily.  
* Suresh: I will take this back to the IdP team and ask.  
* Sam: Passive mode is optional, so if the SW isn’t registered and there is no endpoint, then we would fail and be semantically correct. Maybe that’s not a problem. In active mode, it requires that we take you to the login URL if you’re logged out. So maybe this isn’t a big deal. So, Ben’s proposal is to use the IdP registration at the moment you visit the IdP as the main way to register the SW. There are some difficulties with the corner cases between cookie/SW storage lifecycles. If we find that is too much, we can fallback to registration being done in .well-known since we make .well-known requests frequently.  
* Ben: Beyond the bootstrap scenarios, we need to think about when the SW is evicted/uninstalled by the browser. In that scenario, you’d like to re-install the SW. You’ll want something different in the request to make sure you know if something is coming from the SW (by using destination?) or something else.   
* Christian: the SW could add a special header.  
* Ben: The IdP could do something themselves, but they need to know they have to do that.   
* Christian: The primary part of the SW is to allow special cookie handling. So this should be fine. How often do we think eviction happens? Is it rare or not?  
* Ben: When it happens, all the origin storage goes away atomically. The inverse could also happen with cookies being wiped but origin staying. More common on mobile than desktop.  
* Sam: What do you mean by SW installation and eviction? Is it an expensive process? Or can it be put in the middle of an http flow, or is there the need for user permission?   
* Ben: It’s not lightweight, but how heavy weight depends on the origin of the SW. It’s an async process \- you trigger the registration through the API, then it will go out and fetch the SW script, then parse/run the script in a new worker thread, then an install event on that thread which may do arbitrary things. It’s all in the background so is probably fine. When all that’s done, it will go to the activating stage. So, probably a second or less, but more than tens of milliseconds. An IdP could do something expensive here.   
* Sam: Not worried about the IdP taking a long time; there are no incentives to slow them down. Outside any developer bug, is the rest of the process lightweight? If the IdP is making it fast, could it make it under a second?  
* Ben: depending on network speeds,  yes. The important thing here is whether there is a requirement that the FedCM request after .well-known goes through the SW. If that’s a hard requirement, you have to make sure old versions of the SW have exited and if there are things its keeping alive are resolved. Is best-effort enough?  
* Christian: Because they add the special proof-of-possession cookie handling, if you don’t go through the SW it will fail because it doesn’t have the correct information.  
* Sam: I’m working under the assumption that the browser has to make sure the SW is operating, installed, working as intended. Will MS also expose a FedCM endpoint, or will it rely entirely on SW?  
* Christian: AIUI: There has to be a URL but iIf you fetch the URL directly without the SW it will fail.  
* Suresh: Not sure, will ask.  
* Ben: I don’t have a specific concern, but you will need to hook into SW versions and installing process, and you should write into the spec that you have to wait for it to complete and activate. But SW was designed as a best-effort thing.   
* Christian: With passive mode, we can ignore this issue. We can start a process and don’t have to wait. For active mode, then we’ll have to wait.  
* Sam: If we made it so the IdP is forced to expose an http accounts endpoint, then when it doesn’t get a special DPoP header, it can send response to the browser so it degrades gracefully. We shouldn’t assume SW are always working.   
* Christian: What does “degrades gracefully” mean?   
* Sam: I am assuming there is an accounts endpoint in the file, but I’m assuming the server doesn’t have to implement an accounts endpoint. That the degrade response will be the responsibility of the IdP and the instructions in the account endpoint.   
* Christian: Still not sure what degrades gracefully means. If the accounts endpoint returns an error, in active mode we’ll show the login page.  
* Sam: Maybe that’s the graceful degradation. We should assume SW is a best effort, not guaranteed.  
* Ben: Should also consider that some sites are concerned about pushing a bad, buggy SW. Will need a fallback scenarios so the IdP can install the fixed version of the SW. How do you recover from a buggy SW?  
* Sam: This is a lot of homework for Suresh\!  
* Suresh: It would be if IdP does the registration and FedCM can assume that things will flow smoothly. There should be no fallback at all.   
* Christian: That the registration happens when the user logs into the IdP.   
* Ben: That works if you consider the SW as a best effort. You can have your flow wait until it’s activated, but you need to consider other paths.  
* Heather: What do we need to do in the next four minutes?  
* Ben: to document all our decisions in the GitHub issue, and to highlight the new questions about the fallback scenarios.   
* Suresh: will do that in Dominic’s issue. 

#### Next Steps

* Suresh to update GitHub issue with agreed decisions  
  * Document security property resolutions  
  * Capture redirect handling changes  
  * Note service worker partitioning decision  
* Investigate Microsoft IDP requirements  
  * Check re-authentication frequency patterns  
  * Determine existing service worker usage  
  * Clarify fallback scenario handling  
* Design fallback mechanisms for service worker failures  
  * Bad deployment recovery process  
  * Eviction scenario handling  
  * Best effort vs guaranteed service worker operation model

## AOB

* 

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Sam Goto (google chrome)  
* Christian Biesinger (Google Chrome)  
* Suresh Potti(Microsoft Edge)  
* Ben Kelly (Meta)  
* Emelia Smith (joining later)