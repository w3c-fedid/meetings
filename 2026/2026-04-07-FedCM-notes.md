# FedID WG/CG Telecon, 2026-04-07

* Moderators:  Heather

* Scribe: Wendy

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
* Discussion (30 minutes)  
  * [Allow IDPs to delegate well-known file hosting via DNS TXT record \#821](https://github.com/w3c-fedid/FedCM/pull/821)  
* Any Other Business (AOB)

# Notes

## Administrivia

* So noted.

## 

## Ecosystem Updates (10 minutes)

* Emily: Microsoft Identity is starting a prototype for FedCM, expect some feedback in the coming months.

## Discussion (30 minutes)

### [Allow IDPs to delegate well-known file hosting via DNS TXT record \#821](https://github.com/w3c-fedid/FedCM/pull/821)

* Christian: I believe open question whether DNS query should happen in parallel or after well-known?  
* Will: As it stands currently, spec requires hosting .well-known at the apex domain, which has operational challenges. I gave some options in the PR: have DNS contain the config file, point to the config, or have a subdomain. We can have one or more responses, in various combos. We need something from MS perspective.   
* From a latency perspective, most efficient is putting it in DNS, then fetching in parallel with first response winning. I’m open to any of the options .  
* Nicolas: main objective is to get the .well-known out of the top-level of eTLD+1, so use DNS?  
* Will: Use DNS TXT or a subdomain (fixed).  
* Nicolas: How is that easier than root?  
* Will: Subdomain might be easier for implementers who don’t have a lot of ability to customize DNS.  
* Christian: IDPs who delegate the entire thing. You can’t delegate the apex domain to middleware. Others who benefit, big orgs where different teams are responsible for apex domain and for FedCM.   
* Nicolas: We haven’t yet aligned on the solution  
* Heather: The PR isn’t yet proposed for merging, but it’s a way to discuss  
* Will: I’d like the spec authors to pick one of the options. From my perspective, any would do.   
* Nicolas: Where’s the best place to look at the options?  
* Will: [PR \#821](https://github.com/w3c-fedid/FedCM/pull/821).   
* Christian: I’d prefer something more deterministic than whoever happens to respond first. Not depend on latency.   
* Will: If your apex domain is timing out, then it becomes a blocker. I’d prefer parallel and whichever responds first, or prefer new to old. Sam had been unhappy with pessimizing the old.   
* Achim: These delegation patterns are used quite broadly, different failure modes and inconsistencies if two different responses are possible.   
* Wendy: Maybe ask TAG for a review of the .well-known considerations. Also consider security implications of having two potentially inconsistent paths.   
* Nicolas: \+1 to asking TAG, also \+1 to Christian’s concern about being non-deterministic. Can we make it backwards-compatible?   
* Will: It sounds as though this group finds non-deterministic to be a problem, so I’m happy to change the PR  
* Heather: chair-hat-off: if you’re saying two go in parallel, and look at the first response, how is that deterministic?   
* Will: I was assuming browsers already have a timeout. Use that when doing 2 in parallel.   
* Christian: Browsers don’t really have a DNS TXT query. We prototyped something… we should probably specify a timeout. It’s uncommon that things timeout instead of failing  
* Nicolas: We can test today whether the new thing fails with non-existent.   
* Will: DNS records are less likely to hit legacy content, because people don’t yet have the \_ domain.   
* Christian: Chrome would probably implement via a web-based DNS query  
* Wendy: Over at IETF DNSOPs, DNS has its own set of administrative silos and authority challenges.   
* Heather: This set of administrative challenges (ownership of IDP and tech stacks) has been with us from the beginning of FedCM, e.g., universities and federations, big and small organizations.  
* Nicolas: We picked the root because we wanted the uniqueness of the endpoint.   
* Achim: I think we were also talking about privacy issues if not eTLD+1 [https://github.com/w3c-fedid/FedCM/issues/230](https://github.com/w3c-fedid/FedCM/issues/230)   
* Phil: Agree with the overall concept of having a mechanism to support something not just on apex.   
* Aaron: I also think this is needed. I’d be a fan of the option that requires the fewest new obligations on the person who manages the apex domain. Easier to add a DNS record than a web file  
* Will: From that perspective, I think the options are similar. One DNS record, depends which type. Service record or CNAME  
* Heather: I’m going to assign homework: Everyone except WIll, please read the PR and write in your feedback on preferences.   
* Will \[in chat:\] Question for TAG is: What is the pattern (or, is there a pattern) for an item which MUST has a cardinality of 1 on the registrable domain? FedCM requires one endpoint for user+relyingParty privacy. Today, the FedCM spec uses the apex domain, which has operational considerations. We are examining: 1\) using an underscored prefixed DNS name (\_web-identity.\<domain\>) 2\) using a non-underscored prefixed DNS name through HTTP (web-identity.\<domain\>). Does TAG have a preferred pattern for problems like this or have any considerations for choosing between these options?  
* Heather: I will send to TAG, since I’m new there.   
* WIll: I also sent a query to IETF DNSOPs ML as suggested by Emelia. [https://mailarchive.ietf.org/arch/msg/dnsop/aLACo0YpxJezsvlXZipp9aL0mFs/](https://mailarchive.ietf.org/arch/msg/dnsop/aLACo0YpxJezsvlXZipp9aL0mFs/)   
* Bumblefudge: I think Emelia suggested DNS OPS WG at IETF because atproto folks do [something similar](https://atproto.com/specs/handle#dns-txt-method) and are looking at recent draft RFCs in DNS OP WG. (uses TXT record for now)

## AOB

* Heather: Next call is a week before IIW, think about things you’d like to discuss there/then. 

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Wendy Seltzer (co-chair)  
* Achim Schlosser (Bertelsmann)  
* Christian Biesinger (Google Chrome)  
* Aram Zucker-Scharff (The Washington Post)  
* Aaron Parecki (Okta)  
* [bumblefudge.com](http://bumblefudge.com) (learningProof UG)  
* Phil Smart (Shibboleth/Jisc)  
* Yi Gu (Google Chrome)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Nicolás Peña Moreno (Google Chrome)  
* Emily Lauber (Microsoft Identity)  
* Theo \- @thhck \- https://liquid.surf  
* Will Bartlett (Microsoft Identity)  
* Mike jones  
* Nick Steele (OpenAI)  
* Suresh Potti (Microsoft)  
* Michael Animashaun (DSIT)

