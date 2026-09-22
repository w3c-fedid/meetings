# FedID WG/CG Telecon, 2026-09-22

* Moderators:  Heather Flanagan

* Scribe: Scott Lanoue

* Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

* Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * [FedID CG/WG process](https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md)  
* Ecosystem Update (5 minutes)  
* Discussion (25 minutes)  
  * TPAC planning  
* AOB

# Notes

## Administrivia

* Participants have agreed to relevant Code of Conducts  
* Call for questions \-- nothing to share

## Ecosystem Updates (5 minutes)

### FedCM in the wild updates

* Sam: presented some of the mocks to the Bluesky community  
  * Lots of validation, “handwavy” nothing too concrete   
  * Devin from Bluesky is excited to move forward with implementation  
  * Trying to determine resourcing to figure out who/how this can be implemented  
  * Christian left Google for Igalia and hopes to continue working on this / similar things  
* Emelia: working out how FedCM can integrate with existing services  
  * DPOP can be figured out via FedCM params and id\_assertion endpoint can be used instead of using a PAR (Pushed Authorization Request) or Authorization request  
    * Answers one of Emelia’s long standing questions on this work *(would still be interested in DPoP from the service workers folks)*  
    * Receive an Authorization code on response  
    * Longer term IETF draft for token exchange NOT using Authorization code grant  
    * Sam: Did you get to connect with Aaron on this work, I believe he used DPOP?  
      * Emelia: I did not, I don’t think he’s using DPOP but we do need to re-sync  
  * Wants to figure out the Fields ecosystem  
    * Fields API makes a lot of sense when you don’t want to return a security credential, better for just returning a handle  
    * Sam: Agreed, have you looked into how EVP works?  
      * The browser is more involved in the key binding and selective disclosure  
      * This increases interoperability between clients as opposed to each individual verifier  
    * Emelia: The identity assertion endpoint and accounts endpoint aren’t clear how they flow in the Fields API  
      * There should be another response property that is the fields themselves  
    * Sam: Yes I think this might be in EVP, every field is what the relying party has requested. Fields aren’t returned by the Identity Provider because the browser doesn’t open the request  
      * This might potentially be a bit of bike shedding?  
    * Emelia: we have 3 things in the response: token, an error, and continue on  
    * Sam: There’s one we introduced as well, redirect-to  
      * Browser knows what to do with these fields  
    * Emelia: The fields API could know and only return the relevant fields, if the IdP returns more fields than the browser requested  
    * Sam and Emelia are in agreement that Fields API is not doing this perfectly  
      * Sam suggests looking into EVP to see how it handles it  
    * Sam: If the browser makes a verification the same as a verifier would do, it makes this more interoperable \+ adds a reference impl.   
    * Heather: Sounds like Emelia has found a potential problem, and Sam has a potential solution/workaround. Are you (Sam) going to bring this over from EVP?  
    * Sam: Potentially, need to sync with Emelia to determine if this can be utilized to port this from EVP into FedCM  
    * Emelia: Unfamiliar with mechanics of EVP but specifically concerned about Fields API and curious to know if it is fully fleshed out (or not)  
    * Sam: This was removed from core because Firefox wasn’t implementing the disclosure box (at least, a couple years since this conversation), instead using OAuth scopes and continue\_on  
      * Fields API handles the authentication case without extra OAuth scopes. Just gives an ID token, not necessarily a full access token  
    * Emelia and Sam agree that limited scopes are best, Sam questions what is required in Bluesky because of access to the PDS  
      * Sam: Are read and write access required for communicating with the user’s PDS?  
      * Emelia: No because of the current public data implications of the PDS, not dependent on Spaces (private data in AT Protocol). Read access is implicit today  
    * Sam: There needs to be a way to get the handle  
    * Sam: EVP defines what the token looks like, how it’s encoded, selective disclosure, key binding, handle resolution  
      * When someone is developing an issuer, they develop it against a Browser which can help it become a reference verifier  
    * Heather: Really interesting, there might be some homework for Emelia to dive into EVP, then syncing with Sam on potential improvements that can be brought over into Fields API? Also maybe a bug/issue that needs to be filed with FedCM?  
      * [https://github.com/w3c-fedid/FedCM/issues/846](https://github.com/w3c-fedid/FedCM/issues/846)   
    * Emelia: Agreed, also have another concern with EVP's approach is would it stand true for all uses of the Fields API? I.e., you never notify the IdP who is requesting the information from the Fields API, much like EVP today, where it doesn't use the ID Assertion endpoint at all.  
    * Sam: Yes but unsure about all implications  
    * Heather: We discussed EVP in the last call but we haven’t brought it into this group yet.   
      * Working Group charter is up for review (Feb. 2027\) — what should be the focus?  
      * FedCM on the REC path (or not), or should it remain a community item?  
      * Going to have to make discussions at TPAC  
    * Emelia: Potentially a conversation to have with Igalia so that it can be brought over to other Browsers  
    * Sam: This should be working group, not community group, maybe not ready to be moved over *just* yet  
      * Either would work with Chrome  
* Emelia: What’s the status of defining the “core” profile here?  
  * Heather: Still being determined, it’s only Chrome for now  
  * Emelia: Okay, is there progress on getting this written \+ published \+ shared so that we can start conversations around this?  
  * Wendy: Is there interest in a community group member to start writing this?  
  * Emelia and Heather in agreement on beginning to write this  
    * Heather: Would be great to have this by TPAC  
    * Emelia: Could we try to cover IdP Registration as part of this?  
      * Answer was "yes, that would be the idea", i.e., forward looking version of "core" even if extensions haven't yet reached stage 2 (i.e, IdP Registration)  
  * Sam: Mozilla is privy to these conversations  
    * Only remaining blocker is candidate registration  
  * Heather: Agreed on the big blocker, but all of the little pieces are also additive blockers  
  * Sam: Also agreed, but I only see 1 or 2?  
  * Heather: Maybe we’re looking at different places, because I see \~ a hundred smaller blockers  
  * Sam: Is everything in [https://github.com/w3c-fedid/FedCM/issues](https://github.com/w3c-fedid/FedCM/issues) a blocker  
    * Was under the idea it was a small subset of issues, not all of them  
  * Nicolas: Maybe there needs to be a clarification on what is a blocker vs. non-blocking issue in this queue  
  * Heather: There should be a tag (label) that defines what is blocking here  
  * Nicolas: So is the goal that we have 0 open issues with the blocking label in this queue?  
  * Wendy: Clarifies that the w3c process requires a formal address of all issues raised since the last maturity stage of a project  
    * [https://www.w3.org/policies/process/\#transition-reqs](https://www.w3.org/policies/process/#transition-reqs)  
  * Emelia: Do we need a weekly triage meeting on these issues with a subset of members / interested parties?  
    * Sam agrees  
  * Heather is partially in agreement, but wants to ensure inclusivity while also recognizing prior attempts at including this in the bi-weekly sync becomes a snoozefest  
    * Emelia agrees, but notes that there have been issues with other triage meetings she's participated in in the past.  
* Emelia: Cross-site scripting risk, how can this be avoided in the FedCM login process?  
  * Discussed this draft at IETF OAuth Interim yesterday: ([https://www.ietf.org/archive/id/draft-hardt-oauth-protected-authorization-00.html](https://www.ietf.org/archive/id/draft-hardt-oauth-protected-authorization-00.html))   
    * Group decided against adopting it because the draft doesn’t fully acknowledge the problems at hand  
    * This draft is attempting to protect OAuth query parameters in the redirect, “hiding from them from the user”  
    * Cases where an attacker starts a login chain and then hands that over to the victim to hijack their login flow  
    * slides from IETF 124, browser swapping, [https://datatracker.ietf.org/meeting/124/materials/slides-124-oauth-sessa-browser-swapping-01.pdf](https://datatracker.ietf.org/meeting/124/materials/slides-124-oauth-sessa-browser-swapping-01.pdf)  
    * Heather: Is Dick going to be working on this, or dropping this?  
    * Emelia: I had the feeling that he is going to drop this without OAuth WG adoption  
    * (from Bumblefudge in Zoom chat): is Sam dropping it, too? 😏  
      * Emelia: Yes, I saw that as well  
      * Sam: Yes, part of my job is to make changes to improve the security and usability around OAuth in browsers. Unfamiliar with what exactly Dick proposed, but if it fits in here then yes, but not exactly planning on doing this work  
    * Emelia: Also mentioned during that meeting the Idp-Initiated FedCM proposal, in case there's overlap  
  * Emelia: FedCM is Javascript, so it's hard to avoid cross site scripting attacks, besides requiring CSP and HTTPS and similar measures.

## Discussion (25 minutes) 

### TPAC Planning

## Any Other Business (AOB)

* Heather: Wraps up the meeting due to time constraints. Thanks Scott for Scribing

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* Wendy Seltzer (co-chair)  
* Nicolás Peña Moreno (Google Chrome)  
* Scott Lanoue (Community Group)  
* Bjorn Hjelm (Yubico)  
* Emelia  
* Sam  
* Bumblefudge  
* 

### Regrets

* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))

