# FedID WG/CG Telecon, 2025-10-07

* Moderators:  Heather

* Scribe: 

* Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

* Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (5 minutes) \*  
* TPAC Planning  
  * What needs high-bandwidth discussion?  
  * Coordination with the payments group(s)  
  * [Breakout Sessions](https://github.com/w3c/tpac2025-breakouts/issues) due by 22 October  
* Any Other Business (AOB)

# Notes

## Administrivia

* W3C code of conduct

## Ecosystem Updates 

* Any updates…nope

## TPAC Planning

* [2025 TPAC](https://www.w3.org/2025/11/TPAC/schedule.html) FedID WG meeting dates:   
  * Thursday, 13 November, @ 09:00-12:30 UTC+9  
  * Friday, 14 November, @ 09:00-12:30 UTC+9  
* Heather:  
  * How many TPAC attendees are remote or otherwise:  
    * Sam, Heather (attending);  Emily, Bjorn, Ted, Alan (remote)  
    * FedID sessions are 9am until 12:30pm  
    * Not sure which days are DC API and which are FedCM yet  
  * Payments groups are interested in both DC API and FedCM  
  * Deeper dive into more difficult issues  
    * For example, multi-idp  
  * Where is the time best spent?  
* Achim:  
  * We are now seeing a larger deployment of FedCM and DC API. What about consolidation of the APIs, or do they live in parallel?   
  * Tim already has that session ([https://github.com/w3c/tpac2025-breakouts/issues/3](https://github.com/w3c/tpac2025-breakouts/issues/3))  
* Tim:  
  * Do not want an hour-long conversation about whether the APIs should exist.  
* Heather:  
  * Breakout sessions are on Wednesday. Those can get us started on issues.   
* Sam:  
  * Two things: IdP registration has a lot of open questions, intersection with the Solid ([https://www.w3.org/community/solid/](https://www.w3.org/community/solid/)) or Social Web WGs (https://www.w3.org/community/socialcg/). The other, the Agentic work.  
* Heather:  
  * Agent authentication is important to talk about  
* Sam:  
  * Yes, this would be good to talk about.  
  * I was waiting until IIW to talk about the Agentic Web.  
* Simone:  
  * Pull in all the people working on credentials for Credentials and Web Payments.  
  * I will talk to Ian about this tomorrow.  
* Tim:  
  * There will be a CG meeting for Agentic, so we should attend that and not create a new session  
* Heather:  
  * Other items, multi-idp could be discussed, which is a CR blocker.   
  * Still open on that list  
* Nicholás:  
  * We closed that.  
* Sam:  
  * Registration is the big open item  
* Nicolás:  
  * And SameSite  
* Sam:  
  * Maybe that is for TPAC, yes.  
* Heather:  
  * Want payment people in the room  
* Yi:  
  * There is work on an API for passkeys, password consolidation, and FedCM. Unified support for credentials.  
  * (Tim) This is similar to my session: [https://github.com/w3c/tpac2025-breakouts/issues/3](https://github.com/w3c/tpac2025-breakouts/issues/3)  
* Sam:  
  * Working on email verification. Either FedID or breakout  
* Heather:  
  * Talk to Tim and Sam about that  
* Achim:  
  * Is that to prevent double email verification?  
* Sam:  
  * Avoiding the magic link email verification  
  * Might not fit into FedID  
* Heather:  
  * Anything else for the list for TPAC?  
  * Can polish things not on the list for IIW  
* Tim:  
  * FedCM for managed browser context, close to IdP registration flow.  
  * This should be a work profile in the browser, and FedCM seems like a good entry point for that.  
* Heather:  
  * Is there an issue, Tim?  
* Tim:  
  * No, thought exercise  
  * Can add an issue.  
* Emily:  
  * I’ve added an issue on Enterprise consent (https://github.com/w3c-fedid/FedCM/issues/715)  
  * You can relate to the one I have  
* Tim:  
  * Yes, we can relate them  
* Sam:  
  * In the context of Enterprise (and consumer), FedCM accounts that come from the OS.   
    * We are actively working on that.  
    * Is not a Web standard, but is worth looking at  
    * Working on Android support for this, not sure how to do this in Windows, iOS, or macOS.   
* Emily:  
  * Edge has the web platform authentication proposal. Would love to discuss that.  
* Sam:  
  * Is related, yes. We can discuss. We are converging to the same point, does this live in a browser or OS, and we are thinking OS.  
  * Are you going to IIW?  
* Emily:  
  * I will be, Suresh is not going to be.  
* Sam:  
  * Making progress on ‘intrusion’, the FedCM widget is more intrusive than it needs to be. So, experimenting with machine learning models and different UX we want to show.  
  * Not a WG thing, but we are working on this.  
  * (Heather) will add to AOB  
* Heather:  
  * Working with Simone and Wendy to take the notes and make a draft agenda.   
* Wendy:  
  * Possibility to visit the payment groups on Wednesday when they meet. TBC.   
  * Breakouts across several days of the week.  
* Heather:  
  * IETF a week before, so might not be there until Tuesday (same as others)  
  * Authenticate next week, so might pull FedCM next week.

## AOB

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Achim Schlosser (Bertelsmann)  
* Phil Smart (Shibboleth/Jisc)  
* Bjorn Hjelm (Yubico)  
* Simone Onofri (W3C)  
* Alan Buxey (MYUNiDAYS Ltd.)  
* Wendy Seltzer  
* Suresh Potti(Microsoft)  
* Christian Biesinger (Google Chrome)  
* Nicolás Peña Moreno (Google Chrome)  
* Yi Gu (Google Chrome)  
* Siddhartha Pandey (Microsoft Edge)