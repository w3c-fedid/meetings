# FedID WG/CG Telecon, 2026-08-11

* Moderators:  Heather Flanagan

* Scribe: Phil and Sam

* Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

* Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * [FedID CG/WG process](https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md)  
* Ecosystem Update (10 minutes)  
* Discussion (40 minutes)  
  * [IdP Registration](https://github.com/w3c-fedid/idp-registration)  
  * [Identity Handler](https://github.com/w3c-fedid/identity-handler)  
* AOB

# Notes

## Administrivia

* Welcome.   
  * Also a FedID WG for DC API  
  * Topics overlap; some of the folk overlap  
* If here, member of either WG or CG. 

## Ecosystem Updates (10 minutes)

* Heather:  
  * Any eco-system updates?  
  * …  
* Sam:  
  * Facebook presented last week.  
  * Email verification related, progress there. Uses parts of the work defined here.  
* Emelia:  
  * Item on TPAC agenda for Identities across platforms.   
  * Overlaps with DIDs, ActivityPub, Solid Project, etc.  
  * [https://github.com/w3c/tpac2026-meetings/issues/62\#issuecomment-4723363296](https://github.com/w3c/tpac2026-meetings/issues/62#issuecomment-4723363296) 

## Discussion (40 minutes)

### [IdP Registration](https://github.com/w3c-fedid/idp-registration)

* Sam:  
  * Can frame the work with Emelia.  
  * Emelia to use the browser to help decentralized identity  
    * ATproto  
    * ActivityPub  
  * Made progress at the UX level recently.  
    * Weekly meetups  
  * Find ways to get IdP Registration to get to stage 2\.  
    * Need a good idea of what the UX looks like  
    * Intersection with R\&E federations.  
* Emelia:  
  * Weekly sessions to hammer out the design of IdP-Registration  
  * (Demonstrates IdP-Registration, screenshare)  
    * Shows how to register and IdP via the API  
      * Call is silent, no user feedback: [https://github.com/w3c-fedid/idp-registration/issues/21](https://github.com/w3c-fedid/idp-registration/issues/21)   
      * Identified as a problem  
        * Early versions had a prompt, which was removed, so looking to add that back in  
      * User prompt is being demonstrated  
      * We have a toast option, which is easiest to add back ASAP, and there are two options for the toast: opt-out or opt-in, we have a preference towards opt-out for now, since that will get more people setup with FedCM faster.  
        * On the  'opt-out' toast we would have a button to directly opt-out rather than hiding that.  
        * The opt-in 'allow' toast could disappear before the user has a chance to agree to it, which we think wouldn't lead to sufficient registration.  
        * Can be implemented soon, as common browser components.  
      * Some problems with these flows: a lot of the dialogs looked like permission prompts, and not the FedCM flow.  
        * (Tim in chat) ‘the inconsistency across Chrome identity prompts is really unfortunate.’  
        * Now looks more native, as a browser prompt  
      * The account can be immediately shown in the browser when the IdP registers. (P.S. The account is already known via the Login-Status APIs)  
      * We have another set of options which require more implementation work but potentially provide a better user experience:  
        * URL bar button, anchored like a permission prompt, this automatically shows a further pop-out for adding the account  
          * Similar UX to auto-fill, e.g., microphone access or geolocation access  
        * URL bar pill, still anchored, but with a "save account" prompt which feels more natively "FedCM", shows initially as a pill that then automatically opens a further pop-out allowing choice of adding the "account" to your browser (this really adds the IdP at the moment, not the account)  
        * (Sam) which we pick is TBD  
        * These are all passive mode UX, non-blocking. They can be dismissed and re-opened as long as you're still on a page on the IdP.  
      * We have also discussed an Active mode UX, which blocks the page interactions with a prompt.   
        * Needs a new API param to add ‘active’ or ‘passive’ mode to the IdP Registration API  
        * (Sam) Active needs a user gesture to work; cannot be called silently.  
        * This Active Mode UX is really intended for non-login use cases, e.g., an account management/settings screen.  
          * We did discuss if origins can determine if they are currently registered or not, this probably needs an additional API, but would allow giving different UX on page if the identity provider is already registered or not.  
      * (Sam) Toasts (UX element) is intended to be an ephemeral, lightweight specification (for the passive mode); the active mode is blocking, less lightweight  
      * (Sam) These are all early UX mocks, so lots can change and be polished.  
        * A lot of the language, URLs, text, etc is very rough, we'll have another meeting to polish these before we publish these designs publicly.  
    * Now, how onto how this is actually used  
      * Looks at ‘type’ in the credential.get API, matches registered IdP's/accounts by \`type\` of IdP.   
      * Currently, only passive mode is supported; active mode is not yet supported. We want active mode for parity with centralized IdPs.  
      * An RP can use the registered IdPs, but also provide fallback IdPs (commonly used IdPs, using the normal FedCM call)  
      * Can then choose one of those other IdPs, even if you are not logged in yet.  
        * As we know the loginUrl for the IdP we can show you that UX that we currently have for centralized IdPs.  
      * There is a find your account search box, which takes an input (username, handle, email) and attempts to lookup a suitable IdP.  
        * How this works is extremely TBD, probably requiring new APIs or endpoints.  
      * (Wendy) Questions in the chat.   
        * (Isaiah) ‘Users with mobility issues would have problems interacting with a toast. If we did go with that, it should be opt-in, since the user might not physically be able to decline consent in time for an opt-out toast.I like the other options (autofill/fedcm windows) better.’  
        * (Isaiah) A more persistent window would be better for this UI  
          * Emelia: Agreed from my perspective, right now the toast would be temporary just to get back *some* consent here.  
        * (Evan) The UI presented of the enumerated list of IdPs, tends to push toward a certain number of servers, but too many in the list push toward unusability.  
          * This is a concern, and we're trying to provide balance here, it is a centralizing factor, but each RP can specify their own list, so we don't have a centralized ranked list per \`type\` — an RP will usually know which IdP's are commonly used with their app.  
      * We did discuss having an ‘add another account’ button, which returns to the RP to let them figure out the login with the IdP. This would make the call effectively return \`null\` instead of a credential.  
        * The problem with this is that the UX would then be heavily dependent on RPs and would vary significantly from RP to RP.  
        * This led to us changing the "add another account" to show a "Find your account" which would provide a consistent UX across relying parties, but also poses the question of "how do you 'find your account'" — we're using "account" here when this is really "find your IdP" because people generally know what an "account" is compared to an "identity provider" (so it's just a language thing)  
      * (Sam) this is a fancier NASCAR flag, it only shows accounts in which you are logged into.  
        * (matched by \`type\` of IdP for the account matching the requested \`type\`)  
      * (Sam) NASCAR flag can become an empty search box, if you find one, it becomes an option in the list of accounts you can sign in with.  
      * Issue opened about, instead of having a String of ‘Type’, ‘Type’ could be a URI: [https://github.com/w3c-fedid/idp-registration/issues/29](https://github.com/w3c-fedid/idp-registration/issues/29)   
        * By switching to a URI for \`type\` we can also provide ecosystem branding for the type of account, which provides some brand recognition for the various ecosystems, which we previously lacked.  
        * This also solves the need for a "registry" of string literals that would need to be created otherwise with IANA or similar, since we can just defer to DNS.  
        * This could return the resolver for the ‘find your handle’ input, which would solve the interoperability problem across ecosystems with the different ways that account resolution works.  
      * (Heather) loads of work, shall we bring this back to continue the conversation. Do you want a dedicated side-meeting?   
        * Emelia, yes dedicated side-meeting when the design is ready, I'll be posting the designs after another polishing meeting to the Decentralizing FedCM blog: [https://decentralizing-fedcm.leaflet.pub/](https://decentralizing-fedcm.leaflet.pub/)   
      * (Tim) This looks amazing. Caution from passkeys, more than one option/prompt puts the user off. So just check the user is not overwhelmed.  
* Phil  
  * Register by the enterprise / organization rather than the user  
  * [issue\#715 Enterprise Scenarios: admin consent for users](https://github.com/w3c-fedid/FedCM/issues/715)   
  * Academic staff are issued enterprise managed devices  
  * Sam: enterprise policies could set that up  
  * Tim: yeah, this could help BYOD, when users log in to the browser profile and get enterprise policies loaded  
* Phil  
  * Second issue is being able to register for another origin  
  * [https://github.com/w3c-fedid/idp-registration/issues/3](https://github.com/w3c-fedid/idp-registration/issues/3)   
* Emelia:  
  * Workshop ideas with ActivityPub folk on UX, as mentioned at the last WG/CG meeting's notes, I am still looking for a point of contact to liaise with.   
    * For client apps, you want a credential, since the client would directly be interacting with the APIs for the account.  
    * For fediverse servers that only implement S2S parts of ActivityPub, you probably want to use the Fields API to request back just the identity information and then continue with Activity Intents FEP (already implemented by Mastodon, et al). This prevents issuing credentials to 30,000+ unknown origins, and takes you back to your trusted "home server".  
    * For C2S, this is TBD as to what you want, depends on how many "apps" exist in the ecosystem — you probably don't want to recreate the 30,000+ unknown origins problem.  
    * For the flows that **do** return a credential, you will need to protect that credential through means of DPoP and fine grained access such that you do not have as large an attack surface. Currently Mastodon's access tokens:  
      * Never expire  
      * Have no refresh  
      * Are not bound to the client instance, so could be stolen/exfiltrated  
      * This is why the Fields API is probably the recommended flow for the Fediverse in that sense.  
  * I have a meeting with Jesse from the Solid ecosystem tomorrow to try to work out some of the issues for Solid accounts. (Theo, my usual point of contact, is currently unavailable for a few weeks).

### [Identity Handler](https://github.com/w3c-fedid/identity-handler)

* Brandon, Microsoft  
  * Service Workers  
  * Thanks for the feedback in the github issue, spec PR  
  * Another PR for just-in-time registration  
  * Good feedback from Nicolas and the service worker team  
  * [issue\#715 Enterprise Scenarios: admin consent for users](https://github.com/w3c-fedid/FedCM/issues/715)  
  * It now has a repo of its own  
  * [https://github.com/w3c-fedid/identity-handler](https://github.com/w3c-fedid/identity-handler)  
  * We expect all issues to be resolved  
  * We are not going to proceed with 815, we are opening a new 842 that will subsume it  
  * We are also working on the service worker spec  
  * Brandon is leading this at Microsoft  
* Ted:   
  * When new repos are created we don’t know about them until the next call, so I’ll get to them later  
  * My workflow is based on github notifications  
  * Would be great if we could notify somewhere when they are created  
  * Heather: ack  
* Heather: any particular area that you need guidance?  
  * Brandon: we are working on implementation

## Any Other Business (AOB)

* 

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* Wendy Seltzer (co-chair)  
* Brandon Maslen (Microsoft Edge)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Yi Gu (Google Chrome)  
* Sam Goto (Google Chrome)  
* Evan Prodromou ([Social Web Foundatio](https://socialwebfoundation.org/)n)  
* Phil Smart (Shibboleth/Jisc)  
* Nicolás Peña Moreno (Google Chrome)  
* Bjorn Hjelm (Yubico)  
* Emelia Smith (Bluesky grant / independent)

