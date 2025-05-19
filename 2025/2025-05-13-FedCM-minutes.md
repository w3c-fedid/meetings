# FedID WG/CG Telecon, 2025-05-13

* Moderators: Heather Flanagan

* Scribe: Benjamin VanderSloot

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (10 minutes)  
  * IdP/RP implementations  
    *   
* FedCM issues  
  * [Decide on a format for phone numbers \#722](https://github.com/w3c-fedid/FedCM/issues/722)  
* FedCM IdP Registration   
  * [Allow IdP registration and RPs to match on a "type" \#1](https://github.com/w3c-fedid/idp-registration/issues/1)  
  * [Users can't use IdPs outside of the ones enumerated by RPs \#2](https://github.com/w3c-fedid/idp-registration/issues/2)  
  * [Make it easier to deploy this at the eTLD+1 for registered IdPs \#10](https://github.com/w3c-fedid/idp-registration/issues/10)  
* Email Verification (see [https://github.com/dickhardt/verified-email-autocomplete](https://github.com/dickhardt/verified-email-autocomplete))  
* Any Other Business (AOB)

# 

# Notes

### Administrivia

* Heather: Reminders given

### Ecosystem Updates 

* Heather: Updates? Hearing none. Expecting one later this month from Achim’s colleagues.

### 

### FedCM issues

* [Decide on a format for phone numbers \#722](https://github.com/w3c-fedid/FedCM/issues/722)  
  * Christian: This should have been de-selected. I should draft spec text to our consensus from last time.

### 

### FedCM IdP Registration 

* [Allow IdP registration and RPs to match on a "type" \#1](https://github.com/w3c-fedid/idp-registration/issues/1)  
  * Heather: Aaron is not here. Are there updates from Sam?  
  * Sam: No, but the github issue description and implementation may match and seem sufficient. Hesitant because of the granularity of type and registry.  
  * Ben: I think this has had some early adoption (testing in Canary). Next step is getting spec tests and a second implementation. This does have a lot of demand so we probably should bring it into core.  
  * Sam: Happy to start spec text if that is a next step.  
  * Ben: Where does issue 2 then fall?  
  * Nicolas: That may be an artifact of moving issues. (Resolves it.) Are we okay with a single type when the RP is requesting? That makes it hard when the other top level parameters don’t match. Also the naming of type needs bikeshedding.  
  * Heather: Clarify the implications.  
  * Nicolas: Allowing one type vs multiple on request isn’t hard technically, but is   
  * Sam: Start as specific as possible, but leave room for expansion. Type at IDP request config rather than a layer above is a little weird. If it is at the \`IdentityProviderRequest\` level, that would be better. I’ll follow up on the issue.  
  * Phil: Does the IdP communicate to the RP what type was chosen?  
  * Sam: It could easily.  
  * George: An IdP could support a couple of types and an RP could support a few types. One seems too restrictive.  
  * Sam: Good point. Cardinality at RP, IdP, and IdP registration time.  
  * Nicolas: What if the intersection is multiple types? Then we need to report back multiple types. Arrays everywhere.  
  * Ben: Question to Sam: at what level should the type parameter exist? Why put it a level higher than inside a request of this type? Let’s discuss it in the issue. Will also open an issue to bikeshed the name.  
  * Sam: Agree; let’s take this offline and discuss options. String or registry?  
  * Ben: This should be an open string; there shouldn’t be structure there. Maybe suggested values: “work”, “indieauth”, …  
  * Elf: Use a URL.  
  * Tim: A few in the spec as examples, but not an exhaustive list.  
  * Ben: \+1  
  * Sam: Should we enforce URN?  
  * Tim: DC API had some guidance around what characters not to include in the string.  
  * Sam: ???  
  * Heather: Registries are a lot of work. Not absolutely necessary, so let’s not.  
  * Mike: W3C registries \=/= IETF registries. Not easy in W3C. If we really want a registry, use an IETF one, though it is work to spin up.  
  * Tim: URN vs URL, let’s be clear on the difference.  
  * Ted: Briefly. W3C registries are relatively new. Let’s be clear on where they are good and bad. The WG that defines a registry also defines who manages it; that can be the WG itself, a CG, the W3C Team (subject to negotiation with them), or otherwise.  
  * Ben: Agree we shouldn’t do URL but hesitant about URN (mostly because not familiar with their properties when it comes to arbitrary strings).  
  * Sam: How do URNs work?  
  * Tim: Can be formally registered, or …  
  * Sam: DNS was the win I thought.  
  * Tim: No.  
  * Christian: XML namespaces are URLs\!  
  * Ben: If it is not a formally managed thing, can URNs exist to provide a shape/form that mostly works?  
  * elf: What is the problem with URNs?  
  * Tim: URLs must be parsable as URLs. How do you do a consortium for the fediverse? Force a non-entity into registering a domain?  
* [Users can't use IdPs outside of the ones enumerated by RPs \#2](https://github.com/w3c-fedid/idp-registration/issues/2)  
  * Covered by the above.  
* [Make it easier to deploy this at the eTLD+1 for registered IdPs \#10](https://github.com/w3c-fedid/idp-registration/issues/10)  
  * Ben: I want to move the needle on the IdP registration API. This was the third of the issues tied to open concerns. We discussed this at the April 11 meeting and having DNS as the reasonable alternative.  
  * Heather: Was there anything unresolved?  
  * Nicolas: We have two options according to that issue. DNS or skip \`.well-known\` check for registered IdPs. We were leaning toward skipping the \`.well-known\` check. We would have to skip client metadata because of privacy leaks. Type checks would also need to be performed before any fetch. We should validate the FedCM IdP on registration.  
  * Phil: \+1 validation on registration  
  * elf: Do we change the prompting consideration based on this?  
  * Nicolas: It is somewhat independent. The prompt is for abuse prevention in Google’s view.  
  * Sam: It would be wonderful if we could just elide the \`.well-known\` check.  
  * Ben: I believe there was an issue where if you are in the first instance that is using the login URL, it will work if you do not have the DNS solution. So we need at least the DNS solution.  
  * Mike: FWIW, \`.well-known\` was invented because custom data in DNS is harder. I understand that enterprises make \`.well-known\` harder, but DNS is hard with most hosting providers.  
  * Tim: Some things are just hard. Is it that bad?  
  * George: AOL openids were either [aim.com](http://aim.com) or [aol.com](http://aol.com) . Had to use weird netscalar config tricks to make it work. Redirects helped.  
  * Heather: Consensus would be nice to have.  
  * Ben: I will take the action item to investigate the use of redirects for \`.well-known\` files

## 

## Email Verification

* [https://github.com/dickhardt/verified-email-autocomplete](https://github.com/dickhardt/verified-email-autocomplete)  
  * Bumped to next week.

## Any Other Business (AOB)

	

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Phil Smart (Shibboleth/Jisc)  
* Chris Needham (BBC)  
* Brian Daugherty (Google Identity)  
* [elf Pavlik](https://elf-pavlik.hackers4peace.net) (independent, Solid CG)  
* Frank Somich (Google Chrome)  
* George Fletcher (Practical Identity LLC)  
* Zachary Tan (Google Chrome)  
* Yi Gu (Google Chrome)  
* Mike Jones (Self-Issued Consulting)  
* Erica Kovac (Google Chrome)  
* Christian Biesinger (Google Chrome)  
* Chris Fredrickson (Google Chrome)  
* [Theo](https://github.com/thhck) ( liquid.surf \- Solid CG )  
* Parth Bhatt (Independent)    
* Bjorn Hjelm (Yubico)  
* Tim Cappalli (Okta)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* Alan Buxey (MyUNiDAYS Ltd.)   
* Benjamin VanderSloot (Mozilla)

