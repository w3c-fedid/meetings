# FedID WG Hybrid meeting notes, 11 April 2025

Date/Time: Friday, 11 April 2025, 09:00-16:00  
Location: Google Building, Sunnyvale, California


Reminder: WebAuthn will also be having a meeting 4/11 in the a.m.

Morning draft agenda (9-12 Pacific): **FedCM**

* Announcement:   
  * Scribe volunteer(s)? Johann until 10am; Emily next  
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* FedCM Core  
  * [https://github.com/w3c-fedid/FedCM/pull/712](https://github.com/w3c-fedid/FedCM/pull/712)  
* [Status of FPWD Issues](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues) ([github tag](https://github.com/w3c-fedid/FedCM/issues?q=state%3Aopen%20label%3A%22FPWD%22))  
  * Focus on issues that have NOT had attention to date  
  * Triage: resolution, continued discussion, or no-action response (assign writing of responses)  
  * Next steps  
* Other topics:  
  * Delegation?  
  * Process PR? — probably covered already  
  * IIW Debrief

**Lunch, joint with WebAuthn WG (12-1 Pacific)**

Afternoon draft agenda (1-4 Pacific): **DC API**

* Announcement:   
  * Scribe volunteer(s)? Matt, Wendy  
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * [Working Group Process](https://github.com/w3c-fedid/Administration/pulls)  
* WICG approved migration to WG ([issue 206](https://github.com/WICG/digital-credentials/issues/206)) — 5 minutes  
  * Migrate [repo](https://github.com/WICG/digital-credentials/), prepare for FPWD (see [FPWD blocker](https://github.com/WICG/digital-credentials/issues?q=is%3Aissue%20state%3Aopen%20label%3A%22FPWD%20Blockers%22))  
* FPWD publication goal date: 1 June 2025 — 5 minutes  
  * Consensus on blocking items no later than 1 May 2025  
* Registry Inclusion Rules \- [https://github.com/WICG/digital-credentials/pull/157](https://github.com/WICG/digital-credentials/pull/157) — 30 minutes  
* Issuance — [https://github.com/WICG/digital-credentials/pull/204](https://github.com/WICG/digital-credentials/pull/204) and Issuance: multiple requests — [https://github.com/WICG/digital-credentials/issues/207](https://github.com/WICG/digital-credentials/issues/207) — 30 minutes  
* **BREAK — 15 minutes**  
* Test development — 10 minutes  
* Open discussion — \<1 hour  
  * Multi RP requests  
  * [Get Client Capabilities](https://github.com/WICG/digital-credentials/issues/200)  
* Wrap up — 10 minutes

## **MINUTES**

### DC Coordination

Heather:

* [Consensus call](https://lists.w3.org/Archives/Public/public-fedid-wg/2025Apr/0000.html) to bring in DC [closed](https://lists.w3.org/Archives/Public/public-fedid-wg/2025Apr/0005.html) with no objections \- now a work item  
* Have a doc to describe meeting structure  
* Tue FedCM, DC Mon/Wed split, design team for that particular item, coming together quarterly to coordinate, next Madrid, then TPAC  
* Expect updates to the W3C calendar as well — see [Proposed 2025 Meeting Schedule](https://docs.google.com/document/d/1yR7emdjwk4BJsQWTrt06m5BTrawjlo6U-Q_ShTEpEy8/edit?usp=sharing)

### IIW Debrief

* Notes from the IIW Session, “[Can FedCM Work for Enterprise?](https://docs.google.com/document/d/1kI6tx5VUWa02_aNoFfjpabqwFP5kBiyw10577Xms6LQ/edit?tab=t.0)”  
* Sam Goto:  
  * Discussion with Microsoft, maybe a path to a proposal, some AIs  
  * Talked about Front-Channel Logout  
  * The “Cold-Start problem” and IdP registration  
  * Enterprise policies / trust signals  
  * Accounts for FedCM from the OS  
* Emily Lauber:  
  * FedCM is Social Login / Consumer Login, we want converged infra with Enterprise  
  * Had discussions around these enterprise scenarios at IIW such as when the IT admin consents for the user so there aren’t user prompts / disclaimer texts for the end user  
  * Future discussion on the mechanism for FedCM to accept that IT admin consent  
* Johann:  
  * Had good discussions on Front-Channel Logout — will try to formulate a proposal for this group to review  
* Sameera:  
  * Not clear if it should be a FedCM specific thing or not  
* Johann:  
  * To be clear \- this might not be only for FedCM, but definitely compatible with FedCM  
* Sam:  
  * Demoed delegation at IIW \- had good discussion around how it intersects with other things, IdP registration, autofill, etc.  
* Dick Hardt:  
  * I love autofill  
* Sam:  
  * Nice that it has progressive enhancement properties — degrades gracefully, e.g., in browsers that don’t support it, triggering matches the user intent nicely. Also matches with selective disclosure

### FedCM Core

[https://github.com/w3c-fedid/FedCM/pull/712](https://github.com/w3c-fedid/FedCM/pull/712)

* Nicolas Pena Moreno:  
  * Created a proposal for what are in core and what moves to extensions spec  
  * Landed a PR yesterday  
  * \[Presenting the spec on screen sharing\]  
  * Extension issues: things that will move into the extension spec, e.g., client metadata  
  * Most things are still in core spec, but marked with extension issues  
  * Permission request with disclosure will also not be part of core  
  * Fetching identity credential — passing fields, additional parameters moved to extensions  
  * Request permission to sign up moved to extension  
  * Fetch client metadata moved to extension  
  * Approved clients still used in core  
  * Again, client metadata moved to extensions  
  * Disclosure text also shown to extension — open question: what do we pass in browsers where it’s not supported? Do we just omit it? What does the IdP expect?  
  * TOS/Privacy Policy moved to extensions as part of client metadata  
  * Next step is to create an actual document and move extension issues to it, keeping notes in core that extensions may modify it in certain parts, want to call out for readers of core spec that implementers of extensions may behave differently  
* Johann:  
  * So one extension spec? \[Nicolas: yes\]  
  * If there is an extension we all agree on, it’s a bit easier to pull it back into main if it has its own spec, as opposed to factoring it out of a big “extensions” spec.   
  * Also separation of issues into their own repos could be helpful to organizing discussion.   
  * My suggestion would be to do separate repos per-extension, but I won’t push strongly  
* Heather:  
  * Separate specs make more sense to me as well  
  * Easier for browsers to say I support this one and not that one  
* Pavlik:  
  * Most important to me how conformance is defined  
  * If you have a spec with 6 extensions but the browser only conforms to 3 of them, WPTs, etc.  
  * Could be easier to have separate specs  
* Sam:  
  * Another benefit is it’s easier to have conceptual names, fields, passive mode, etc., get feedback on what it takes to move things out of extensions.  
  * Also easier with the stages process  
  * Also if, say, Mozilla wants to create additional proposals.  
* Ben VanderSloot:  
  * Would like to get feedback on passive mode: Maybe a subset that makes sense to Mozilla, e.g., when you’ve already logged in, once per session, etc., seems more reasonable. Having an AI model to bless it seems unreasonable.  
  * Don’t have strong opinions about extensions in one spec or not  
* Sam:  
  * Is passive mode in core spec?  
* Nicolas:  
  * It’s in the core spec  
* Sam:  
  * So maybe change it to say that it’s only allowed for returning users, extensions could disable that requirement  
* Ben:  
  * Already says “may” show, could tighten that definition. Maybe no point if there’s no commonality and no point of convergence anyway  
* Heather:  
  * Question about this note:  
    * core spec \= accounts pull, Active Mode, continuation API, login status API, IdP assertion endpoint, parameters API. This would be a non-fictional starting point.  
    * Remove passive mode, not fields as currently defined, metadata endpoint, IdP Registration (tho’ this last one has a requirement in the Solid demo)  
  * We said passive mode would not be in core, did that change?  
* Ben:  
  * It’s moving back  
* Nicolas:  
  * IdP registration: not in the core spec  
  * Question whether it should be  
* Ben:  
  * It’s not in any spec, core or extension. Got a lot of feedback that it’s really important for a lot of use cases, swayed me that we should lean on it more. I’m supportive of having it in core.  
* Transitioned note taker from Johann to Emily   
* Chat: multiple \+1 for IDP registration — elf Pavlik, theo \- thhck, Emily Lauber, Sameera Gajjarapu  
* Nicolas  
  * How do we shape the spec? Multiple specs or core & extensions in one  
  * Having a spec for a tiny feature that is removed to extensions, doesn’t make a lot of sense  
* Heather  
  * It would be easier for outsiders looking in to have them separate  
  * They will be in different stages in their life cycles  
* Nicolas  
  * Point of extension spec is things we don’t intend to move ahead into stages  
* Sam  
  * Goal is to have extension spec be empty in the future, so that extensions are none  
  * Way you make them empty is by having a very narrow discussion  
* heather  
  * Good goal but maybe not realistic   
* Sam  
  * Seems resolvable though  
  * Not clear to me whether or not we are going to need feature detection, so that websites can tell what’s available in the browser. Are there features pulled from core to extension that would require things for people to test?  
* Ben  
  * Makes sense to have feature detection for extensions or x-set of extensions   
* Nicolas  
  * Feature detection can be via a generic method that receives some parameter of what is supported. Extensions should be per thing. Probably nicer for IDPs instead of them having to figure it out per extensions   
* Heather  
  * Do we have an issue on this?  
    * [https://github.com/w3c-fedid/FedCM/issues/713](https://github.com/w3c-fedid/FedCM/issues/713)   
* Dick  
  * Not just feature detection for IDPs but for RPs  
* Heather  
  * Read through the editors draft and on the next call will include next steps based on that  
* Sam  
  * To Ben, do you feel represented by what’s in the core spec?   
* Ben  
  * I think so, but need to go back and read through it again.   
* Sam  
  * Where are you from prototype to spec compliance?   
* Ben	  
  * Prototype is a big gap. Different runway and 2 year timeline difference from Firefox than Chrome on implementation   
  * Could demo right now   
  * Key difference in Firefox user experience than Chrome  
    * The first time you use an IDP on an RP, will give some sort of permission to make the request   
    * First time ever in this browser instance / user profile. Same place that you store the connected account sets  
    * If you are in the connected account set or have an account in the connected account set, wouldn’t show the IDP permission request, would just go to the account selection UI of FedCM  
  * Things are converging though using the existing   
* Sam  
  * Is there a production level IDP to test this?   
* Ben  
  * Doesn’t have an available production level IDP to try this with based on the user agent switching   
* Nicolas  
  * Knows other IDPs to test with   
* Pavlik  
  * Spec only has one editor, Nicolas   
  * Is Ben open to join as an editor?  
* Ben  
  * With extensions taken out and just being a core spec editor, open to it   
  * Still needs to read through after the edits   
* Break time and then focus on FWPD

### [Status of FPWD Issues](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues) ([github tag](https://github.com/w3c-fedid/FedCM/issues?q=state%3Aopen%20label%3A%22FPWD%22))

* Focus on issues that have NOT had attention to date  
  * Triage: resolution, continued discussion, or no-action response (assign writing of responses)  
* Heather  
  * How close are we to candidate recommendation? Can’t tell because it is not marked up  
* Wendy  
  * Reminder, these need to be addressed before Candidate Recommendation. Don’t have to be fully resolved but do need a path or comment   
* Heather : issue 320 [https://github.com/w3c-fedid/FedCM/issues/320](https://github.com/w3c-fedid/FedCM/issues/320)	  
* Christian  
  * Opinion is that we can close the issue, having resolved the core discussion. I’ll write a comment and close  
* Ben  
  * \+1 to close and open new issues for any networking complications   
* Issue 578: [Allow IdPs to return JSON objects rather than Strings back to RPs https://github.com/w3c-fedid/FedCM/issues/578](https://github.com/w3c-fedid/FedCM/issues/578)   
  * Looking for comment from Okta who opened this   
  * Skipping for now because don’t have engagement from Aaron   
  * Potential connection from Microsoft IdP feedback \- Emily to follow up   
* Issue 585: [Allow IdP registration and RPs to match on a "type" – IdP Registration](https://github.com/w3c-fedid/FedCM/issues/585)  
* Heather  
  * This is actually in Stage 1  
* Sam  
  * a resolved issue for Chrome is when it is merged into the spec   
* Heather  
  * But IDP registration isn’t merged into the spec? So this isn’t resolved  
  * Probably going to need a dedicated session on IdP registration   
* Nicolas  
  * The issue needs to stay open. There are probably other IdP registration-related issues and none of them can be closed because there is no spec for IdP registration   
* Issue 587: [Why must \`SameSite=none\`?](https://github.com/w3c-fedid/FedCM/issues/587)  
* Heather  
  * Question in the W3C general thread asking about \`SameSite=lax\` being automatically set [https://w3ccommunity.slack.com/archives/C010CACSKAL/p1744367438057449](https://w3ccommunity.slack.com/archives/C010CACSKAL/p1744367438057449)   
* Christian  
  * Discussion has gone in the direction of probably okay to do it and Chrome has partially implemented it behind a flag   
  * Not fully agreed upon though, needs more work to drive it but has prioritized other issues   
* Heather  
  * Will reach out to Phil who opened the question in Slack and see if he wants to update anything   
* Issue 599: [OAuth profile for FedCM](https://github.com/w3c-fedid/FedCM/issues/599)  
* Heather  
  * Open question for Aaron   
* Sam  
  * If this isn’t part of the browser changes itself, then is it in scope as a blocker for this working group?  
* Heather  
  * If it prevents FedCM from actually working for IDPs, then yes we should cooperate to the fullest extent to get this working   
* Ben  
  * If there is work to be done to enable an OAuth profile, we should track it in this issue   
* Sameera  
  * We (Microsoft Identity) would use FedCM with OAuth, so we would back this   
  * \+1 from Emily   
* Action item  
  * Heather to talk to Aaron   
* Issue 609: [Spec says we send \`SameSite=Strict\` cookies](https://github.com/w3c-fedid/FedCM/issues/609)  
* Christian  
  * Editorial change that a part of the spec says \`SameSite=Strict\` but that it is not true in implementation  
* Nicolas  
  * Action item for Christian to make the change   
* Issue 616: [Once params are merged into the spec, deprecate the nonce parameter](https://github.com/w3c-fedid/FedCM/issues/616)  
* Sam  
  * The idea is to use “nonce” inside of the newly merged params, instead of separately.   
  * Could deprecate nonce and move it into params and make a backwards compatibility change to resolve this issue, and then come back to it after dedication   
* Nicolas  
  * Disagree this is worth making a fuss for since there is not a lot of spec work that references nonce   
  * Vote is to keep it   
* Ben  
  * Think delegation could use params instead of nonce   
  * A backwards incompatible change, is it worth cleaning up a now useless field?   
* Sam   
  * if/when get to delegation, would we rather have nonce as a top level or inside of params?   
* Heather   
  * If we remove it, it’s a backwards incompatible change. Who is impacted?   
* Sam  
  * All IdPs use this today, but it is only a few IdPs   
* Heather  
  * Not clear as to why we should bother. What’s the problem with leaving it?  
* Sam  
  * Aesthetically it is unpleasing, ugly   
  * It would be pretty if we got to delegation   
* Heather  
  * No urgency to do anything now, address it if delegation gets sorted out   
* Sam  
  * Leave it open as an option to make the backwards incompatible change   
* Dick  
  * As an implementer, if you’re going to make the change do it now.   
  * Not for ugly, but could make the change because it is confusing to developers   
* Sam  
  * Architecturally incorrect because all OAuth stuff should go into params, but why is the nonce thing outside of it?   
* Dick  
  * Clarified this is important for OpenID Connect, not OAuth  
* Sam  
  * Params are not something the browser would read, so nonce would fit in params  
  * Nonce as it’s being used today is architecturally incorrect, so could make the backwards change all at once  
* Ben  
  * Do changes earlier rather than later and developer confusion is a good point   
  * It feels wrong to have a legacy param hanging around that duplicates functionality and especially to accept legacy behavior at the first working draft   
* Sam  
  * Bucket all the backwards incompatibly changes at once to make it easier for IDPs to make the change  
  * Expects us to have more as we get closer to candidate recommendation   
* Dick  
  * It’s hard to predict how many changes. It is better to do it earlier   
  * If there are other changes in the spec, signal you want to change   
* Pavlik  
  * Breaking changes are to be expected up until Candidate Recommendation and early adopters should realize it is possible to make it happen  
  * Implementers may support both ways for some time; it doesn’t have to be a hard transition   
* Nicolas  
  * We’re already frequently asking them to make breaking changes   
* Sam  
  * It is expensive for the IDPs that Chrome has worked with in early adopters in production to make this change   
* Heather  
  * Can we mark it in some way as coming for changes  
* Sam  
  * Doesn’t help because the IDPs would have to make the change before the browser makes the change  
  * Reasonable outcome to mark this as deprecated   
* Ben  
  * It is a great scenario for deprecation if you know the set people that need engaged to make the change   
* Sam  
  * Two action items: immediately mark nonce in spec as deprecated; asynchronously work with existing IDPs that are deploying FedCM to move out of using nonce and use params instead   
* Issue 618: [Support chained authentication flows before reducing heuristics and classifications/lists in navigational tracking mitigations](https://github.com/w3c-fedid/FedCM/issues/618)  
* Nicolas  
  * Not sure why this is a CR blocker  
  * Is a hard problem to solve   
* Heather  
  * Because they can’t use FedCM at all without this addressed   
* Ben  
  * This is something we should try to resolve. Lightweight was heading in this direction   
  * Login URL work could relate to this, something to investigate   
  * Don’t think impossible but it is hard work and might require UI changes   
* Wendy  
  * How can we help that work to progress?   
* Ben  
  * Can comment on the issue to try and move it forward and engage there   
  * Agenda \+ to discuss it on next call   
* Emily  
  * \+1 as an IdP, this would be important to us (Microsoft)  
* Issue 620: [Make it easier to deploy this at the eTLD+1 for registered IdPs](https://github.com/w3c-fedid/FedCM/issues/620)  
  * Part of IdP registration   
    * [https://github.com/w3c-fedid/idp-registration/issues/4](https://github.com/w3c-fedid/idp-registration/issues/4)   
* Nicolas  
  * Now every fetch is problematic. Do-able, though, and have a path forward for this one   
  * Need to keep in mind the potential privacy issues   
  * Did make some progress on [IdP Registration issue 4](https://github.com/w3c-fedid/idp-registration/issues/4) but need to make spec changes   
  * Did not make progress on the other alternative. But if one alternative, just solving \#4 is okay, and then closing the alternative   
* Heather  
  * Future meeting on IdP registration to discuss   
* Issue 625: [Returning accounts go first in getUserInfo](https://github.com/w3c-fedid/FedCM/issues/625)  
* Ben  
  * The function to get accounts returns an array of stuff, but should probably return just the stuff the user selected  
* Nicolas  
  * Has a PR for this. Current experience is it returns all accounts and the IDP doesn’t know which ones are returning   
  * Could sort, just return the returning, or do both. Wants some way to do this   
  * Did already ship this in Chrome. The order in which returning is not important because it is just provided by the IDP   
* Issue 626: [PP/TOS requirements are different from auto reauthentication](https://github.com/w3c-fedid/FedCM/issues/626)  
  * Already closed by PR   
* Issue 627: [Add webdriver command to open PP/TOS](https://github.com/w3c-fedid/FedCM/issues/627)  
* Sam  
  * Anything that is extensions should not be a candidate recommendation blocker?  
* Heather  
  * It does mean we have to say what we’re going to do with it  
* Sam / Nicolas  
  * Fine to just remove the tag of FWPD and will move it to the extensions repository once we have that   
* All the 0 ones \!  
* [Issue 677](https://github.com/w3c-fedid/FedCM/issues/677#issuecomment-2594192449)  
  * Seems already closed  
* Sam  
  * Closed the issue because moved it to a [ReadMe file in the delegation repo](https://github.com/w3c-fedid/delegation), but the issue itself seems open   
* Nicolas  
  * Needs to be re-opened for tracking the resolution  
* Sam  
  * Is this a CR blocker? Unclear  
  * This has a connection to the auto-fill work   
* Dick  
  * Wants auto fill   
* Sam   
  * So far, I think it is tightly connected to auto fill. Do we want to block a candidate recommendation on it or not?  
  * What is the bar for candidate recommendation?   
* Heather  
  * Want it to be usable? Let’s ask people that care directly  
* Dick  
  * Feels extremely strongly about verified email addresses   
  * This seems by a multiplier more significant than anything else   
  * Easy for an RP to add support for this   
  * Empowers the indieweb people who want control over their email address as a way to set up and run their own IdP in a lightweight way   
  * Enables dream from many who started OpenID   
* Sam  
  * Personally shares the excitement, can’t speak for Chrome as a whole   
  * But it is less mature than other things. Need this group to define our goal for CR   
  * Has some of the personas hint, so how do other browsers feel about it?   
* Ben  
  * Having zero knowledge proofs integrated is probably further out than we’d like for CR, but having blindness to IdPs is probably very important   
  * Don’t know if want to call it a blocker, maybe closer to a stretch goal   
* Heather  
  * Process question: how much change can you have to the spec after CR?   
* Wendy   
  * Don’t think there are guidelines for level of change between Candidate Recommendations and Proposed Rec. Can have multiple CR drafts. There is a tag that you can use for more Candidate Recommendation drafts if you have to return to add a new feature or significant change  
* Heather  
  * Could we go to CR with what we have to do and then add this type of functionality and go to a second CR with those changes?   
* Wendy  
  * It's more in the process than the patent policy   
  * We don’t have to agree now on everything we would like to add before CR; we can add big chunks of features later if the group agrees that is the right way to build the spec   
* Pavlik  
  * Process to follow for changes: [https://www.w3.org/policies/process/\#revising-cr](https://www.w3.org/policies/process/#revising-cr)   
* Ben   
  * Move forward with this in the CR set. If we get to something stable and this is the only thing missing, then take this issue out and then do a change to the CR. But if we keep it in for now and continue to work on it, maybe it is ready when we go to CR   
* Sam  
  * Does IDP registration fit the same mold?   
  * Unclear if included in the OAuth profile issue   
* Ben  
  * Think IDP registration and IDP blindness fit into the same bucket   
* Heather  
  * Our charter has the timeline in there: wanted CR between April & June   
  * It has multiple dates in the charter: Q1 or Q2 in 2025   
  * Realistically, would want CR by TPAC   
* Sam  
  * Both IDp registration and delegation is likely not ready by then   
  * Chrome has not launched anything with evidence of demand. Haven’t seen enough interest in IDP registration and delegation   
* Ben  
  * Argues there is a lot of demand in the room   
* Sam  
  * Difference between abstract demand and actual implementations of code running in production   
  * Don’t see code for RPs or IDPs running    
* Pavlik  
  * If something doesn’t have enough adoption, mark it as at risk and remove it later in the process   
* Sam  
  * Internally as working group could take a leap of faith on adding it and then later seeing adoption grow   
  * IdP registration is plausible as get for CR if we took a leap of faith   
* Heather  
  * This is something that belongs in CR. Haven’t seen implementation of it because people maybe just learned about it  
  * Give it till end of summer if we don’t see implementation   
* Emily  
  * As an IdP who learned about this feature at IIW, give us some time to investigate it and decide how we might implement it   
* Ben  
  * Let’s drop it and use it as a leap of faith   
* Sam  
  * Do we think there is a leap of faith in lightweight mode?   
* Ben  
  * I think IdP registration depends on what you want to accomplish. Let’s focus and set priorities on leaps of faith  
  * IdP registration is probably the biggest   
* Revisiting items with Aaron returned to the room   
* Issue 578: [Allow IdPs to return JSON objects rather than Strings back to RPs](https://github.com/w3c-fedid/FedCM/issues/578)  
  * Be able to return JSON data from assertion endpoint instead of a string  
* Aaron   
  * We had a workaround to use JSON parse on the string, but agree it is useful to return the data  
* Sam  
  * Feel strongly enough to block on CR  
* Aaron  
  * If we don’t change it now, it will probably never change   
  * Is there a downside to changing it now?   
* Sam  
  * Potentially extra scope   
* Aaron   
  * Better pattern this way  
* Sam   
  * Browser engineers can look at it and level of effort involved   
* Emily  
  * Also something Microsoft as an IdP is interested in, but need to confirm   
* [https://github.com/w3c-fedid/FedCM/issues/599](https://github.com/w3c-fedid/FedCM/issues/599)  
* Aaron  
  * Don’t think this goes into the spec, but are the right things in place in the spec to even do this? Writing it pointed out a lot of gaps. Haven’t followed up on all the issues that came up from writing it but need to make sure those are resolved   
* Ben  
  * Did this use any of the IDP registration?   
* Aaron  
  * The OAuth protocol doesn’t, but the INDIE registration does  
  * This issue was meant to be OpenID connect   
  * IdP registration would be extra credit, but not required   
* [https://github.com/w3c-fedid/idp-registration/issues/10](https://github.com/w3c-fedid/idp-registration/issues/10)   
  * Revisit with Aaron  
* Aaron  
  * Trying to remember about the scenario of corporate marketing splash page vs the login domain being on a subdomain   
* Ben  
  * It might not work for you if you’re relying on the registration for the first time. Might end up having to do the DNS one as well   
* Sam  
  * Second alternative only solves for registered idps, first alternative solves for both scenarios   
* Ben  
  * So we probably need both and will investigate the DNS code   
* Sam  
  * Need to investigate if we need both. Will explore further and report back   
* Emily  
  * Sameera and I created some new issues based on IIW conversations. Not necessarily blockers, but we’d like to discuss them in a future meeting  
  * [https://github.com/w3c-fedid/idp-registration/issues/20\#issuecomment-2797666514](https://github.com/w3c-fedid/idp-registration/issues/20#issuecomment-2797666514)  
  * Both consumer and enterprise scenarios  
  * Enterprise scenarios we could use IT admins to manage the registration consent for the users  
  * Consumers can manually accept these  
  * We’d like to see a path where the IT admins could set registered IdPs for the users  
  * We’d also like some of the disclosure text to be controlled by IT admins  
* Aaron  
  * Is autofill related to this?  
  * We need the IdP registration feature so that it can be used for enterprise scenarios, because IdPs wouldn’t be able to enumerate all IdPs  
  * I don’t think that the autofill vs popup is a distinctive factor in that discussion  
* Emily  
  * SGTM  
* Aaron  
  * That's just the idea of pushing the IdP registration to the browser without the user clicking the button  
  * That might not need to be part of the spec; it can be an internal browser API or from the OS  
* Emily  
  * We need a trusted signal outside of the end user itself  
  * Definition of the mechanism TBD  
* Ben  
  * Do you just not want to show a dialog for a given IdP?  
  * Or do you want to push an IdP registration via an extension?  
* Emily  
  * Both?  
  * Depending on the time of scenario  
  * Enterprise scenarios can be managed browsers, managed devices, etc.  
* Ben  
  * That makes sense, could  be extended, added to the extensions spec  
* Emily  
  * Action item to add the github issue once created  
  * [https://github.com/w3c-fedid/FedCM/issues/715](https://github.com/w3c-fedid/FedCM/issues/715) 

Afternoon draft agenda (1-4 Pacific): **DC API**

* Announcements:   
  * Scribe volunteer(s)? Matt,   
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * [Working Group Process](https://github.com/w3c-fedid/Administration/pulls)  
* WICG approved migration to WG ([issue 206](https://github.com/WICG/digital-credentials/issues/206)) — 5 minutes; WG approved taking on the work-item   
  * Migrate [repo](https://github.com/WICG/digital-credentials/), prepare for FPWD (see [FPWD blocker](https://github.com/WICG/digital-credentials/issues?q=is%3Aissue%20state%3Aopen%20label%3A%22FPWD%20Blockers%22))

## MINUTES (Afternoon)

* WICG approved migration to WG ([issue 206](https://github.com/WICG/digital-credentials/issues/206)) — 5 minutes  
  * Migrate [repo](https://github.com/WICG/digital-credentials/), prepare for FPWD (see [FPWD blocker](https://github.com/WICG/digital-credentials/issues?q=is%3Aissue%20state%3Aopen%20label%3A%22FPWD%20Blockers%22))  
* FPWD publication goal date: 1 June 2025 — 5 minutes  
  * Consensus on blocking items no later than 1 May 2025  
  * FPWD is independent from OIDF processes  
  * OIDF needs something to refer to, and prefer a working draft  
  * EU needs something tangible to link to as well  
* Schedule breakdown: [Proposed 2025 Meeting Schedule](https://docs.google.com/document/d/1yR7emdjwk4BJsQWTrt06m5BTrawjlo6U-Q_ShTEpEy8/edit?tab=t.0)  
  * FedCM will still meet Tuesdays \+ Thursdays (?)  
  * DC API will continue to meet Mondays \+ Wednesdays  
  * Quarterly joint working sessions w/both FedCM \+ DC API peeps: hybrid meetings  
* Registry Inclusion Rules \- [https://github.com/WICG/digital-credentials/pull/157](https://github.com/WICG/digital-credentials/pull/157) — 30 minutes  
  * A list of protocols and related formats that meet expectations for use with DC API  
  * Want to make sure protocols are secure by design, meet certain security requirements, can handle the complexities of JavaScript  
  * Helps protocol architects understand requirements of browser runtimes to adapt the protocol for interoperability across browsers  
  * Also gives other groups within the W3C a chance for wide review  
  * A blocker for FPWD  
  * Q: Is the intent that conforming implementations may support things not in the registry?  
    * Yes, everything in the registry is optional, but it’s optional to support other protocols  
  * Nick Doty: Want not just privacy review, but that we affirm that certain expectations are met  
  * Simone: To require security/privacy review needs approval of W3C Security and Privacy WG review groups, since it’s asking them to take on significant work. I’ll talk with them next week about security. As groups we need to evaluate the effort of third party reviews, else use a SHOULD. I liked the idea that we can require protocols to have Security and Privacy considerations sections.  
  * Rick: How are we thinking about versioning? If there’s a new version of OID4VP do we consider that a new version?  
    * Rick: If the top level data structure changes that would require a new protocol identifier  
    * Lee: If there are no breaking changes then we want things to be flexible enough to not require a new identifier  
    * Sam: Understanding is that some browsers will raise TypeErrors if new fields are added, until the browser updates to support the new value  
    * The spec can support multiple implementation approaches  
    * Could this cause developer confusion?  
    * We’re so used to thinking about the browser, but we need to think about the browser *and* the wallet together  
    * Goal between 1.0 and 1.1 is that the request wouldn’t get dropped  
    * Whether it’s the browser or wallet dropping new values, it shouldn’t matter  
      * So long as it’s only the new values being dropped and not the whole thing  
  * Heather: Big issues remain: requiring free accessibility, handling optionality of new values  
  * Tim: Does the current proposed text support the acceptability of dropping unrecognized values if the identifier doesn’t change?  
    * Including a version number in the protocol identifier seems obvious, but there’s an assumption that the “web is unversioned”  
    * Requirement  can be relaxed, “avoid using a version identifier if possible”  
    * Major version is important  
    * “mdoc” doesn’t convey version, year  
      * “mdoc” implies Annex C, the identifier could be an opaque identifier  
  * Matt: if the id is too vague, its unclear if 2 years ago if the protocol id.  
    * Http example there hasn’t been any breaking changes  
    * we need to tell protocol designers not to make  backwards incompatible changes  
  * Rick:  
    * Our decision in this room: id represent contract for data format may be extensible over time but not change   
  * Matt: time will tell if doc formats or protocols will need to change  
    * Registry should help influence decisions and save time for protocol designers  
    * Don’t want to see registry entries being pushed on W3C  
    * Multiple requests with new identifiers in them  
  * Naming rules  
    * Maybe we take out the requirements  
    * We can get more precise, remove the part about major version changes triggering a new identifier  
    * Let’s point to TAG policy at the end?  
  * Matt: So if there’s a new major version of a protocol, shouldn’t the identifier change to help verifiers specify multiple requests of each version?  
    * Point is don’t feel constrained to strictly use numbers in new registry identifiers  
  * BrianC: Let’s not make decisions that throw away conversations and progress made in other SDOs about communicating version changes  
    * Current changes will involve A) pointing to TAG rules on naming, or B) simply removing the line  
  * **“Freely available”**  
    * In ISO specs are typically not made freely available unless a government organization says they must be  
    * This makes ISO specs difficult to review  
    * Requiring free availability excludes ISO from being included to registry  
    * Procedurally, PRs to add to the registry cannot be approved until the spec is made available  
    * Unfair for us to stomp on organizations that rely on proceeds from selling spec access to survive  
    * What is the floor for how expensive is “too expensive” for a spec? 0.50?  
    * If an organization want to add a spec that is not freely available, we can make it a requirement that they provide access to the spec  
    * It’s about developer ergonomics and usability. It’s not unreasonable for an org that promotes the free and open web to require other standards to be freely available too.  
    * We would be starting a bit of a fight with those orgs. How can we more constructively liaison with, e.g., ISO?  
    * What if we remove the requirement about free availability? Instead require making a suggested registry entry available for review?  
    * We should care about the evolution of the protocols. Especially if we defer privacy and security questions to the protocols, this would be concerning if many of us are prohibited from participating in review. We should be allowed to participate in the development of related standards  
    * Excluding non-free specs from the registry wouldn’t impact the use of those specs. Adding “freely” doesn’t help efforts to get for-pay specs made freely available  
    * Proposal: let’s leave “freely available” in, because there are other conversations to be had about e.g. Annex C and by the time those conversations happen then free availability could be taken care of  
    * For FPWD, we can probably get away with keeping text as-is. Requiring free availability is not typical in W3C, though, so it will lead to further discussion. Note it in the “list of known issues” in FPWD that must get addressed before CR.  
    * So the text represents the ideal state, and when FPWD comes out we’ll find lots of other examples of problems the rules will cause. “Is this set of rules good enough right now to go into the spec?”  
    * What if this spec has normative references to other specs that are not freely available? Other W3C specs reference ISO specs  
    * Sometimes it’s unavoidable. If there’s no way to reconcile availability then the spec can still be referenced. If it’s normative and not simply informative then there has to be a discussion about including a reference to that for-pay spec  
    * \<PR suggestions to be able to merge sooner than later\>  
* Issuance — [https://github.com/WICG/digital-credentials/pull/204](https://github.com/WICG/digital-credentials/pull/204) and Issuance: multiple requests — [https://github.com/WICG/digital-credentials/issues/207](https://github.com/WICG/digital-credentials/issues/207) — 30 minutes  
  * Mohamed: Issue: whether we should support multiple requests in the same call. Each request contains a protocol and data block; response is some wallet is taking care of that. Use case: you go to a website to issue credentials, wallet handshake then do issuance. Don’t think we have many issues open. Agreed it’s something we need  
  * Tim: Open question, whether we restrict members by protocol identifier  
  * Matt: In general, issuance via DC API makes sense just to return up/down whether the wallet handled the request.  Re Marcos’s comment. In issuance scenario, is the assumption that the user is on the issuer’s website? Bc my understanding issuance can be triggered on any website that has knowledge of where the issuer is.   
  * Lee: You're triggering the upload to a wallet, the wallet takes over to get it.  
  * Matt: You don’t want the website getting the credential back, privacy. Deferred …   
  * Tim: At minimum, you need “yes, the wallet got the request or not” , or get back request ID.   
  * Mohamed: Terminology point: is it provisioning or issuance. Some preference for “provisioning”  
  * Heather: I thought “issuer” was term of art  
  * Tim: You can have an alias in the spec.  
  * Rick: Argument I heard re “issuance” is that there are 2 phases, issuance and provisioning; the thing we’re doing here is provisioning phase.   
  * Lee: We see “issuance” everywhere in OpenID4VP  
  * Marcos: We can add a note. We did lots of work on get part of the API. Worried about rushing this one. I assumed there would be UI on issuance; vs Lee said could send to the wallet for deferred issuance. Other issues re-create, store,.. I’m worried if we try to land too quickly w/o enough implementation experience, want to have a committed second implementation.   
  * Can we hold this one a little bit to experiment more, find a second implementer? Don’t think we need it for FPWD.  Get to shared work, e.g., presentation at IIW  
  * Rene: Is the expectation to create the connection between wallet and issuer at this point, and protocol defines how credential gets provisioned to the wallet, somewhat out of band? It’s mostly creating the route issuer-wallet  
  * Tim: to provide the route selector  
  * Rick: I won’t take a strong stance whether this needs to be in FPWD or not, but we have use cases we intend to support soon in chrome. We might then need to start another spec in WICG to meet commitments to partners who want to start using this thing.  
  * Lee; OpenID4VCI has dependency on this spec. We’re trying to get rid of custom schemes here too. I think we want this in the June 1 draft, else we only have custom schemes in the draft for issuance.   
  * Joseph: We need to have some idea on the form and rules of the API, not just the reference. Lots of knock-on effects  
  * Marcos: You can look at the PR diff, even before it gets to a Draft  
  * Mohamed: By splitting things, we can make fixes without breaking presentation  
  * Sam: This is still WD, not Candidate Rec. Can you explain the hesitation?   
  * Marcos: Once it lands in the spec, the cost of changing goes up, it’s in the wild. Harder to change the API.  
  * Sam: Can we fix the way we’re working with the ecosystem, so we can get things into the spec  
  * \[break\]  
  * Heather: We’ve been having a process discussion, more than technical. Debate is whether to accept for FPWD without 2 browser implementers, as was done in previous WICG draft inputs.   
  * Rick: I don’t think we established a model. The concerns I heard from Marcos relate less to spec development than to shipping and origin trials. Which for chromium don’t depend on spec   
  * Tim: Going forward, what does 2 implementations mean: 2 browsers; 1 browser and 2 wallets?   
  * Marcos: All the spec text we have relates to things going into the browser. We’re not testing protocols, just interop of thing that comes in and goes out  
  * Tim: We also didn’t define discovery for external sources, which is how you talk to the wallet, even for a presentation.   
  * Heather: could we add a note here that implementations are still pending and this may change?   
  * Marcos: CredMan has lots of bugs, like going to look at internal cred store. We need to fix the underlying specs too. The assumptions other specs made didn’t hold up, so we need to fix those too  
  * Rick: I’m down with investing to fix those things (elsewhere than this group). Have you seen evidence they have caused interop problems?  
  * Marcos: We had to refactor WebAuthn out of CredMan  
  * Mohamed: Agnostic re issuance or presentation  
  * Heather: We think it’s technically sound, but if Webkit team implements and finds necessary changes, Google will be on the hook to change   
  * Rick: in origin trial, that’s ok  
  * Marcos: We can come to the WG with feedback.    
  * Rick: We’re bumping into the ARF timeline.  Can we make reasonable progress in the next 2 weeks, so until the end of April?  
  * Heather: Does anyone object to merging for FPWD for reasons we haven’t already discussed?   
  * Hearing nothing, we should go ahead and merge, looking for feedback to make sure we’ve gotten it right.   
* Test development — 10 minutes  
  * Marcos: We have a test suite. Relying on empty OpenID4VP dictionaries. It would be nice to have real things there.   
  * Lee: There's a conformance test suite.   
  * Joseph: there are official examples, open source, not normative  
  * Marcos: does anyone else want to be involved  
  * Rick: Big fan of comprehensive test suite. How do our tests take account of registry  
  * Sam: What are we going to write in spec/test if you make a request that’s out of registry?   
  * Rick: that’s a question for the registry criteria, re optionality  
  * Tim: We had consensus in the IIW session, if a request makes it to the wallet, always get a promise that resolves successfully.   
  * Sam: by that criteria, it would fail in Safari because it doesn’t reach the wallet. No WPT test can codify the right behavior unless we agree on behavior  
  * Wendy: Testing policy: do we need tests before a PR is merged, or at CR  
  * Tim: WebAuthn requires tests before CR  
  * Rick: what do we have for FedCM, do similar here  
  * Mohamed: we have some issuance tests waiting to be merged  
  * Sam: We need to agree on test conditions  
  * Mohamed: How much are we opinionated on the request itself? As chrome, as long as it’s well formatted, we’re ok. Webkit is more opinionated  
  * Lee: It's an object that can be serializable JSON.   
  * Sam: in WPT we shouldn’t test on parsing errors in the request  
  * Marcos: Give me something that could make it to the wallet. In WebKit, we do check everything, but that’s an implementation detail, we may fail earlier.   
  * Sam: What should we call that boundary? Selector?   
  * Hicham: We should make sure the spec allows security architecture that wants to check the content before it gets out of the browser  
  * Mohamed: testing, what is the expected response when you send a malformed request? What’s the value of the registry?  
  * Sam: We should not have a WPT that fails on the specific structure of a MDOC request, it’s gone somewhere.  For unanticipated protocols, we should have a test  
  * Marcos: We should have test of thing that should have gotten to the wallet  
  * Sam: What would happen if we wrote a test for OpenID4VP  
  * Marcos: We’re checking all the error paths  
  * Lee: Can the test of unsupported match Android response if there’s no wallet?   
  * Heather: What tests are needed?  
  * Marcos: OpenID, mDoc  
  * Heather: Joseph, can we get OpenID help on the testing?  
  * Joseph: Probably not today…  
  * Marcos: All contributors to tests are welcome. Mohamed and I are working together not to stomp on one another’s test implementations  
  *   
* Open discussion   
  * Heather: preference between remaining topics for discussion.   
  * Tim: Issue 205, intent to migrate. WG adopted. Applause all around.  
* [Get Client Capabilities](https://github.com/WICG/digital-credentials/issues/200)  
  * Tim: now that we know there will be a difference, we heard at IIW developers will need this. We should un-park it.   
  * I will do the PR  
  * Nick: look forward to seeing the PR, but still not clear what capability exactly is being revealed.  
  * Tim: PR I’ll put forward is hybrid support, protocol support. In WebAuthn, we returned a list of strings, don’t think we want that here  
  * Lee: We don’t want to return a list of strings  
  * Tim: Prefer we call it something different if opposite from WebAuthn.   
  * Matt: This is very specifically about the client, not about the wallet. Does the browser recognize or pass through OID4VC? yes/no  
  * Tim: There could be value in splitting. Difference between browser understands the extension, browser supports the extension   
  * Matt: This isn’t a method you’d use to see whether there’s a wallet supporting the protocol. Escape hatch for graceful improvement as capabilities are added. Developer story is better to help devs implement something now  
  * Mohamed: cross-device…   
  * Matt: In WebAuthn, merely, “could the client facilitate hybrid,” not, will it work. Could still fail because user doesn’t authorize  
  * Mohamed: cross-device is part of the platform,   
  * Sam: what we need to test is whether protocol is supported  
  * Tim: we don’t have to do hybrid now, but determining ergonomics  
  * Rick: think we should do “is Protocol Supported” not Get Client Capabilities   
  * Tim: Let me take a stab at a PR for is protocol supported, not blocking FPWD  
* Multi-RP requests.   
  * Lee: Not requests, multiple wallets. You can ask for more than one credential at the same time. E.g., ask for a driving license and a passport. Today, if they come from the same wallet, it can probably return them. If they come from different wallets, we can’t compose them into a single result, because of response encryption. So we probably need to return an array of DC objects.   
  * Sam: Is it multiple responses to the same OID4VP request?  
  * Lee: Yes.   
  * Sam: Why not modeled within the OID4VP response?   
  * Lee: We’re the ones who compose the response  
  * Mohamed: This should be at the protocol level, not API. Data object encoding array  
  * Lee: layering issue. It can be an array of data objects. The data object is what comes back from wallet  
  * Hicham: More complicated than having a list of encrypted objects — privacy, who put together the responses, whether it’s ok to return, etc.   
  * Lee: We do that today at the OS level but then can’t return it  
  * Sam: Share Hicham’s concerns about the layering . Need more discussion, how do we satisfy a response with multiple credentials  
  * Lee: I’m saying return multiple DC objects  
  * Sam: That worries me less  
  * Christian Bormann: This is going to be hard to solve  
  * Hicham: From wallet perspective, currently, wallet determines whether it can fulfil response; if need to reach consensus among multiple wallets, tricky problem  
  * Lee: That's an OS-level problem. It is challenging.   
  * Mohamed: Again, concerned about putting this at the API level  
  * Sam: Can do this at different layers  
  * Tim: Can Lee and Mohamed create issues for their proposals so we can compare?  
  * Lee: or in one issue  
  * Sam: Is there no fallback?   
  * Tim: Optimized for DC API.   
  * Heather: Homework: create an issue so we can compare the options.   
* Wrap up — 30 minutes  
  * Heather: We got 35 pages of notes (so far\!) Thanks to the scribes. Go us, lots of good work. Do you want to meet Wednesday, 16 April? \[no\]  
  * Next call, Monday 21 April. If critical mass. 

## **Sign-in:**

* Heather Flanagan  
* Wendy Seltzer  
* Nicolás Peña Moreno  
* Christian Biesinger (Google Chrome)  
* Aaron Parecki  
* Sameera Gajjarapu (Microsoft Identity) \[morning\]  
* Emily Lauber (Microsoft Identity)  
* Dick Hardt (Hellō)   
* Harrison Tang  
* Sam Goto  
* [Ted Thibodeau](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/)) \[remote, both sessions\]  
* [elf Pavlik](https://elf-pavlik.hackers4peace.net) (independent, Solid CG) \[remote, both sessions\]  
* [Thhck](https://github.com/thhck) \- Theo   
* Johann Hofmann (Google Chrome)  
* Chris Fredrickson (Google Chrome)  
* Benjamin VanderSloot (🦖Mozilla)  
* Marcos Caceres  
* Brian Campbell (Ping Identity) remotely \[afternoon\]  
* Simone Onofri (W3C) \[afternoon\]  
* Tim Cappalli (Okta) \[afternoon\]  
* Matthew Miller (Cisco) \[afternoon\]  
* Rick Byers (Google Chrome) \[afternoon\]  
* David Waite (Ping Identity) \[afternoon\]  
* Sam Goto (Google Chrome) \[afternoon\]  
* Rene Leveille (1Password) \[afternoon\]  
* Christian R. (1Password) \[afternoon\]  
* Nick Doty (CDT) \[afternoon\]  
* Helen Qin (Google Android) \[afternoon\]  
* Joseph Heenan (Authlete) \[afternoon\]  
* …