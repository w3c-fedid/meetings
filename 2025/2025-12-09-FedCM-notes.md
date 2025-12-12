# FedID WG/CG Telecon, 2025-12-09

* Moderators:  Heather

* Scribe: AI Zoom Notetaker

* Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

* Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (5 minutes)  
* Issues and PRs  
  * [Delegation-oriented FedCM](https://github.com/w3c-fedid/delegation) status  
* Any Other Business (AOB)

# Notes

## **Key takeaways**

* Chrome is working on FedCM interception features that will be available in Chrome Canaries soon  
* Delegation-oriented FedCM is being explored as a potential "end state" for FedCM with better privacy properties  
* Shopify expressed interest in implementing delegation-oriented FedCM, and Okta may also be interested  
* There's a prototype for delegation-oriented FedCM available in Chrome Canaries that developers can test  
* Breaking changes to FedCM were announced in the FedCM newsletter  
* Same-site legacy cookies implementation is available behind a flag in Chrome for testing

## **Discussed topics**

### **AI Transcription Setup**

Brief discussion about enabling AI transcription for the meeting.

* **Details**  
  * Simone: Suggested enabling transcription so a human could fix AI errors later  
  * Joel: Confirmed seeing a banner about AI transcription  
  * Christian: Noted the transcription message appeared and disappeared  
  * heather: Expressed some skepticism but proceeded with the meeting

## Ecosystem Updates (5 minutes)

* **Details**  
  * goto: Mentioned several features being pushed out in coming months  
  * goto: Highlighted interception as a key feature coming to Chrome Canaries soon  
  * goto: Mentioned upcoming intent to prototype for connecting with Android apps  
  * Joel: Asked for clarification on what interception is  
  * goto: Shared links to the interception explainer and intent to prototype  
  * goto: Noted interception might be more applicable to Microsoft than Shopify, but could be interesting in the context of AI agents

### [Delegation-oriented FedCM](https://github.com/w3c-fedid/delegation) status

Extensive discussion about the status and future of delegation-oriented FedCM.

* **Details**  
  * heather: Asked for updates on delegation-oriented FedCM  
  * Christian: Explained they've been focusing on email verification, which doesn't need an accounts list  
  * goto: Provided historical context about the three variations explored for FedCM: permission-oriented, mediation-oriented, and delegation-oriented  
  * goto: Explained that delegation has always been seen as a better end state but was more difficult to implement due to backward incompatibility with relying parties  
  * goto: Confirmed there's a working prototype in Chrome Canaries that developers can try  
  * goto: Noted that individuals from Apple and Firefox have expressed preference for the delegation approach  
  * Joel: Expressed Shopify's interest in exploring delegation-oriented FedCM implementation  
  * Joel: Asked about the process for prioritizing development efforts on this version of FedCM  
  * heather: Explained that having more entities express interest would help prioritize the effort  
  * goto: Highlighted that Shopify is an interesting case as they represent many merchants/stores and operate an identity provider  
  * goto: Outlined Chrome's process: intent to prototype (already done), dev trials, origin trials, and intent to ship  
  * Joel: Asked about the availability of flags in Canary for prototyping  
  * goto: Confirmed flags are available in Chrome Canaries now and offered to provide documentation  
  * Gorman: Noted in chat that Okta might also be interested in delegation-oriented FedCM

### **Breaking Changes Announcement**

Brief mention of upcoming breaking changes to FedCM.

* **Details**  
  * heather: Shared a link to the FedCM newsletter about upcoming breaking changes \- https://groups.google.com/a/chromium.org/g/blink-dev/c/\_5P00uaafKM  
  * Christian: Confirmed these changes had been previously discussed in the working group  
  * Christian: Mentioned they're reaching out directly to affected IDPs

### **Same-site Legacy Cookies**

Update on the implementation of same-site legacy cookies.

* **Details**  
  * Christian: Announced that same-site legacy cookies are now implemented behind a flag in Chrome  
  * Christian: Requested that interested parties try it out and provide feedback  
  * heather: Shared the GitHub issue link (\#587)

## **Action items**

* **goto**  
  * Send instructions to Joel about how to test delegation-oriented FedCM in Chrome Canaries  
* **Joel/Shopify**  
  * Test delegation-oriented FedCM prototype in Chrome Canaries when documentation is available  
* **Gorman/Okta**  
  * Look into delegation-oriented FedCM and discuss internally at Okta  
* **Interested parties**  
  * Test same-site legacy cookies implementation behind flag in Chrome and provide feedback (GitHub issue 587\)  
* **heather**  
  * Set up new calendar entry for 2026 meetings  
  * Cancel calls on December 23rd and December 30th

## AOB

* [https://groups.google.com/g/fedcm-developer-newsletter/c/B1uzU6MzrYY](https://groups.google.com/g/fedcm-developer-newsletter/c/B1uzU6MzrYY) 

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Erica Kovac (Google Chrome)  
* Joel Antoci (Shopify)  
* Christian Biesinger (Google Chrome)  
* Wendy Seltzer (co-chair)  
* Sam Goto (Google Chrome)  
* Nicolás Peña (Google Chrome)

# Regrets

* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/)) (double booked with [Authentic Web Workshop](https://www.w3.org/events/meetings/f10ec76d-5894-49d0-892c-4cb6f8036a64/) for [Credible Web Community Group](https://www.w3.org/events/meetings/f10ec76d-5894-49d0-892c-4cb6f8036a64/))  
* 

