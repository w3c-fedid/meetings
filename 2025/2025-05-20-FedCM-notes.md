# FedID WG/CG Telecon, 2025-05-20

* Moderators: Heather Flanagan

* Scribe: Johann Hofmann

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
* Lightweight FedCM  
  * [approved\_clients in Accounts Push \#61](https://github.com/fedidcg/LightweightFedCM/issues/61)  
* FedCM issues  
  * [Support showing iframe origins in the UI, when they are third-party \#725](https://github.com/w3c-fedid/FedCM/issues/725)  
  * [CR Blocker List](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-\(Consensus-Blockers-for-CR\))  
* Any Other Business (AOB)

# 

# Notes

## Administrivia

* Heather: Reminders given

## Ecosystem Updates 

* Any FedCM implementers want to talk about it?  
  * No volunteers

## Lightweight FedCM

### [approved\_clients in Accounts Push \#61](https://github.com/fedidcg/LightweightFedCM/issues/61)

* Erica Kovac: Normally approved\_clients is fresh from accounts endpoint, needs to be pushed in push model. Do we want the browser to add the IdP to the list automatically, or do we want to have a separate API affordance for that?  
* Phil Smart: No opinion yet, will have a look  
* Heather: Maybe let’s raise this in Slack

## FedCM issues

### [Support showing iframe origins in the UI, when they are third-party \#725](https://github.com/w3c-fedid/FedCM/issues/725)

* Christian: In Chrome today, we show the top-level origin, it’s what the user sees in the URL bar. But you can use FedCM from a cross-origin iframe. But it could be conceptually “first-party”, e.g. ebaystatic and ebay. However, they could also be truly third party, like a third party embedded in a photo editor. There’s no way for the user agent to know which is which. Proposal in the issue suggests sending the top-level origin to the client\_metadata endpoint, and adding a boolean to the returned JSON e.g. client\_same\_toplevel. If true, show top-level origin because it’s the better user experience. Have a prototype implemented. Would like thoughts from the group.  
* Emily: Is the boolean a browser heuristic?  
* Christian: It is set by the IdP in the response  
* Ben: Showing iframe origin in the UI is weird, not common in permission dialogs. The examples I see aren’t particularly strong for even allowing it.  
* Christian: Calling it has been allowed for a long time.  
* Ben: Just talking about showing the origin in the UI.  
* Christian: Depends on how you think about the FedCM prompt \- Payments dialog has it, for example  
* Johann: SAA also has it. Let’s not think about previous permissions patterns too much and just consider whether the user needs to understand it from a privacy and security perspective  
* Yi Gu: Feedback from partners \- they issue the token to the iframe, but we don’t show it, the UI is misleading  
* Ben: Yeah, that makes sense \- in SAA, we have some interaction with the iframe, so the user should know the embed. In FedCM it’s probably just an invisible iframe  
* Johann: But it’s not always an invisible iframe, that’s the point here. There’s the ebay case where it’s invisible, but other examples such as a File hosting provider inside of a photo editor where you’d interact with the file hosting provider as a user.  
* Emily: Yeah, that’s very common (the visible embed case). E.g. sharepoint being embedded in another site, we’d want the iframe branding in that case. But we also have the other scenario. As an IdP, we have both and would know who we’re issuing the token to.  
* Heather: Are iframes ever nested in a way that e.g. sharepoint has an iframe that points to something else  
* Emily: Yeah, Sharepoint can have an iframe that has another iframe inside of it, turtles all the way down  
* Christian: The proposal is just for the actual iframe making the call, not intermediate iframes. If that’s not flexible enough for IdPs we can think about it. Obviously you’ll need the permissions policy anyway.  
* Ben: I’m convinced there’s utility here. I’m convinced that this might be enough flexibility too. Challenge: If presenting just the embed, there’s a pinky promise that gets problematic.  
* Johann: But can the top-level silently access navigator.credentials.get()?  
* Christian: No.  
* Johann: That helps the case that this matches user expectations in my view  
* Ben: Example: Maps iframe, location dialog says top-level because they will get the access  
* Christian: Payments shows the iframe as well  
* Yi: In this case, we just get the information from the IdP \- the browser can still decide for itself which origins to show. The iframe can choose not to share information with the top-level, so maybe communicating this to the end user is also misleading  
* Ben: Ok. I think this is probably useful, but it turns it into a UI problem: How do we present these three origins to the user?  
* Yi: The proposal involves the client\_metadata endpoint, which is not a part of Core, just a heads up for Ben  
* Ben: [Issue 700](https://github.com/w3c-fedid/FedCM/issues/700) is still open? Because of that we can’t ship client\_metadata endpoints. If it was part of the IdP config, we could ship it. Could come from the iframe, it should know.  
* Yi: That could not always be true. E.g. in ebaystatic the Sign-In SDK has no knowledge about it.  
* Johann: Why would the IdP know better?  
* Christian: IdP might have a list of origins associated with the client id and could match.  
* Yi: Was your concern about the timing attack, Ben?  
* Ben: Different concern  
* Heather: Suggestion: Let’s think about this some more.

### [CR Blocker List](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-\(Consensus-Blockers-for-CR\))

* Heather: Got some updating to do on this list. Do it now or side meeting? Any particular items to discuss?  
* Npm: We closed some of them already, we should update it.  
* Heather: Still want the closed ones here, nice to have all of them in one place  
* Npm: would be nice to have a closed table or something like that  
* Heather: Would like to see us move to CR within this year, this table will help us figure that out.  
* Heather: Will set up a call with npm and others to go through this \- anyone want to join? \<crickets\>

## 

## Any Other Business (AOB)

* Wendy and Heather went through the next few months of calls \- will be updating the calendar, apologies for the spam.

	

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Benjamin VanderSloot (Mozilla)  
* Emily Lauber (Microsoft Identity)  
* Yi Gu (Google Chrome)  
* Phil Smart (Shibboleth/Jisc) for 30 mins  
* Parth Bhatt (Independent \- Individual Contributor)  
* Johann Hofmann (Google Chrome)  
* Brian Daugherty (Google Identity)  
* Erica Kovac (Google Chrome)  
* Christian Biesinger (Google Chrome)  
* Zachary Tan (Google Chrome)  
* Nicolás Peña Moreno (Google Chrome)  
* Wendy Seltzer  
* Simone Onofri (W3C)  
* Bjorn Hjelm (Yubico)  
* Ketan Mehta (NIST)  
* Chris Fredrickson (Google Chrome)  
* Theo @thhck \- Solid CG

