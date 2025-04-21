# FedID WG Telecon \- DC API Series A, 2025-04-21

* Moderators: Heather Flanagan

* Scribe: Helen Qin

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (10 minutes)  
* DC API  
  * [Define registry inclusion rules \#157](https://github.com/w3c-fedid/digital-credentials/pull/157/)  
    * OK to have an empty registry for FPWD?  
  * No remaining items blocking FPWD?  
* Any Other Business (AOB)

# Notes

### Ecosystem Updates (10 minutes)

* DCP OpenID4VP final call last Friday. public review for final; focus on issuance next.  
* Interop event on May 5th. Participants include many RPs and wallets.   
  * Joseph: in person DCP meeting also planned for the same week  
  * Signup links here: [https://lists.openid.net/pipermail/openid-specs-digital-credentials-protocols/Week-of-Mon-20250414/000739.html](https://lists.openid.net/pipermail/openid-specs-digital-credentials-protocols/Week-of-Mon-20250414/000739.html)  
  *   
* Matt: Do we have an “awesome-digital-credential” list anywhere? Is/was a popular way to find projects in a certain slice of tech as a launch point for people who wanted to find libraries, etc., to work with  
  * Tim: create one in the digitalcredentials.dev org.

### DC API

### [Define registry inclusion rules \#157](https://github.com/w3c-fedid/digital-credentials/pull/157/) (OK to have an empty registry for FPWD?)

* Heather: Is it ok to have an empty registry list in the first version of the working draft?  
* Tim: Need to work face to face with Marcos.  
* Lee: if registry is optional, if the browsers can implement protocols outside of the registry or don’t have to implement all protocols in the registry, then it doesn’t matter that much to have an empty registry.  
* Heather: Registry is a shortcut to understand how things are structured?  
* Lee: The purpose of the registry has loosened over time. Now it serves as guidance and a good way for developers to know what is recommended. An ecosystem thing rather than something that can be enforced.  
* Brian: Is the registry going to be a separate document or was it really intended to be part of the specification?  
* Tim: In the spec for now, and move outside as part of the process.  
* Sam: Isn't the registry intended to influence what gets returned in the supported-protocol api? Then it isn’t just an ecosystem thing.  
* Lee: Not necessarily, if the browsers aren’t always going to implement everything or only things inside of the registry.  
* Sam: Used by the verifier to test whether the request will go through.  
* Lee: But can test, e.g., annex-c, and that won’t be in the registry.  
* Sam: So the way each browser returns the protocols is different from the registry. Makes sense. The former is a superset.  
* Brian: Not a superset. Could just be a list.  
* Christian: Hopefully it’s a somewhat complete list.  
* Lee: The proposal now is \`isProtocolSupported(string)-\>boolean\`. The registry is not authoritative in terms of what can be put in that call.  
* Sam: It could be used to reserve and centralize keys.  
* Lee: Could be, but still possible for collision since an implemented protocol could be outside of the registry. To answer the original question, it should be OK to have an empty list in the first working draft.  
* Sam: Agree, an empty list is OK.  
* Tim: A user agent can choose to only return true for things in the registry list. Some have chosen to push that concern to the wallets.  
* Heather: No remaining items blocking FPWD?  
* Tim: PRs need to be merged.   
* Lee: we did agree issuance is blocking  
* Tim: Yes — there’s no open discussion. Just needs to be merged.  
* Lee: When will the WD get published?  
* Heather: I hope to start the process to get this published on May 1st.  
* Wendy: Record WG decision to move to the first public working draft. Then editorial steps to get the draft published. Deploy the tooling to auto publish editor drafts.   
* Simone Onofri: After the CFC, one week, then the next Tue/Wed. \+1 for autopublish.  
* Conclusion: End of May seems reasonable.  
* Wendy: Do we want to auto-publish in TR, post-FPWD?  
* Heather: Hearing no objection.

### Any Other Business (AOB)

Tim: \#221 [https://github.com/w3c-fedid/digital-credentials/pull/221](https://github.com/w3c-fedid/digital-credentials/pull/221). Shouldn’t be controversial. Don’t need to block the WD but it would be nice to have it done.  
Matt: \+1 would be nice to have it added.  
Sam: Heard from Marcos that Safari will only support certain credential types (e.g., mobile driver's license), so it would drop not at the protocol level but at the credential-type level.  
Lee: That's an implementation choice, and we shouldn’t go to that level of details at the spec level for scalability.

Matt: Do issues get added to the agenda? I have added some issues.   
Heather: Use the agenda tag.  
Tim: You can’t add labels if you are not in the org. Should be added as a contributor.

Heather: Sending the automated scribing tool to the mailing list to get permission to use. Will also check in before the calls.  
Wendy: Heard such a tool would prevent some members from participating. Welcome concern and would get group consensus before proceeding  
Lee: Do we have to publish the raw transcripts? Maybe just the summaries? Then we won’t have to worry about the raw transcripts.  
Tim: Looking at usage by the CCG, the tool seems to be working well.

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting)  
* Matthew Miller (Cisco)  
* Michael Jones  
* Wendy Seltzer  
* Joseph Heenan (Authlete / OIDF)  
* Helen Qin (Google Android)  
* Lee Campbell (Google Android)  
* Tim Cappalli (Okta)  
* [Ted Thibodeau](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* Simone Onofri (W3C)  
* Christian Bormann  
* Brian Campbell  
* Monty Wiseman  
* Sam Goto