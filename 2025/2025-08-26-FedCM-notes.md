# FedID WG/CG Telecon, 2025-08-26

* Moderators: Heather Flanagan

* Scribe:  Dan Moore

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * [2025 TPAC](https://www.w3.org/2025/11/TPAC/schedule.html) FedID WG meeting dates:   
    * Thursday, 13 November, @ 09:00-12:30 UTC+9  
    * Friday, 14 November, @ 09:00-12:30 UTC+9  
* Ecosystem Updates  
  * Update from Phil Smart's testing  
  * [Email autocomplete](https://github.com/dickhardt/verified-email-autocomplete)  
* Issues & PRs  
  * n/a  
* Any Other Business (AOB)

# Notes

## Administrivia

* Heather: TPAC meetings are Thu Nov 13, Fri Nov 14\. Times are UTC \+9. FedCM will be focus on one of these days.  
* IIW dates have moved.

## Ecosystem Updates 

* Phil: Been looking at [issue 618](http://github.com/w3c-fedid/FedCM/issues/618).   
  * IdP proxies are commonplace in research and education for protocol translation, facing multi-lateral federation (common in UK), additional assurances like MFA, hiding upstream IdPs.  
  * Has been looking into support for this via FedCM. Has a video.  
  * FedCM RP talking to Proxy IdP, which is talking to an authentication server(?)  
  * Two scenarios, one with a stateless forwarding proxy and the other with a stateful proxy holding session. The second is more interesting/problematic and he’s looking for guidance on that.  
  * Phil walked through the second scenario.  
    * Interaction with proxy is in active mode, then the interaction with the upstream server is passive.  
    * After login with the upstream, the proxy stores the token.  
    * RP requests account endpoint.  
    * Proxy pulls out the account, presents that to the RP.  
    * Proxy then delivers the upstream token to the RP.  
    * After RP logout, proxy has upstream token (if it hasn’t expired).  
    * The biggest limitation is that the proxy only shows you the account it has an assertion for. Some UI/UX issues as well (he’s more concerned with the technical issues).  
  * Phil walked through the first scenario as well.  
    * Initiate FedCM with proxy IdP; proxy then lets you log into the upstream IdP.  
    * Proxy is going to get assertion from upstream, but will drop it because it is stateless. It can’t give a token to RP.  
    * Next, FedCM tries to go to proxy, but no accounts are available (because they were dropped), so back to login, then back to accounts, etc. Used to go into a loop; that doesn’t happen now.  
    * Best understanding is that you have to have a stateful proxy for FedCM to work. Also limited to one account until a token expires.  
  * Also showed a video of the scenario where the proxy does redirects not FedCM.  
  * Accounts endpoint can’t follow redirects, so you can’t have backchannel communication to the upstream.   
    * You could have the proxy do some backchannel communication, but not part of standard and not coming from the browser.  
  * Stateful is what comes closest to working implementation, and what he showed was pretty simple in comparison to some topologies.  
* Sam:  
  * It was useful. Can you share the video later?  
  * Two things:  
    * Trying to think about incentives. What do people get by using FedCM that would justify this amount of work? Is there a way to break this problem into smaller parts?   
    * Third party cookies and link decoration already work. Why do we need to change the tree of IdPs? Why do they need to move to FedCM?  
    * Phil showed the how, Sam is stuck in the why.  
* Phil:  
  * Worried about link decoration and redirect issues, thought of this as a FedCM flow because of that.  
  * If that doesn’t happen, no reason for folks to do what he showed.  
  * Looking for issue resolution started long ago by Judith, others, and him. Maybe the answer is that FedCM isn't the answer, just worried about the future.  
  * If it can keep doing proxy via redirects, no problems.  
* Sam:  
  * None of us have scope to make predictions about link decoration. No browser vendor has found a way to block link decoration without breaking the entire web. Not necessary now, not sure about the future. In future things will be different. If you can solve this problem now, we still don’t have incentives for people to use it.  
* Phil:  
  * Lots more console logging showing up, thanks for that.  
* George:  
  * Sam, you propose an interesting solution to the problem. The privacy CG group stopped working on navigational tracking because FedCM is going to solve the problem.  
  * If industry agrees that navigational tracking is okay, then this solution is okay.  
  * There could be issues with other groups proposing to stop navigational tracking.   
  * Need to get agreements from others that we aren’t going to block identity redirects for foreseeable future.  
* Sam:  
  * Yes, we need to coordinate.  
  * Maybe write a note about this.  
  * Solving navigational redirects is in-scope in the long-term, but fine to have a solution that doesn’t solve everything right now.  
  * There are use cases that rely on nvaigational redirects that are not solvable today.  
* George:  
  * Okay in the future to break how FedCM works now.  
  * Might constrain FedCM 2.0 with choices we make for FedCM 1.0 (w/r/t navigational tracking). If 2.0 breaks 1.0, that affects uptake  
  * Would be nice to have assurances.  
* Sam:  
  * This might be a one-way door.  
  * The incentives are still obscure.  
  * Not technicaly cornered  
  * Possible statement:  
    * “Please make sure you are aware that there are plenty of use cases in identity federation that are not solvable by FedCM today”  
  * No easy solution for this. If it was easy, we would have already solved this.  
  * The problem feels artificial when considered in the context of incentives because people can escape to lower level primitives. Until navigational tracking gets mitigated.  
  * Would a note acknowledging the state of this (that redirects are okay for some use cases) that there’s no need for transition to anything solve this problem?  
* Phil  
  * As long as there were sufficient warning about changes in the future, it’s acceptable.  
* Sam:  
  * Can you and I write something down and see if we can get to a resolution? Also will include George.  
* Sam  
  * Talking about email autocomplete.  
  * [https://github.com/dickhardt/verified-email-autocomplete](https://github.com/dickhardt/verified-email-autocomplete)  
  * Working with dick hardt.  
  * Verification of email addresses is the problem they are trying to address. Big part of web identity and sign up flows and account recovery flows. Also for second factors.  
  * Collected data on how many websites use this. Surprise how many who are using it.   
  * Email verification is done almost exclusively via proving the user has access to the email inbox.  
    * Email acquired  
    * Website signs non-guessable code to email  
    * The user goes to their inbox, gets code, then pastes it into the input box.  
  * Happens for consumers, enterprises, education.  
  * Dick and Sam are EXPLORING (emphasis his) a proposal to hook in a protocol that allows the user to give to the website cryptographic proof of email address ownership. Skips manual steps.  
* Dan: How big a problem is the current process?  
* Sam: From a  design of incentives, it’s a three-way entity.   
  * Drop off costs in acquisition funnels. For every user that tries to verify an account, there’s dropoff. No concrete numbers, meaningful amounts based on conversations with developers.  
  * Email verification can fail/drop off for many reasons  
    * Spam folder  
    * Time/async  
    * Context switching between web app and email app  
  * For users, it’s friction to have to context switch.  
* Tim:  
  * Had the same conversation with Dick, fears Dick wants to use email address as the account identifier. We’ve moved away from that, and Tim fears we are heading back that way.  
* Sam:  
  * Equally concerned about that.  
  * In practice, email acquisition is used by a majority of top 100 sites.  
  * Can construct different dataset  
* Tim:  
  * Talking about identifiers at the back end, not how the user identifies.  
* Sam:  
  * Agree. Ideally have shielded email addresses.   
* George:  
  * 100% agree Tim, never use user mnemonic as an identifier.  
* Sam:  
  * Move on?  
* Heather:  
  * Scope question: how do you see this fitting in with what this group works on?  
  * In FedCM? Separate work item?  
* Sam  
  * Initial version is built on top of FedCM and has the browser more involved.  
  * From a use case perspective is similar, people use federated login to get access to verified email addresses.  
  * Email is in some way a cross-origin identifier.  
* Tim:  
  * At some point, we should ask the question about if this is a digital credentials API with a wallet.  
  * Would that make extensibility model easier too if we followed that pattern (plug into wallet natively).  
  * Digital credentials debate should happen.  
* Sam:  
  * Been thinking that we should have that discussion once we know what we want to build.  
  * FedCM provides needed infrastructure.   
* Tim:  
  * Is this an opportunity to kill two birds with one stone that don’t like the fact they need a native app for credentials.  
  * SD-JWTs could be in some wallet, and the wallet is built into Chrome/the browser.  
  * Let prototyping continue with FedCM, but consider this in the future.  
* Heather:  
  * Would be good conversation for IIW  
* Sam:  
  * Architecturally speaking, for digital credentials the browser does nothing.   
* Tim:  
  * Had same debate for 5 years how a traditional password manager should integrate.  
  * In theory, would be a huge shift, when Chrome goes to query the platform, it could send requests from itself too.  
  * Don’t limit decisions, this just adds a new capability to the browser.  
* Sam  
  * The part that is hard is privacy, UX, protocol. Retrofitting is the easy part.  
* Sam  
  * Protocol is simple.  
  * Aiming at having no UX at all. (Same as acquisition.)  
  * Same as getting an unverified email address.  
  * Easier for users.  
  * Need to make sure we meet right privacy boundaries.  
  * Mechanism (should review linked explainer)  
    * Upon selection of autofill, send DNS request, ask for issuer fo email provider.  
    * Email provider makes SD-JWT assertion for account.  
    * Use browser cookies.  
    * Browser does keybinding to the email address, then returns proof  
    * … There was something about communicating with the identity provider …  
    * Identity provider doesn’t learn anything  
* Heather:  
  * Need further discussion about whether this should be part of this group.  
* Sam   
  * Happy to chat more about this.

## Issues & PRs

* 

## Any Other Business (AOB)

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting, co-chair)  
* Sam Goto (Google Chrome)  
* Christian Biesinger (Google Chrome)  
* Dan Moore (FusionAuth)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* Bjorn Hjelm (Yubico)  
* Emily Lauber (Microsoft Identity)  
* Alan Buxey (MyUNiDAYS Ltd.)  
* Wendy Seltzer (co-chair)  
* George Fletcher (Practical Identity LLC)  
* Phil Smart (JISC)  
* Tim Cappalli (Okta)  
  