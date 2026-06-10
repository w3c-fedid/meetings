# FedID WG Telecon — DC API Series B, 2026-06-10

* Moderators: Heather Flanagan

* Scribe: Matt Miller

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/participants/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/20240318/)  
* Ecosystem Updates (10 minutes)  
* DC API Issues & PRs (45 minutes)  
  * [Spec doesn’t enforce encrypted response requirement \#519](https://github.com/w3c-fedid/digital-credentials/issues/519) & [Specify protocol validation \+ enforce encryption \#520](https://github.com/w3c-fedid/digital-credentials/pull/520)  
  * Issue Triage (starting with issue 263, oldest to newest)  
* Any Other Business (AOB)

# Notes 

## Administrivia

* 

## Ecosystem Updates

* Heather: Credential harmonization will occur in OIDF. Last year someone made the observation that OID4VP and ISO families of protocols do very similar things. So of course we decided to create a third protocol to unify them. Last several months have involved discussions of where to host this work. OIDF, ISO, and FIDO Alliance were three main contenders.   
  * WG link: [https://openid.net/wg/digital-credentials-harmonized-presentation-working-group/](https://openid.net/wg/digital-credentials-harmonized-presentation-working-group/)  
* Heather: No chairs yet, still to be decided.  
* Marcos: Confused about a third format. WebKit only supports ISO. Now there’s regulatory pressure to do OID4VP. What does this mean for a third format?  
* Heather: The official answer is, the intention is that the new thing replaces OID4VP and ISO 18013 specs.  
* Brian: That is the intent of some people involved.  
* Heather: The snarky answer is, “ha ha ha ha ha now we have three.”  
* Marcos: Why don’t we put an end to that?  
* Tim: Because there was industry consensus that this was needed.  
* Heather: The good news is that this is not our problem. I would not let that work come into our group.  
* Wendy: A reminder not to imply motives to members of the WG.  
* Tim: We are here because there was consensus including with the company that … and harmonization between in-person and online presentation  
* Matt: Was it not the case that OID4VP didn’t do in-person while ISO did? Maybe I’m missing something.  
* Tim: OID4VP already works in-person.  
* Brian: We don’t have harmonization at all. There is a broken, fragmented process that led to the creation of a WG without a clear path forward. Remote vs in-person stuff, the in-person stuff \[in OID4VP\] worked fine. We’re going to end up with six protocols.   
* Nick: I’m seeing a joint partner SDO, is there something I can read to learn more?  
* Heather: It’s an OIDF WG, the link above has all the current info as of today.  
* Bjorn: Yes, it’s an OIDF WG. The intent is to have participation across DCP WG and ISO WG10.

## 

## DC API PRs and Issues

### [Spec doesn’t enforce encrypted response requirement issue\#519](https://github.com/w3c-fedid/digital-credentials/issues/519) & [Specify protocol validation \+ enforce encryption pr\#520](https://github.com/w3c-fedid/digital-credentials/pull/520)

* Heather: Before we decide as a group whether encryption is required or not, there were concerns in previous calls about \[a variety of issues I couldn’t type fast enough.\] Is DC API required?  
* Heather: Is anything new to discuss? Should we take it to an informal vote?   
* Tim: My concern remains: we came to consensus on many things that this would now change. We also shouldn’t make non-normative sections normative  
* Marcos: As new implementation experience is gained, consensus changes. I looked at the privacy considerations in the context of OpenID and found some new concerns, as described in the issue.   
* Tim: There are no design requirements around that. Can you share insights from experimentation?   
* Marcos: Some of our work is open source and some is closed source.  
* Heather: When we first came to work on this, we were relying on Google’s experience with OpenID specs. Now Apple is working with those specs too.  
* Marcos: I was looking as editor of the spec trying to address outstanding privacy & security issues. Saw a hole around this issue in privacy and security considerations.  
* Tim: Point of clarification: is this implementation or editorial experience?  
* Marcos: Mostly the editor role, but also I did some implementation work earlier and then reverted it.  
* Brian: There are plenty of others who have implemented.  
* Nick: Seems this is more on the security side, but the privacy considerations section, originally non-normative, was trying to summarize other parts of the spec.  
* Tim: I’m pushing back on design goals. Responses were assumed to be encrypted but not enforced, as browsers don't need to inspect. If we do this, we’re essentially telling users who don’t want to encrypt to go to custom schemes.   
* Marcos: We (Apple) feel pretty strongly that this is a requirement  
* Heather: I haven't heard any new information today. The calls seem split. Chairs will put out a straw poll, send it to the list. Encourage more voices to weigh in with opinions.   
* Matt: Checking my understanding, the decision point is whether or not to mandate response encryption. Proponents are saying it improves security. The other side is that it frees up the browser from having to implement request introspection.   
* Tim: Today, the browser can do what it wants. Now we’d be saying you must. OpenID 1.0 is one protocol that has multiple operating modes. The browser would be supporting only some. We’ve already said it's the wallet's responsibility to implement the protocol.   
* Heather: Expect a straw poll, 2 week response time. 

### [Issue Triage](https://github.com/w3c-fedid/digital-credentials/issues/) (starting with [issue 263](https://github.com/w3c-fedid/digital-credentials/issues/263), oldest to newest)

* Heather: Let’s do some issue triage\! We really need to respond to the issues about privacy considerations. 

#### [263](https://github.com/w3c-fedid/digital-credentials/issues/263). [Clarify the relationship and trust model of multiple user agents](https://github.com/w3c-fedid/digital-credentials/issues/263)

* Tim: We had that. I was asked to take it out.   
* Marcos: The TAG has a new user agent document, can we leverage that?   
* Heather: [https://w3ctag.github.io/user-agents/](https://w3ctag.github.io/user-agents/)  
* Marcos: It’s supposed to be generic  
* Heather: Tim, if you bring your text to me, I can take that to TAG.  
* Tim: This issue: [https://github.com/w3c-fedid/digital-credentials/issues/190](https://github.com/w3c-fedid/digital-credentials/issues/190)   
* Nick: I’m not sure the definition of user agent solves the question.   
* Tim: You’re still operating on the assumption that the UAs do the right thing.   
* Heather: This one needs to stay open

#### [265](https://github.com/w3c-fedid/digital-credentials/issues/265) [voluntary usage and protections against coercion](https://github.com/w3c-fedid/digital-credentials/issues/265) 

* Tim: I think the spec naturally mitigates against this. The API doesn’t provide a signal whether the credential is available. We explicitly decided not to. (Even though developers would prefer to know.)  
* Nick: I think the issue was referring to risks, that indicators of availability make it possible for sites to condition access.   
* Tim: There's no disclosure. The API gives no insight into whether a call will be successful.  
* Matt: Similar pattern to WebAuthn. Are we protecting against silent discovery?  
* John: Right now, I don’t think it’s in the DC API. it’s up to the protocol.   
* Matt: I forgot that lots of error codes would be transmitted back through the protocol.   
* Tim: By that point, you’ve still taken the user through permission in the browser and consent in the wallet. Lots of steps against passive tracking.   
* Matt: Would it be a problem if a protocol that you could exercise through the API returned a response “no credentials were available”? Is that a problem we need to solve in DC API text?  
* Tim: The nuance is that the browser is not leaking it. There are many steps and lots of friction.  
* Matt: Could a wallet make a quick no-response, as a problem?

#### [266](https://github.com/w3c-fedid/digital-credentials/issues/266) [registration of and commitment to a particular use case and purpose](https://github.com/w3c-fedid/digital-credentials/issues/266)

* Tim: this is largely being done in other layers, organizations.   
* Nick: we saw some demos suggesting it would be more effective if presented at the time of permission request, accountability through well-known URL or other mechanism.   
* Marcos: Can we shift gears on privacy consideration issues, about 12 of them? Is there a more effective way to review them?   
* Heather: Suggestions welcome\!  
* Tim: Most of them are back to division of responsibility. We either need to review them separately or try to reach consensus on roles and responsibilities.   
* Nick: I don’t think it’s effective to say “we hope others will address” when we don’t think they will.  
* Heather: Should we have a privacy-dedicated meeting looking at the collection of issues? I’ll try to get a conversation scheduled.

## AOB

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* Matthew Miller (Cisco)

* George Fletcher (Practical Identity LLC)

* Wendy Seltzer (co-chair)

* Tim Cappalli (Okta)

* Marcos Caceres (Apple)

* Brian Campbell (Ping)

* Nick Doty (CDT)

* Bjorn Hjelm

* John Schanck

* Simone Onofri

* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* 