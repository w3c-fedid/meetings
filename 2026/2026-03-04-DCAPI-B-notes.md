# FedID WG Telecon — DC API Series B, 2026-03-04

* Moderators: Wendy Seltzer

* Scribe: Wendy

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/participants/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/20240318/)  
  * Warning: DST Clock skew is coming up\! 8-29 March 2026  
* Ecosystem Updates (10 minutes)  
* DC API Issues & PRs (45 minutes)  
  * [Add "Abort the credential request" algorithm \#462](https://github.com/w3c-fedid/digital-credentials/pull/462)  
  * [Define "prepare credential requests" algorithm \#420](https://github.com/w3c-fedid/digital-credentials/pull/420)  
  * [Addressing Request Tampering \#426](https://github.com/w3c-fedid/digital-credentials/pull/426)  
  * [Wallet Selection Binding during Issuance \#382](https://github.com/w3c-fedid/digital-credentials/issues/382)  
  * Privacy status or issues  
* Any Other Business (AOB)


# Notes 

## Administrivia

* Reviewed membership and CoC

## Ecosystem Updates

* Welcome John from Mozilla  
* John: We have a basic API wired up, still have some UX to do; I’ll probably bring some questions to the group regarding transparency. I will have something written soon.   
* Marcos: Feel free to use the *agenda+* label

## 

## DC API PRs and Issues


### [Add "Abort the credential request" algorithm \#462](https://github.com/w3c-fedid/digital-credentials/pull/462)  
  * Marcos: Something triggers aborting a credential request, e.g., an iframe triggers request but context goes away. What should happen? This algo makes the credential sheet go away, and resets the state machine. Presentations will also use it.   
  * Lee: On Android, when you call, and the UI pops up, the browser can’t cancel the UI; only the user can. We don’t like the apps being able to flash a screen and then cancel it. We could have it not be continuous. It’s not just our UI; the wallet controls one too, and you’re limited in your ability to cancel.   
  * Helen: Chrome might be doing something fancy. We don’t usually support the app cancelling once the user has seen something.   
  * Marcos: The underlying mechanism there is from CredMan, which doesn’t define what to do with the abort signal.  If you navigate away and you’re holding these promises, they need to settle somehow.  
  * Lee: Browser will have to maintain the web state. Even if it’s not totally reflected in what the OS is showing.   
  * Marcos: In macOS and iOS we have code to check what’s showing.  
  * Lee: The browser would throw the result on the floor if no promises are pending.  
  * Helen: When you abort, I thought the expectation was the dev isn’t expecting to receive anything.  
  * Marcos: But the promises are still sitting there.  
  * Lee: You’re not returning the real result.  
  * Marcos: I think that’s more or less reflected in the current PR. Will have another read, and note that it may not be possible to shut down the OS UI.  
  * Wendy: Not quite ready to merge, but almost?  
  * Marcos: I’ll discuss with Mohamed tonight… On re-read, I think it might be OK.  
  * Wendy: OK to merge when Marcos and Mohamed agree.  

### [Define "prepare credential requests" algorithm \#420](https://github.com/w3c-fedid/digital-credentials/pull/420)  
  *  Marcos: Gotten quite a bit of review. Thanks John also. Latest comment from Tim re validation. John had proposed some additional clarifications. Tim asked for more discussion; I created [Issue 472](https://github.com/w3c-fedid/digital-credentials/pull/472).   
  * Lee: If a browser is going to parse further and reject based on additional criteria beyond what’s in OpenID4vc or mDocs, I think that should be in the spec. Or we should take it back to OpenID, ISO.  
  * Marcos: This is to say “here’s the point at which you apply constraints” but not defining what they are.  
  * Lee: Would you need that in the spec?   
  * Marcos: It’s for predictability. \[reads issue text\]  
  * John: My original concern was that it said, “if the request fails validation criteria defined in the specs,” and my thought was there might be other criteria applied by browsers.  
  * Lee: To have a consistent experience, if you’re making a fully valid request per protocol, and it’s not a hard security issue, if the browser is then asking for additional attributes, it seems *that* would lead to fragmentation, an anti-pattern. Maybe if a key has leaked, that’s cause for an exception, but I’m concerned about things that are more browser opinion, even in non-normative text.   
  * John: It seems we agree on some reasons the browser could deny a request, e.g., if there’s a revocation of a cert in an environment without a specified revocation mechanism. I don’t want to lose that ability.   
  * Lee: It's reasonable to say a browser could apply some additional security policy. I don’t think we should be calling out examples of discretionary refusals based on attributes.  
  * John: If the user has said, “I don’t ever want DC API to give out social security number,” it should be ok for the browser to block that  
  * Marcos: Privacy and security mitigations?  
  * Lee: User preferences? I don’t want to set the precedent of browser choice making some things impossible.  
  * Brian: Agreeing with Lee, there’s a big difference between user prefs and control, and paternalistic choices from the browser.  
  * John: I agree, the user agent is supposed to represent the user.  
  * Marcos: The TAG is putting together a User Agents Finding that we hope will be useful on what is the responsibility of the user agent. I might take this to the TAG. [https://www.w3.org/TR/web-user-agents/](https://www.w3.org/TR/web-user-agents/)   
  * Lee: I also see the argument that the user has made their choice by picking a browser, and the settings available there, But we also want consistency.  
  * Marcos: The experience is already fairly distinct. We compete on experience. Intent is to give a pointer to where things happen.  
  * Lee: I’d tend to defer to the lower layers.   
  * Marcos: Do you want to propose some text, Lee?  
  * Lee: I’d be happy to remove examples.  
  * John: If the carve out is there, I’m happy.  
  * Marcos: The rest of the PR is good to go; waiting for Tim to give another review. We have this issue (\#[472](https://github.com/w3c-fedid/digital-credentials/pull/472)) pulled out separately.  

### [Addressing Request Tampering \#426](https://github.com/w3c-fedid/digital-credentials/pull/426)  
  *  Marcos: I’ve been working with Simone and Mohamed. Trying to get considerations and their mitigations piece by piece. Would welcome review from others.  

### [Wallet Selection Binding during Issuance \#382](https://github.com/w3c-fedid/digital-credentials/issues/382)  
  *  Lee: this is getting much more critical: issuers saying they won’t use the API until we have it. Last time we talked, we agreed option 3 was preferred. See if that’s doable on iOS. More recently, option 4 is also looking attractive.   
  * … For the issuance flow, you’re getting a credential, getting “save to wallet”. The issuance protocol can contain a token, access token you’ll exchange for the credential (like a bearer token). Normally you’d call create, pass the token in, OS will give a selector asking which wallet, OS will hand the token to the wallet to say create the credential. If the token goes to a bad wallet, that wallet gets the cred. Most issuers have wallet attestation. They won’t issue creds to non-trusted, non-attested wallets, e.g. European issuer. Say the user has installed a bad wallet. …  
  * Ted: I’m involved in the VC and other groups, where there isn’t any binding that happens at issuance. The content of the credential can include something like authorized presenter, and how that can be confirmed, e.g., biometric. The credential itself is just a sequence of bytes.  
  * Lee: The holder-binding problem is slightly different from the issuance wallet-binding.  
  * Ted: The sequence of bytes could be on my physical desktop as a QR code. Why does it matter what wallet holds it?  
  * Lee: There are features of the wallet the issuer needs to know it has, e.g. European regs require wallet certification, so the issuer needs to know the wallet is certified. Payment credentials, you need to know the wallet can do transaction confirmation. At the moment, that’s done through certification.  
  * Ted: That’s regrettable law out in front of the tech.  
  * Lee: This issue assumes that the attestation system exists. If a bad wallet gets the token, injects it into an attested wallet on a bad phone, then goes to the issuer and gets the credential. There are real issuers who don’t want to use this API because this attack is possible. That’s why you don’t get “save to wallet” but rather “save to Google wallet” or “save to Apple wallet” as deep links, which isn’t what we want.   
  * … There are a few ways we could solve it. DC call could return which wallet was selected, not be spoofable. The problem is that normally the provisioning flow is async, and poor privacy properties.   
  * … Option 2, issuer could pass allow-list, filter. That perpetuates fragmentation, exposes OS-specific package names to the web.  
  * … Option 4\. You do allow lists with certs rather than package names, e.g., “I’ll accept any wallet certified by FIDO.”  
  * … Option 3\. Issuer passes a secret set of bytes (binding key) and hash with wallet name selected, wallet passes this during attestation. The issuer can recreate the hash to test for matching.   
  * Lee: I’m leaning toward 3 or 4\. 4 can also remove non-malicious wallets that would just fail. Question, especially to Marcos, how would iOS handle this?  
  * Marcos: We haven’t yet looked at / discussed web issuance. I think it’s great that you’ve experimented. I can take it to the wallet team  
  * Lee: I’m worried about putting a PR up and then turning out you can’t handle it.   
  * Marcos: We can signpost that issuance is all completely experimental at this point. I’ll take it to the wallet team, Hicham and friends.   
  * Lee: We’d welcome a signal. We’re open to anything that would work. THere are real issuers that have built issuance and are ready to launch on country-wide scale and are worried about this attack. The answer is not obvious, because of tradeoffs.   
  * Marcos: I’ll ping the wallet folks and see if they have an opinion

## AOB

* [EUDI Wallet functional conformance testing \#471](https://github.com/w3c-fedid/digital-credentials/issues/471)

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Wendy Seltzer (co-chair)  
* John Schanck (Mozilla Firefox)  
* Helen Qin (Google Android)  
* Lee Campbell (Google, Android)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* René Léveillé (1Password)  
* Bjorn Hjelm (Yubico)  
* Marcos Cáceres  
* Brian Campbell
