# FedID WG/CG Telecon, 2026-06-09

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
* Ecosystem Updates (10 minutes)  
* Discussion (45 minutes)  
  * [Enabling IDP Interception in FedCM Request \#815](https://github.com/w3c-fedid/FedCM/pull/815)  
* Any Other Business (AOB)

# Notes

## Administrivia

* W3C Code of Conduct

## 

## Ecosystem Updates (10 minutes)

* (hold for next week)

## Discussion (45 minutes)

### [Enabling IDP Interception in FedCM Request \#815](https://github.com/w3c-fedid/FedCM/pull/815)

* Suresh: See the update to our action items here — [FedID WG/CG - FedCM - Notes](https://docs.google.com/document/d/1sXG7AdDO61nMSyO9Z3eic5aCTyRfJmwmKGl4yrNrL0k/edit?tab=t.1wmr4wa572w3); notes added below for inclusion in today’s meeting minutes.  
* Ajay: I don’t have access to create a PR so I created notes. I have proposals for how to solve the SW problem and would like input from this group, then I will take it for internal Microsoft review.   
* Nicolas: Dominic asked this in the doc — what is the scope of the SW that you need? If the user visits Microsoft to login and we register a SW there, is that eligible for FedCM? Or do we need something specific for FedCM?  
* Ajay: Either would work. If there is an existing SW running, either FedCM doesn’t do anything (because the existing SW already does what’s needed) or it registers it again, which is fine.  
* Dominic: The tradeoff is that you have one existing SW that will need the correct identity handlers built in, as opposed to an SW that’s only keyed on the web identity file. Having one scoped to FedCM specifically might be cleaner, but not sure. Suggest taking this back to Alex Russell for input.  
* Nicolas: What did the SW working group say about this?  
* Suresh: They wanted to know which approach we were choosing and then they’ll give us advice.   
* Christian: If you do something that’s partitioned just for FedCM, I worry about the complexity. The SW code probably doesn’t do that right now, and it could get complicated.  
* Dominic: I agree; it’s best to avoid special keying. But we need to see if that complicates Microsoft’s angle on this. Let’s tentatively decide to avoid special keying and see if we run into problems.   
* Nicolas: That makes sense. For now, we can see how we would implement scoping using the IdP existing or matching SW that’s already registered. What about the soft update thing? Is that roughly equivalent to how SWs are updated today?  
* Ajay: There is an update method in SW that looks to see if the script has changed. If it hasn’t, it doesn’t do anything. The browser does this naturally once every 24 hours. We want to invoke it directly from FedCM browser code, and then the IdP is responsible for configuring the caching time.   
* Nicolas: So, today if we update an SW twice a day, the user would get only one of those updates?  
* Ajay: When we invoke the update command, it would do a bit-by-bit comparison. The browser also does the update operation at a 24-hour frequency. There is an API available to do this today.  
* Nicolas: The IdP cannot call this because they don’t have JavaScript; instead, it would be called in every FedCM call.  
* Christian: Couldn’t the SW itself call it?  
* Ajay: Even that SW script that is invoking these operations might need to be updated (e.g., if there is a bug). So if the update is called from FedCM, it will protect against that scenario. If the update is in the SW script, that could be broken, which is a bigger problem.  
* Nicolas: I don’t know how expensive this update check is.  
* Ajay: It won’t be used for the existing call; it would update it for the next call that happens. If it finds a change, it would load that.  
* Nicolas: That seems maybe ok. What if FedCM calls in the same minute? Would there be two checks for this?   
* Ajay: That’s what the IdP would control based on their caching configuration. If it makes a call to a server, it could get changed, but if the cached bit-by-bit comparison shows no changes, it will continue with the existing registered SW script.   
* Dominic: The cache could have been updated by a different call in a different tab. So you can’t avoid the byte-by-byte check because it exists in the cache; it will just be faster.  
* Heather: Any reason not to try this as an experiment?  
* Dominic: Has the SW group weighed in on this?  
* Ajay: We can ask, and I’ll also ask internally to Microsoft.  
* Heather: Let’s ask the additional experts to chime in.  
* Nicolas: My next question is for the staged rollout. How would this work in a staged rollout? One idea could be that the SW server would split its traffic into two.  
* Ajay: FedCM doesn’t need to do anything for a staged rollout. If there’s going to be a soft update operation on FedCM, that will facilitate what the IdP does.   
* Will: Are you thinking about calling import conditionally based on import script?  
* Ajay: That and the SW script itself.   
* Will: One of the things we worry about with rollout is “poisoning”. If you have a rollout at 5%, you want 5% impacted. If you roll out in a way that a 5% rollout impacts 50% of your users, that’s a problem. So we have something about affinity groups. I’m clarifying that we’re going to use that import script mechanism at Microsoft.  
* Ajay: Yes, we would need to use the import script on the IdP side. But we’ll need a way to fix that if there’s something wrong with the script.   
* Nicolas: The accounts endpoint is specified in the .well-known, but does that create an issue for the staged rollout? Technically, you could respond differently to the same account endpoint, so maybe this is fine, as long as the users are split via the SW. This is probably a Microsoft internal detail.   
* Nicolas: My other question was about eviction. Should the updates allow eviction? The SW can be removed by the user, but if that happens, they’ll have to log back in again. It sounds like everything we’ve talked about is handled by the existing proposal from Suresh? Or is there some part that needs changing?  
* Ajay: It’s additive to what Suresh has proposed. It helps clarify what happens on the SW side vs the FedCM side.   
* Nicolas: The only thing new to me is the forced update in the FedCM call, but other than that, the rest of the requirements seem to be handled?  
* Suresh: Yes, the rest of the things have been handled with regards to the security gaps.   
* Ajay: First question, “What does the desired state mean?” What is defined in the .well-known file takes precedence; it is the final source of truth.  
* Sam: Have we converged on having the SW isolated to FedCM requests or shared across all requests?   
* Dominic: Shared  
* Sam: So the registration in the browser could impact normal requests?  
* Ajay: The normal registration would not affect FedCM if it’s different.   
* Sam: So, FedCM will always define what’s in the .well-known file?  
* Ajay: Yes.  
* Dominic: If there’s an existing SW that matches the filename, what happens?   
* Nicolas: If it’s shared, it should use the existing one. It can’t be scoped just one way.  
* Sam: There is a requirement about it being fresh and recently installed. Is it ok for it to be shared and out of date, or does the browser always fetch the .well-known file and SW?  
* Nicolas: This is what we discussed earlier.  
* Sam: So if you visit ahead of time and get the SW in the .well-known, and you go to the IdP and kick off a FedCM request, what does the browser do?  
* Nicolas: You register the IdP, sw1, you will use sw1 for the FedCM request, and in parallel, the browser will run an update to make sure sw1 is up to date. If not, it will update it for the next FedCM request. It does not block the initial FedCM request; it remains a best effort.  
* Christian: If you were in a case where the SW is broken and you need to fix it, the initial request would fail and the next one would succeed.  
* Nicolas: The alternative of waiting for the SW to update would be a big performance hit.  
* Christian: If there is no SW, we need to wait for registration to finish.  
* Will: We care about updates over time, but we don’t care about it in terms of the number of requests. If the user can refresh the page 2-3 minutes later and the update will work, that’s ok.  
* Christian: What happens if it tries to update the SW and it gets an error back (e.g., a 404 or a connection refused)?  
* Will: If you cannot initialize the SW, that’s similar to if the .well-known file is missing.   
* Nicolas: You’d rather the request fail than go through the accounts endpoint without SW?  
* Will: Yes.  
* Nicolas: If you don’t have the SW registered, do you want to wait for the SW to be registered before we handle the request?  
* Will: The first SW registration is synced, the updates are asynch.   
* Sam: So we block on registration? But we heard that registration is a heavy process. Is it ok to block there?  
* Dominic: So the flow wouldn’t start immediately?  
* Christian: We’d also have to wait if it was triggered by the .well-known file.   
* Nicolas: Any IdP not using SW would not be impacted by any of this.  
* Dominic: Why is it a hard requirement for the registration to be done?  
* Will: Microsoft is doing a binding. If the SW isn’t there, we don’t get a binding assertion, and so we can’t respond in any other way than an error. If registration hasn’t happened, we make them retry.   
* Heather: What action items do we have now? To take this proposal to SW group and further to Microsoft  
* Sam: I’m having a discussion with Peter Zen (sp?) in Microsoft. Would like Suresh and Ajay to chat with him as well. This is an Android use case.  
* 

## AOB

***From Ajay’s doc:***

**\# FedCM Service Worker Registration and Lifecycle Model**

The FedCM Identity Handler proposal is still evolving. This document proposes a service worker registration and lifecycle model designed for production-scale deployment and resilience.

**\#\# Scenarios Considered**

This proposal considers the following scenarios.

**\#\#\#\# Long-Lived User Sessions**

After a user interactively signs in, the IdP session may remain valid for an extended period. For example, Microsoft Entra may allow a user session to remain valid for up to 90 days, depending on tenant policy. During this period, FedCM may continue making credentialed accounts and identity assertion/token requests without requiring the user to interact with an IdP-hosted sign-in page.

**\#\#\#\# Bad Rollout**

A high-severity defect in the service worker could affect credentialed FedCM requests for a large number of users. FedCM should support bypassing or disabling the service worker, or fetching an updated service worker script, without relying on the user revisiting an IdP page.

**\#\#\#\# Staged Rollout**

IdPs generally follow safe deployment mechanisms where changes are rolled out gradually, for example, to 1%, 5%, 20%, and eventually 100% of clients. The design must allow the IdP to continue using its existing deployment and rollback strategy for the service worker script.

**\#\#\#\# Eviction**

The user may remove the service worker registration, for example through storage eviction or site-data clearing. FedCM should support re-registering the declared service worker when it is needed again, and should support unregistering the service worker when the IdP removes the declaration from the well-known file.

**\#\# Registration**

The IdP declares a FedCM-specific service worker in \`/.well-known/web-identity\`.

\`\`\`json  
{  
  "provider\_urls": \[  
    "https://idp.example/fedcm/config.json"  
  \],  
  "identity\_handler": {  
    "service\_worker": "/fedcm/sw.js",  
    "scope": "/fedcm/",  
    "enabled": true  
  }  
}  
\`\`\`

The presence of \`identity\_handler\` indicates that the IdP has a service worker that should be registered and used for credentialed FedCM requests.

When FedCM is invoked, the user agent treats the \`identity\_handler\` declaration in the well-known file as the desired state. If a matching service worker is already registered for the IdP origin, declared scope, and declared script URL, FedCM does not register it again, but still runs the Soft Update behavior described below. If no matching registration exists, FedCM registers the declared service worker in the IdP's origin and declared scope.

FedCM managed registration fits the use case because FedCM is the component making credentialed requests to the IdP. It can ensure that the required service worker is registered immediately before it is needed, without depending on JavaScript running on an IdP page that may not be visited for several weeks or months.

**\#\# Service Worker Update Model**

This approach supports bad-rollout recovery and aspects of staged rollout by separating registration from freshness checks. FedCM should not re-register the service worker every time the FedCM API is invoked. Instead, when a registration already exists, FedCM should initiate a Service Worker Soft Update in parallel during every FedCM API invocation.

The high-level update flow is:

\`\`\`text  
On each FedCM API invocation:  
  If no matching service worker registration exists:  
    Register the service worker declared in identity\_handler.  
  Otherwise:  
    Use the currently active service worker for the FedCM request that caused this invocation.  
    Initiate a Soft Update for the registered service worker in parallel.  
\`\`\`

The service worker should be registered with cache behavior equivalent to:

\`\`\`json  
{  
  "updateViaCache": "all"  
}  
\`\`\`

This allows the HTTP cache to be used when checking both the top-level service worker script and imported script resources, such as scripts loaded by \`importScripts()\` in a service worker.

The IdP can serve \`/fedcm/sw.js\` with a cache lifetime and an HTTP validator:

\`\`\`http  
Cache-Control: max-age=1800  
ETag: "sw-build-42"  
Content-Type: text/javascript  
\`\`\`

In this example, the cached service worker response remains fresh for 30 minutes. FedCM requests a Soft Update whenever the FedCM API is invoked, but update checks within the 30-minute window can be satisfied from the user agent's local HTTP cache without making a network request to the IdP.

On the first FedCM invocation after the cached response becomes stale, the user agent revalidates the service worker script using the ETag.

\`\`\`http  
GET /fedcm/sw.js  
If-None-Match: "sw-build-42"  
\`\`\`

If the script has not changed, the IdP returns \`304 Not Modified\`, and the user agent continues using the installed service worker. If the script has changed, the IdP returns the new script with a new ETag, and the user agent updates the service worker registration through the normal service worker lifecycle.

The Soft Update should run in parallel with the FedCM request that caused the API invocation. The currently active service worker may handle that request while the user agent checks for an updated version. A newly discovered service worker becomes available after the normal installation and activation process completes.

This model allows the IdP to control how quickly fixes are discovered by choosing an appropriate cache lifetime. A shorter cache lifetime allows faster discovery of updates, while a longer lifetime reduces network revalidation traffic.

**\#\# Failure Handling and Emergency Disablement**

A service worker must not become a single point of failure for authentication.

If registration fails, the service worker cannot start, the service worker does not respond to the identity event before the timeout, or the service worker returns an invalid response, FedCM should use the normal direct-network path.

If the IdP needs to disable the identity handler completely, it can set \`enabled\` to \`false\` in the well-known file.

\`\`\`json  
{  
  "provider\_urls": \[  
    "https://idp.example/fedcm/config.json"  
  \],  
  "identity\_handler": {  
    "service\_worker": "/fedcm/sw.js",  
    "scope": "/fedcm/",  
    "enabled": false  
  }  
}  
\`\`\`

After the user agent observes \`enabled: false\`, FedCM should stop dispatching identity events to the service worker and use the direct-network path. Any existing registration may be ignored or removed asynchronously. If the \`identity\_handler\` declaration is absent, FedCM should also treat that as no service worker opt-in.

**\#\# Recommended IdP Service Worker Structure**

The registered \`/fedcm/sw.js\` file should be a small and stable bootstrap script.

\`\`\`javascript  
// /fedcm/sw.js  
importScripts("/fedcm/identity-handler.a13f92.js");  
\`\`\`

The imported content-hashed script contains the actual identity-handler implementation.

\`\`\`javascript  
// /fedcm/identity-handler.a13f92.js  
self.addEventListener("identityrequest", event \=\> {  
  event.respondWith(handleIdentityRequest(event.request));  
});  
\`\`\`

The bootstrap should contain as little logic as possible. It should primarily load the implementation script and perform only minimal lifecycle work.

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Christian Biesinger (Google Chrome)  
* Sam Goto (Google Chrome)  
* Nicolás Peña Moreno (Google Chrome)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Will Bartlett (Microsoft Entra)  
* Yi Gu (Google Chrome)

