# FedID WG/CG Telecon, 2025-04-22

* Moderators: Heather Flanagan

* Scribe: Phil Smart

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (5 minutes)  
  * IdP/RP implementations  
* FedCM issues  
  * [Why must SameSite=none? \#587](https://github.com/w3c-fedid/FedCM/issues/587)  
  * [FedCM "core": move "extensions" out of the current spec into an independent spec \#703](https://github.com/w3c-fedid/FedCM/issues/703)  
  * [Does "core" need to introduce feature detection for features in "extensions"? \#713](https://github.com/w3c-fedid/FedCM/issues/713)  
  * [Enterprise Scenarios: admin consent for users \#715](https://github.com/w3c-fedid/FedCM/issues/715)  
* FedCM PRs  
  * [Set limit on size of providers \#711](https://github.com/w3c-fedid/FedCM/pull/711)  
  * [Add phone and username attributes \#718](https://github.com/w3c-fedid/FedCM/pull/718)  
* Any Other Business (AOB)

# 

# Notes

### Administrivia

* 

### 

### Ecosystem Updates 

* Erica Kovac  
  * In progress developing accounts push for Lightweight FedCM mode  
  * Flag is Lightweight-FedCM  
  * Will add link to proposal to allow folks to start playing with it  
  * Very early — prob not DevTrial-ready yet, but would be good for people to try  
  * Explainer:  
    * 3 different feature additions to FedCM as opposed to a completely separate mode  
    * Had been getting lots of confusion and questions from partners about that, so hopefully this clears up confusion people had been having

### FedCM issues

* [Why must SameSite=none? \#587](https://github.com/w3c-fedid/FedCM/issues/587)  
  * Heather  
    * Seems like it is still a blocker for some folks  
    * Anders said he’s unblocked but not sure about security solutions  
  * Christian  
    * Summary seems to be to support \`SameSite \= Lax\`  
    * People seem to be generally in favor  
    * Not sure if Mozilla has thoughts on this change?  
    * On Chrome side, various Security and Privacy people seem to be ok with it  
    * Still need to talk to Networking people (Chrome) to see what changes would be needed to implement  
  * Ben  
    * From Mozilla’s perspective, not something we want to die to add  
    * But if it unblocks use-cases for people migrating to FedCM, seems like a win  
    * Still need to talk to Security folks about whether it is OK and a good idea  
    * And if so, seems like a good thing  
    * Rapidly converging to a normative description of Fetch Spec  
    * Spec language should be relatively easy.  
    * The big question is: Are all parties OK with adding another use-case of Lax?  
    * Anand (?) would be the person who would most be likely to block this  
    * If there isn’t an objection from Apple, we’d be happy to implement it (assuming OK with Mozilla security folks)  
  * Christian  
    * OK — seems like the summary is to proceed to push for this then  
* [FedCM "core": move "extensions" out of the current spec into an independent spec \#703](https://github.com/w3c-fedid/FedCM/issues/703)  
  * Nicolas  
    * Already marked things we’re moving to extensions as a Note with issue label  
    * Not sure if anyone has looked at those  
    * Is the next step to actually create extensions repo?  
    * Also debating whether there should be just one extension repo vs. lots of extension repos.  
  * Heather  
    * From editor perspective, having lots of repos is annoying  
    * But for developers, it would be easier to split into multiple repos to avoid having developers needing to go through the whole thing  
    * Also: Separate documents in the same repo vs. multiple documents in one repo vs multiple repos for different features  
  * elf Pavlik (chat)   
    * separate repo or separate documents in the same repo? one could use labels if it is in the same repository  
  * Nicolas  
    * Benefit could be separate issue lists for different features  
    * But still seems overkill to have multiple repos  
  * Heather  
    * Maybe take it offline with Nicolas and hash out pros and cons and then present a proposal next time?  
  * Nicolas  
    * Sounds good  
* [Does "core" need to introduce feature detection for features in "extensions"? \#713](https://github.com/w3c-fedid/FedCM/issues/713)  
  * Nicolas  
    * Wanted to ask developers / IdPs: do you feel like you are going to need feature detection?  And if so, what would be the rough shape?  
    * A method based on parameters?  Input string?  Something else?  
    * With Firefox implementing and shipping in near term, this will be more important (instead of just Chrome vs. not-Chrome)  
    * Especially if Firefox’s implementation might have some feature differences  
    * So, the need to feature-detect available features is more important  
  * Erica  
    * Suggest: Ben have you given thought to how Firefox would behave if \`mode=passive\` is specified?  
  * Ben  
    * Won’t throw exceptions as there are some cases where Passive Mode will actually be supported.  
  * Erica  
    * For the cases where passive is NOT supported, will there be a signal for that?  
  * Nicolas  
    * Not sure if that is feasible (in Chrome, we don’t give that signal)  
  * Ben  
    * Chrome has a block somewhere / relatively opaque mechanism  
    * Would be useful to have some sort of feature detection   
    * Should be easy to implement  
    * Have to figure out where to hang it and what args are  
  * Phil  
    * There’s what the RP can do but Christian also suggested feature detection for the IdP as well  
    * (compared to what the RP can expect and do)  
  * Ben  
    * This would be feature detection of whether the browser supports the Extensions  
    * Could you rely on metadata / policy prompt vs. having to do some UI of your own   
  * Christian  
    * Some of that is handled by Continue-on and Fields (in terms of whether they have to do their own UI)  
    * But not Privacy Policy part  
  * Phil  
    * Would need to know if browser supports Continue-On  
  * Nicolas  
    * Seems like that it is necessary  
    * We can add anything we want to feature detection, so if it seems useful we could add it.  
  * Phil  
    * Yes — would be good to know if continue-on is supported, as UI flow from IdP might be different in those cases  
  * Christian  
    * Wouldn’t expect an implementation to ship without continue-on at this point, as it seems pretty important  
  * Aaron  
    * Generally agree  
    * Would be important for some things  
    * IdP would want to provide some pre-emptive UI or messaging based on available of features  
    * E.g., IdP Registration — user would want to know what the button does / provide explanation to encourage user to click the button  
  * Christian  
    * Can detect to see whether function exists on the object  
  * Aaron  
    * For sure — just wasn’t sure how feature detection would work in the different cases  
  * Emily  
    * Was also going to ask about continue-on  
    * As far as other mechanisms for feature detection — would have to look at specs to figure out what would be appropriate for each feature, but Feature Detection in general seems good / necessary.  
* [Enterprise Scenarios: admin consent for users \#715](https://github.com/w3c-fedid/FedCM/issues/715)  
  * Emily  
    * Talked about in F2F  
    * Not really the end user who consents — it’s the Enterprise Admin who consents  
    * So we need mechanisms that would allow the browser to trust that this RP / IdP relationship is good / trusted  
    * In the discussions, there were 4 possible ways:  
      * Enterprise Policy  
      * Managed browser?  
      * Extension that the IT could push or user could click to add  
      * Browser profile  
      * Operating system account   
    * Johann had mentioned that the last two could be potentially injected into FedCM (but would need further explanation)  
  * Nicolas  
    * What is trying to be achieved  
    * Is it auto-grant for a trusted site with an IdP?  
      * Seems maybe a bit strange  
    * Also not sure which Enterprise Policies would be appropriate  
    * Doesn’t think like something we could allow for general public  
    * If logged into Windows, doesn’t mean I want to sign in with Windows to every website  
    * Wondering what the use-case is — is it full auto-grant or something else?  
  * Emily  
    * It may be arbitrary RP from browser’s side, but there is a pre-existing relationship with IdP and RP  
    * That’s the disconnect — the browser doesn’t know which RPs the IdPs has consented to  
    * And how to allow the Browser to know / trust that that relationship   
    * Also push back on enterprise that the user’s Windows account and it is not a multiple-account scenario, then it is likely the case that the user would want to sign into RPs with   
  * Ben  
    * This goes back 3 years of FedCM discussions  
    * How do you convince us (the browser) that the IdP and RP relationship is pre-consented?  
    * Impossible to tell those relationships from Web trackers  
    * Separating out the entities of OS Admin or some sort of device admin and device provider  
    * Who is the same entity here?  
  * Emily  
    * Great question  
    * When talking Microsoft, talking about Enterprise Identity Provider  
    * They would have access to different device platforms  
    * I’m on my Enterprise-managed Mac, for example  
  * Ben  
    * So, a browser extension endpoint where this IdP works on these RPs / sites  
    * Would that meet demands?  
  * Emily  
    * In fully managed scenarios, Enterprise Policies work great  
    * But it’s BYOD scenarios  
    * Schools in particular  
    * School has consented to which RPs the school has consented to  
    * So, maybe a Browser extension is the way for non-managed scenarios  
  * Ben  
    * You could have user control as well  
    * These are all the things which have 3P cookie access or some user-controlled way  
  * Emily  
    * What is a user-controlled way?  
  * Ben  
    * If outside context of getting an Enterprise Policy  
    * Out to enable that   
    * There has to be some sort of user-affirmative step  
  * Sam  
    * Wondering if Nicolas and Ben, before we talk about the harder cases, what are simpler cases?  
    * Agree that within Enterprise Policy they would want to have the IT Admin waive some of these (FedCM) permission checks?  
  * Phil  
    * Seems reasonable  
  * Ben  
    * Seems reasonable, but would have to talk with more Mozilla folks  
    * Person owning device can grant anything  
  * Nicolas  
    * Not sure — having Enterprise Policy shouldn’t mean that the user waives all privacy rights to the admin  
    * Not user what our Privacy stance is on Enterprise Policies  
    * Guess is that it is \*probably\* ok, but still a bit worried   
    * Could mean that you could use Enterprise Policy to link any site to the Admin and maybe Enterprise Policies are good enough already  
    * But we’ve seen cases where there could be better understanding but not sure if this is a case where this is needed  
  * Sam  
    * Isn’t it possible that Enterprise Policies can re-enable 3PC?  
  * Chris  
    * There are Block and Allow controls for 3PCs in Enterprise Policies  
  * Sam  
    * That seems like stronger controls than Emily’s proposal  
  * Nicolas  
    * Yes — might be over-thinking it  
  * Sam  
    * So, it sounds like both Enterprise Policy and Browser Extensions are easy cases  
    * They get to override lots of things and we are not proposing anything more powerful than existing capabilities of those.  
    * So those might handle Emily’s cases?  
  * Emily  
    * Those are “easy” from browser profile perspective  
    * But that pushes a lot more need for Enterprise’s IT or IdP to deploy them  
    * Which are historically not as reliable  
  * Yi  
    * Some IdPs / Enterprises allow people to sign into both Managed Account and Personal Account in the same Browser Profile  
    * For Managed cases, it seems fine  
    * But for Personal account, not sure  
    * If I go to a new RP, want to make sure that the browser doesn’t auto-sign in using personal account when enterprise account would be more appropriate  
  * Emily  
    * As an IdP, when the IdP fully controls the UX if the IdP knows there are multiple accounts, RP sends a login hint or show an Account Picker in that scenario  
    * Scenario that is more concerning is the just-one-account  
  * Heather  
    * Not sure there is a full resolution  
    * But there are some ideas for comparatively easier scenarios  
    * But still need more time for more complex scenarios  
    * Please review the issue and come back with comments in next mail   
  * From zoom chat  
    * Zacharias Törnblom: Sounds like federation. Is that an accurate interpretation?  
    * Phil: Which would be a bit like: [https://github.com/w3c-fedid/idp-registration/issues/18](https://github.com/w3c-fedid/idp-registration/issues/18)  
    * alan buxey: This is to just ensure/allow the IdP to be appearing at the relevant services that the organisation uses \- so helping the user with the first step of IdP registration ?  
    * Ben VanderSloot: Not quite- I understand it to be bypassing FedCM UI for IdP-RP pairs  
    * Emily Lauber: Depending on the scenario, the user wouldn’t have to enter their credentials. Currently if using redirects, the RP redirects to IDP, IDP has access to 3p cookies and knows there is one account with active session and are available to this RP, IDP redirects to RP with successful login and no user action is required

### FedCM PRs

* [Add phone and username attributes \#718](https://github.com/w3c-fedid/FedCM/pull/718)  
  * Christian   
    * Want to ship this in Chrome M137 (branch point coming up soon)  
    * Have previously discussed shape of feature  
    * Just want to settle on name the phone number field  
    * Previously was “phone” that Christian made up  
    * TAG said we shouldn’t make things up  
    * HTML 5 naming would make more sense  
    * So, “tel” in that case  
    * Wanted to see what people think / object?  
  * Ben  
    * Agree with TAG and “tel” is the right choice  
  * Heather  
    * Objections?  
    * None  
    * Conclusion: Go for “tel”  
* [Set limit on size of providers \#711](https://github.com/w3c-fedid/FedCM/pull/711)  
  * Nicolas  
    * Sent PR \- objections came in  
    * Could be up to browser vendor on what limits are appropriate  
    * Might just withdraw PR  
    * Context: PR is about limiting number of providers they can pass to FedCM get() call  
    * Why specify a limit?  
    * Each IdP that is passed in requires various fetches to endpoints  
    * Also, might it be possible to gain information if lots of IdPs are passed in?  
    * But also there are potentially lots of IdPs so maybe passing in lots would make sense?  
    * But IdP Registration API might help with that (only register those that people actually use)  
  * Ben  
    * Think the key here is that because we don’t have spec language for IdP Registration, those cases aren’t covered  
    * So, that makes a limit more reasonable  
    * Not a bad idea (as opposed to 2 weeks ago when initial reaction was more objectionable)  
    * Having this separate from IdP registration cases will be critical  
  * Phil  
    * On the efficiency of it  
    * No matter how many IdPs are provided in the list, it will only send fetches to ones the user is signed in to?  
  * Christian  
    * Problem is those IdPs that are in the “unknown” state, which will get at least one initial fetch  
    * But then the state becomes known (Logged In / Logged Out) and that state persists  
  * Nicolas  
    * Config / Accounts / Client Metadata / .well-known  
    * Those 4 endpoints are the things that get fetched  
  * Ben  
    * UI issues are another concern, but those could potentially be resolved  
  * Sam  
    * Also thought: Don’t we allow websites to kick off 1,000 image fetches or tags?  
  * Nicolas  
    * We already have lots of concurrent fetches  
    * Just will take a longer time to complete  
  * Sam  
    * It is the website’s choice on how many IdPs it  
  * Phil	  
    * If the RP sent 5,000 IdPs because it wanted the user to choose among them, then that could cause a problem  
    * But that’s not how selecting among them would actually work.  
  * Heather  
    * Didn’t hear “withdraw” — seems like more convo is needed  
  * Nicolas  
    * Conclusion: keep the issue open / no rush  
    * Can revisit when we try to specify IdP Registration API  
    * So maybe just punt it to then?

### 

### Any Other Business (AOB)

	

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* Phil Smart (Shibboleth/Jisc)  
* Alan Buxey (MyUNiDAYS Ltd.)  
* Benjamin VanderSloot (Mozilla)  
* Michael Knowles (Google Chrome)  
* Christian Biesinger (Google Chrome)  
* Nicolás Peña Moreno (Google Chrome)  
* Parth Bhatt (Individual Contributor)  
* George Fletcher (Practical Identity LLC)  
* Erica Kovac (Google Chrome)  
* [elf Pavlik](https://elf-pavlik.hackers4peace.net) (independent, Solid CG)  
* Simone Onofri (W3C)  
* Ryan Galluzzo (NIST)  
* Mike Jones (Self-Issued Consulting)  
* Monty Wiseman (Beyond Identity)  
* Bjorn Hjelm  
* Frank Somich  
* Sam Goto  
* Joel Antoci (Shopify)  
* Emily Lauber (Microsoft Identity)  
* Alex B Chalmers  
* Aaron Parecki  
* Michael Jones  
* Yi Gu (Google Chrome)  
* Chris Fredrickson (Google Chrome)  
* Zacharias Törnblom  
* [Ted Thibodeau](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* 

