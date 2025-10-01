# FedID WG Telecon — DC API Series B, 2025-10-01

* Moderators: Heather Flanagan

* Scribe: [Granola.ai](http://Granola.ai) summary, reviewed by HF

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/participants/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/20240318/)  
* Ecosystem Updates (5 minutes)  
* DC API Issues & PRs (10+ minutes)  
  * [Wallet Selection Binding during Issuance \#382](https://github.com/w3c-fedid/digital-credentials/issues/382)  
  * [Relax the User Activation Requirement \#377](https://github.com/w3c-fedid/digital-credentials/issues/377)  
  * [Is a registry needed? \#345](https://github.com/w3c-fedid/digital-credentials/issues/345)  
* Any Other Business (AOB)  
  * [Preventing Abuse of Digital Credentials](https://w3ctag.github.io/prevent-credential-abuse/) \- Draft TAG finding


# Notes \- currently in progress via an AI app

## Administrivia

WG scheduled for two TPAC meetings Thursday and Friday

* One session focused on DC API work  
* One session focused on FedCM work  
* Joint discussion planned with payments groups for both work items

AI note-taking approved for meeting with chair review before publication

* Summary format preferred over verbatim transcripts  
* Tool used: [Granola.AI](http://granola.ai/) for local document enhancement

## Ecosystem Updates

Tim: End-to-end support table now available on digitalcredentials.dev

* URL: [https://digitalcredentials.dev/ecosystem-support?support-matrix=end2end](https://digitalcredentials.dev/ecosystem-support?support-matrix=end2end)

## DC API PRs and Issues

### [Wallet Selection Binding during Issuance \#382](https://github.com/w3c-fedid/digital-credentials/issues/382)

(Discussion led by Lee Campbell) 

Critical security issue with real-world complaints

* Multiple governments indicating they won’t ship until resolved  
* Issue URL: [https://github.com/w3c-fedid/digital-credentials/issues/382](https://github.com/w3c-fedid/digital-credentials/issues/382)

Problem description:

* Pre-authorization code flow vulnerable to man-in-the-middle attack  
* Malicious wallet can intercept credential offer tokens  
* Token forwarded to attacker’s device with legitimate wallet  
* Credential ends up in real wallet but on attacker’s phone  
* Similar vulnerability exists in WebAuthn passkey creation

Proposed solutions discussed:

* DC Create call returns selected wallet identifier  
  * Exposes OS-specific package names to web  
  * Issuance timing mismatch makes this ineffective  
* Issuer provides allow-list of acceptable wallet packages  
  * Still exposes OS internals  
  * Doesn’t scale for certified wallet ecosystems  
  * Fragmentation risk across issuers  
* Binding key approach (preferred by Lee)  
  * Issuer provides random binding token in DC API call  
  * OS computes HMAC(binding\_key, selected\_wallet\_package)  
  * Wallet receives HMAC but never learns binding key  
  * Issuer verifies HMAC matches wallet attestation  
  * Hybrid flow complications need resolution  
* PKI-based wallet attestation filtering  
  * Standardized attestation requirements  
  * Platform-level filtering before wallet selection  
  * Solves both security and UX issues  
  * Significant standardization effort required

Additional considerations:

* Privacy implications of wallet identifier exposure  
* Threat model assumes OS/browser integrity  
* Browser extension attacks remain unaddressed

### [Relax the User Activation Requirement \#377](https://github.com/w3c-fedid/digital-credentials/issues/377)

Current requirement: user must click before DC API can execute

* API fails silently with “user activation required” on page load  
* Prevents automatic credential requests in sign-in flows

Use case: Verified phone number credentials

* Less phishable alternative to SMS OTP  
* Direct cryptographic proof from SIM card  
* Desired UX: automatic presentation on page load similar to native apps

WebAuthn precedent:

* Originally required user activation  
* Chrome and Safari relaxed requirement \~3 years ago  
* iOS 17.4/macOS 14.4: WebAuthn callable without separate user gesture  
* Current behavior: can invoke after any user interaction with page  
* Reference: [https://developer.apple.com/forums/thread/747036](https://developer.apple.com/forums/thread/747036)

Proposal: achieve parity with WebAuthn behavior

* Allow DC API calls following user page interaction  
* Maintain UI requirements (no silent execution)  
* Consider conditional mediation patterns

### [Is a registry needed? \#345](https://github.com/w3c-fedid/digital-credentials/issues/345)

Brief mention of registry need assessment  
TAG Draft Finding on “Preventing Abusive Digital Credentials” may influence decision

* Document substantially complete  
* Could impact whether DC API needs active filtering vs. passive pipe approach  
* Identity Verification Workshop (London) outcomes also relevant

## 

## AOB

### [Preventing Abuse of Digital Credentials](https://w3ctag.github.io/prevent-credential-abuse/) \- Draft TAG finding

Pending spec merges blocked by dependencies

* Get steps marked as draft pending other algorithm merges  
* Marcus requesting prioritization for next meeting

TAG finding review recommended for all participants

* May influence registry decision and API design approach

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan  
* Wendy Seltzer  
* Helen Qin (Google Android)  
* Matt Miller  
* Lee Campbell  
* Marcos Caceres   
* Tobias Looker  
* Tim Cappalli  
* Brian Campbell  
  