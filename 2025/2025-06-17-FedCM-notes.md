# FedID WG/CG Telecon, 2025-06-17

* Moderators: Heather Flanagan

* Scribe: Wendy, Phil

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (5 minutes)  
* FedCM Issues  
  * [Tracking through IDP with individualized account and client\_metadata endpoints \#700](https://github.com/w3c-fedid/FedCM/pull/700)  
  * [Horizontal Review preparation \#652](https://github.com/w3c-fedid/FedCM/pull/652)  
* FedCM PRs  
  * [Specify "Use another account" \#678](https://github.com/w3c-fedid/FedCM/pull/678)  
  * [Make connected accounts set a quadruple \#732](https://github.com/w3c-fedid/FedCM/pull/732)  
  * [Fix spec bugs reported by togamid \#737](https://github.com/w3c-fedid/FedCM/pull/737) (see Issue 734 and 700\)  
* Any Other Business (AOB)

# 

# Notes

## Administrivia

* Heather: Welcome, reminders

## Ecosystem Updates 

* Phil: Chained authentication, I’ve been going through that flow and updating the ticket (after a prompt from Ben). Not for today, but I invite folks to take a look for a future discussion. 

## FedCM Issues / PRs

### [Specify "Use another account" \#678](https://github.com/w3c-fedid/FedCM/pull/678)

* Christian: I think this one is ready to land. Ben, did you want to look again?  
* Ben: Will give it one more proof read. Think it’s directionally right. 

### [Tracking through IDP with individualized account and client\_metadata endpoints \#700](https://github.com/w3c-fedid/FedCM/pull/700) and PR [Fix spec bugs reported by togamid \#737](https://github.com/w3c-fedid/FedCM/pull/737) (see Issue 700, 734\)

* Nicolas: Issue was discussed within the team. Moving the accounts endpoint to the \`.well-known\` file is probably the best approach. It is backwards incompatible, however. Move the \`login\_url\` to the \`.well-known\` as well  
* Christian: it is already in \`.well-known\`.   
* Nicolas: It is not enforced to be in the \`.well-known\`. This addresses the privacy attack which uses randomisation to determine who the user is (know what IdPs they have used before?) before consent. Or, remove the \`client\_metadata\` fetch, but that has some utility. Could be used to block which (IdP or RP, not clear, sorry) to show in the UI.   
* Ben: Question, I thought you wanted to allow multiple different accounts endpoints per Identity provider. So make sure you still support this.  
* Nicolas: Ideally, multiple configs could allow this, but we are still at 1\. Account labels let you show some but not all of the IdP's accounts. Which is sufficient for the use cases so far, so we’ve not needed to increase this beyond 1\. Could allow an array for the accounts endpoint to allow for this in the future.   
* Christian: Mostly moved away from multiple accounts endpoints.  
* Alex (from chat): We want different account endpoints for subdomains, e.g., dev/prod  
* Yi: Need for privacy metadata endpoint  
* Ben: Not sure if it is needed directly in the JS call. There is a privacy risk, so Firefox did not implement that  
* Yi: For further chat  
* Alex: We have different envs, with different user pools, so we want to not just test everything on a prod environment. Because we only have one TLD+1 and we want different envs under that, like dev, staging, etc., so need different endpoints  
* Christian: Turn off well-known enforcement for testing  
* Nicolas: Can you use labels for this?  
* Alex: Completely different backend, so probably not  
* Christian: Are they under the same site?  
* Alex: Fully separated IdPs, RP is on a different domain. Config URLs is an array, but it only supports 1\. But we can work around these changes if they are a privacy concern.  
* Nicolas: Adding more adds more entropy for tracking. Hopefully using chrome flags is OK for testing (turn off well-known enforcement)  
* Simone: (iframes) If we want to violate the contextual integrity by spec, we need to justify the use case for that  
* Yi: Is this FedCM specific or any iframe features  
* Simone: Need to justify these use cases, so need to discuss the tradeoffs  
* Yi: This is just a string which allows the iframe to use FedCM. So it is off by default unless the embedder allows it. Is a permission policy.  
* Heather: Nicolas do you have what you need for this.   
* Nicolas: Also like to discuss 737 ([https://github.com/w3c-fedid/FedCM/pull/737](https://github.com/w3c-fedid/FedCM/pull/737)) and [https://github.com/w3c-fedid/FedCM/pull/734](https://github.com/w3c-fedid/FedCM/pull/734)). Key thing, this PR fixes a few spec issues, in particular there is also one change to mediation ‘silent’, on failure we now delay the rejection. Currently we do not, but potential privacy issues where the RP may be able to infer information they should not if we reject immediately. So rejection for mediation silent is delay (as with other cases). Also, it is weird that ‘silent’ is not ‘silent’ when you have a mismatch; check if you have connected accounts and login status logged-in then you fetch, but that could return no accounts, so current mitigation is we need to show the mismatch dialog and allow the user to login. Is it OK for it to be silent if the RP already has the connected account, so if the IdP already has a connected account with the RP, there is not huge privacy gain from showing the mismatched dialog (they are already connected)?   
* Ben: I think ‘silent’ should be silent. And if you need to show a UI to preserve privacy, you have gone wrong (operations up to that point should fail beforehand).   
* Nicolas: Yeah, we check everything before we fetch the account. Is there at least one connected account, and is login status not logged out. Which is good, but maybe the mismatch is incorrect in that case, it should be silent. But IdP is already connected, so maybe not an issue  
* Ben: Seems right to me.  
* Nicolas: OK, will update the PR with that.  
* Heather: ‘silent’ should mean silent from a language perspective. Silent \= do not show UI.  
* Ben: and for consistency with CredMan  
* Nicolas: Another set of eyes on the spec will be good.

### [Make connected accounts set a quadruple \#732](https://github.com/w3c-fedid/FedCM/pull/732)

* Nicolas: Privacy issue, connected accounts need to be described also by the embedder, e.g., an iframe. Disconnect could be an issue, as always called by the top level (although that may be OK). Keyed on iframe and top-level. IdPs do not have double keying.  IdP would expect any connected account where the caller is the same, would be removed, even if different top-level.  
* Phil: We already re-key on the RP, IDP-RP. Typically, we don’t iframe  
* Ben: Probably best to treat the top-level and frame as a pair, and clear on disconnect. Disclosure, Firefox doesn’t support any iframing.   
* Nicolas: I’ll keep the spec that way and listen for concerns  
* Kevin (from chat): Why should this work differently from storage? I’d expect it to be scoped parent and child, which is how localStorage and indexDB work. Otherwise you’re allowing tracking across domains, which I think is not what we want.  
* Nicolas: We’re debating how disconnect should work. I will keep it double-keyed. Not sure it makes sense for an IDP  
* Ben: We can ask, how would you expect an IDP to be logged out on this RP if it were also using it at the top level?  
* Nicolas: I think from the top level, not. If both A and C embed B, and A-B calls disconnect, what should happen to C-B? Or B without being embedded?  
* Phil: Should that be a question for the IDP?  
* Nicolas: Yes, we send a question to the IDP

### [Horizontal Review preparation \#652](https://github.com/w3c-fedid/FedCM/pull/652)

* Heather: Wendy, horizontal review.  
* Wendy: Thanks to Kevin for work on accessibility self-review. Let him present the work he has done on issue 741 ([https://github.com/w3c-fedid/FedCM/issues/741](https://github.com/w3c-fedid/FedCM/issues/741)).  
* Kevin: Some comments for implementers, how can we make the notes and spec better.   
  * Biggest thing, in the \`.well-known\` file, in the linkages, we need to think about how IdPs talk about themselves. I want to talk about it, and follow up in the issue.  
  * For example, how much control does the IdP have over naming and working with screen readers?  
  *  It follows the WebAuthn implementation closely, (PS, not sure this part was relevant)  
  * WCAG requirements should be considered. What are the relationships? Making sure the context of the IdP and RP connections is clear, the context needs to be consistently displayed at all levels.   
  * Some things do not apply, reset cooldown felt more appropriate for automation?   
  * Icon and branding is discussed, make sure all of that is clear to the user.  
  * Will update the document when I get my access back.  
* Wendy: any comments from others on the self-review. Is a great place to start.   
* Heather: When the PRs are created, tag them with the accessibility tag.   
* Christian: The more an IdP can control the UI, the more the likelihood you have for nefarious IdPs to display bad information. So that is mostly restricted.  
* Kevin: I understand. The biggest concern is making sure that a screen reader has access to context and content. You are logging in to … etc.  
* Christian: Important that screen readers are allowed  
* Ben: At least add a note it should be accessible to screen readers etc.  
* Heather: Anything else on that? None. Wendy, what reviews are we needing?  
* Wendy: have we requested a TAG review recently?   
* Sam: We have over the years. We have also TAG reviews for things we have not launched yet.  
* Wendy: Let’s gather reference to those existing reviews in a tracking issue

## 

## 

## Any Other Business (AOB)

* [https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-(Consensus-Blockers-for-CR)](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-\(Consensus-Blockers-for-CR\))  
  * Things that need discussion/eyeballs.

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting, co-chair)  
* Wendy Seltzer (co-chair)  
* [TallTed // Ted Thibodeau Jr](https://github.com/TallTed) (he/him) ([OpenLink Software](https://openlinksw.com/))   
* Nicolás Peña Moreno (Google Chrome)  
* Christian Biesinger (Google Chrome)  
* Phil Smart (Shibboleth/Jisc)  
* Alex Miller (Strawberry)   
* Alex Chalmers (self)   
* Parth Bhatt (Independent)  
* Chris Needham (BBC)  
* Yi Gu (Google Chrome)  
* Brian Daugherty (Google Identity)  
* Benjamin VanderSloot (Mozilla)  
* Zachary Tan (Google Chrome)  
* Mike Jones (Self-Issued Consulting)  
* Alan Buxey (MyUNiDAYS Ltd.)  
* Kevin Druff (Capital One)  
* Bjorn Hjelm (Yubico)

# Regrets

*  