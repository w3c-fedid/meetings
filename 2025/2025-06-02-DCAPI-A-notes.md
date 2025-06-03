# FedID WG Telecon — DC API Series B, 2025-06-02

* Moderators: Wendy Seltzer

* Scribe: Mohamed Yosef

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * Upcoming meeting schedule  
    * summer meetings  
    * meeting during IETF 123  
* Ecosystem Updates (10 minutes)  
* DC API Issues (30 minutes)  
  * [\[spec\] write privacy considerations \#183](https://github.com/w3c-fedid/digital-credentials/issues/183)  
    * [issues tagged privacy-considerations](https://github.com/w3c-fedid/digital-credentials/issues?q=state%3Aopen%20label%3A%22privacy-considerations%22)  
    * [Privacy Considerations: Add initial Introduction, Spectrum of Privacy sections \#251](https://github.com/w3c-fedid/digital-credentials/pull/251)  
* Any Other Business (AOB)

# Notes

* 

## Administrivia

* Wendy: Reminders, group membership, code of conduct  
* Wendy: Still waiting for the f2f meeting place, otherwise we will host a long hybrid meeting.

## Ecosystem Updates

* Matthew: what are the updates regarding openid4vp  
* Christian: this is in review, public review started 4 weeks ago, should finish by end of June  
* Matthew: based on version 28?  
* Christian: there were minor changes.

# 

DC API Issues (30 minutes)

* Wendy: Still no consensus for FWPD. Johann stepped up to lead issue 183 for the privacy considerations,  \`privacy-considerations\` tag is used to tag relevant issues, encouraging everyone to participate in this asynchronous discussion.  
  * Johann: Aim for an iterative process, landing small PRs and iterating. There is an almost-ready additional PR for what the permission prompt should contain.  
  * Johann: We should also make progress on [issue 252](https://github.com/w3c-fedid/digital-credentials/issues/252) over time.  
  * [\[spec\] write privacy considerations \#183](https://github.com/w3c-fedid/digital-credentials/issues/183)  
    * [issues tagged privacy-considerations](https://github.com/w3c-fedid/digital-credentials/issues?q=state%3Aopen%20label%3A%22privacy-considerations%22)  
    * [Privacy Considerations: Add initial Introduction, Spectrum of Privacy sections \#251](https://github.com/w3c-fedid/digital-credentials/pull/251)  
      * Wendy: Would be great if this gets reviewed by folks.  
      * Nick: Thanks Johann for starting the work, supportive of the iterative approach. Why are some sections removed as out of scope?  
      * Johann: Happy to discuss what is in scope, and talk about where we should put the energy.  
      * Nick: Discussion about the permission prompt is useful.   
      * Johann: I am trying to moderate what the browser as a user agent should show in the permission dialog to make sure the users are safe, and that it is used for a legit purpose.  
      * Wendy: We have the tension between what can be done using this API and the interaction with the rest of the platform. Please create issues and add the \`privacy-considerations\`  tag to help the chairs. Hoping to reach consensus on the overall shape of the API.  
      * Matthew: There is no precedence for dictating the user agent about how to display the permission prompt (e.g., WebAuthN didn’t define that)  
      * Johann: We should have at least a discussion about it; especially with government-issued credentials, the bar is different.  
      * Matthew: I agree this is a good forum for those discussions, but how much time should we spend on this? Would this stall things?  
      * Johann: Pushed back on building a legal consent framework, but we should balance that with what the user-agent can also display to be rooted in the real world.  
      * Simone: I agree with Mathew that we should agree what should be displayed in the browser's consent dialog and what should be delegated to the wallets.   
      * Nick: Good question, Matthew. I am not interested in a model where we dictate to the user-agent what it should display. It’s not useful to ask the browser to make a scarier prompt. But to make sure the correct information is communicated to the user (right party), and if some capabilities can be delegated to the protocol level, we need that information to decide which protocol can support such a requirement.  
      * Ben: Another direction is looking also at, for example, the EUDI enumerated list of allowed RPs and consuming that information. I agree that dictating UI is hard given how flexible the API is (e.g., government ID vs. concert tickets).  
      * Christian: I agree, dictating the UI won’t work. EUDI plans to have a registration certificate. (Every entity interacting with the wallet will be registered in the ecosystem.) In addition to the purpose of using the data (access certificate). Those mechanisms should work on online and offline cases and hence are hard to build inside the DC API.  
      * Matthew: What next steps are needed before we start updating the DC API?  
      * Johann: Should consider adding more fields in the API to help disclose the privacy properties. It comes down to the trust angle. Does the user trust the wallet? Does the user agent trust the wallet to do the right thing? [https://github.com/w3c-fedid/digital-credentials/issues/247](https://github.com/w3c-fedid/digital-credentials/issues/247) …  
      * Lee: I agree, we shouldn’t hand off to the wallet without anything in between. Even if it is just a wallet selection. But we cannot go crazy in this screen. We cannot understand all those pieces of the system,  (e.g., if this is an EUDI registered request). Wallet can already handle that\!  
      * Johann: I want to leave the door open to add more points to the privacy consideration that the user agent should think about. Can we add some normative text that such trust frameworks should be factored in (e.g., EUDI trust framework)? But shouldn’t block on that\!  
      * Nick: I don’t see how the wallet is in a better position to understand everything about the verifiers. EU regulations or the relationship between the verifier and the wallet can play a role, but in general, the wallet is poorly positioned to do that. For example, California DMV  is not qualified to do that, they don't know most of the verifiers, and they don’t know what has been presented on the web.  
      * Christian: The assumption is, there will be different wallet ecosystems, and hence we should have freedom on the wallet-side. However, I see the browser is well positioned to know how the interaction started,  
      * Ben: Agree on the California DMV concerns, and it is an interesting question whether the browser is the only user agent that can do something meaningful..  
      * Matthew: QR-Code based presentation takes the browser out of the way. Would then consider that the DC API isn’t worse, but raises the security bar. DC API is better than QR-Code approaches even in its current form.  
      * Johann: Yes, we cannot take forever on making this perfect, because it will be hard to recover if the ecosystem develops another way. But we also should spend the time to discuss if we cannot improve privacy.  
      * Wendy: Heterogeneous environment, of which this API is just one piece. If we don’t get this API out, we are aware of the alternatives. We have a threat model that describes the whole ecosystem and the threats associated with the API. Not trying to solve everything, but giving opportunities for people to resolve their privacy concerns. Thank you to those participating in the dialog.  
      * Simone: We are working on the security consideration section in Security Interest GRoup that will be on github. DC API in its current state seems better than alternatives.  
      * Nick: One question: Is there more documentation in the ARF or somewhere else about the access certifications? I want to know about that urgently.  
        One action item: We should make sure we have issues open that capture all those discussion points.  
      * Wendy: We cannot resolve everything about privacy/identity in this API, and there are limitations to what we can do in the spec (e.g., we don’t specify browser UI). Encourage engagement on [issue 252](https://github.com/w3c-fedid/digital-credentials/issues/252) (label issues coming to conclusion and ready for discussion with \`agenda+\`).

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Wendy Seltzer  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* Mohamed Yosef (Google Chrome)

* Lee Campbell (Google Android)

* Nick Doty (CDT)

* Benjamin VanderSloot (Mozilla)

* Chris Needham (BBC)

* Matthew Miller (Cisco)

* Johann Hofmann (Google Chrome)

* Christian Bormann (SPRIND)

* Rene Leveille (1Password)

* Simone Onofri (W3C)