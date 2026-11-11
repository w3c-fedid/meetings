# FedID WG — DC API — TPAC, 2026-10-28

* Moderators:  Heather Flanagan, Wendy Seltzer

* Scribe ( le zoom \+ highlights): Rick Byers \<3 

Logistics: See the [TPAC 2026 calendar](https://www.w3.org/events/meetings/0c6307c0-0cd8-4308-9343-b61e2042d15f/)

## Attendees

* Wendy Seltzer  
* Nick Doty (CDT)  
* Tara Whalen (W3C)  
* Rick Byers (Google Chrome)  
* Simone Onofri (W3C)  
* Mohamed Amir Yosef (Google Chrome)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Heather Flanagan (Spherical Cow Consulting)  
* …

## Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Welcome, status, and debrief from the joint WebAuthn / Web Payments / VCWG meeting **(14:00–14:15)**  
* [Architectural layering and the role of the DC API — \#589](https://github.com/w3c-fedid/digital-credentials/issues/589) **(14:15-14:30, chairs)**  
* [Privacy and security: outstanding issues and design requirements](https://github.com/w3c-fedid/digital-credentials/issues?q=is%3Aissue+state%3Aopen+label%3Aprivacy-tracker+OR+label%3Aprivacy-considerations+OR+label%3Aprivacy-needs-resolution) **(14:30–15:00, Tara/Simone)**  
* **Break (15:00–15:30)**  
* [Wallet selection binding during issuance — \#382](https://github.com/w3c-fedid/digital-credentials/issues/382) **(15:30–15:50, Lee)**  
* [Invocation context and clientData — \#574](https://github.com/w3c-fedid/digital-credentials/issues/574) **(15:50–16:10, Tim)**  
* [Conditional invocation — \#587](https://github.com/w3c-fedid/digital-credentials/issues/587) **(16:10–16:35, Malli)**  
* Decisions, actions, and next steps **(16:35–16:45)**

## Notes

### Welcome, status, and debrief from the joint WebAuthn / Web Payments / VCWG meeting **(14:00–14:15)**

* Wendy: Want to get to CR   
  * Each agenda item should include what we want to do and when we want to do it. 
     * Each issue comes with both “What do we want to do?” and “When do we want to do it?” What are our next steps: PR, Issue write-up, or Investigation.  When do we target the work, Pre- or Post-CR: CR-blocker, Future work, or No action
* Tim: Can we have a Level 2 doc we can iterate on in parallel like in WebAuthn?  
  * Or some other named branch?  
  * Marcos: prefers living standard, but sympathetic to needs from outside the W3C community for named versions  
  * Problem to address: users search for a document and end up with the wrong one (stale instead of current).  
  * Wendy: procedural question, chairs will confer and come back to this  
* Heather: Debrief from joint meeting  
  * Agenda, links to slides: [https\://github.com/w3c/wpsig/wiki/TPAC-2026-face%E2%80%90to%E2%80%90face-meeting-(26%E2%80%9027-October)\#joint-meeting-with-webauthn-wg-vcwg-and-fedid-wg](https://github.com/w3c/wpsig/wiki/TPAC-2026-face%E2%80%90to%E2%80%90face-meeting-\(26%E2%80%9027-October\)#joint-meeting-with-webauthn-wg-vcwg-and-fedid-wg)  
  * Adding an additional permission policy for 3DS iframes for DC is challenging — takes time to update standards and merchants.   
    * Rick: Should we consider whether any existing permission policies should imply DC in some way?  
  * [Manu had feature requests](https://www.w3.org/2026/Talks/TPAC/manu-interop-dcapi-tpac2026.pdf)  
    * Multi-turn in payments flows  
      * But likely solved by Apple's new proposal for multi-turn via PR API ("DCPM")  
    * Interaction URLs relying on TLS — reuse WebPKI instead of new PKI  
      * It's a mode of VP that we've said would not work in DC — goes out-of-band.  
      * We believe identity model needs to be more refined than just a domain name (which is all TLS certificates provide)  
    * If Manu is interested to invest in improving the DC API to meet his use cases, we'd love for his engagement in the group outside of TPAC

### [Architectural layering and the role of the DC API — \#589](https://github.com/w3c-fedid/digital-credentials/issues/589) **(14:15-14:30, chairs)**

* Heather: Suggest we use the architecture as documented on digitalcredentials.dev as our architecture  
  * E.g., to address the problem that "DC API" is used to refer to Digital Credential architecture as a whole. Need to be consistent on how we push back, what we point them to.  
  * Marcos: we do have some layering violations to meet our privacy principles — punching down into protocol  
    * Lee/Rick: architecture is sound but spec is monkey patch rather than a formal option/profile, which we should work to address  
    * Marcos: Is \#520 the right way to resolve this?  
    *   
  * Mamir: I believe the point is to separate the ecosystem pieces from the pieces which are ours.  
  * Heather: Yes  
  * Nick: Note digitalcredentials site still says protocol agnostic  
  * Tim: Yes that's old, PRs welcome, fixing this now  
  * Lee: Each layer has a set of extensibility (protocol, format, doctypes, etc.)  
  * Rick: We should make an effort to direct people to the right places for conversations, not only saying “not us”  
  * Lee: Yes, but we can also be opinionated. We don't completely relinquish our responsibility.  
  * Hicham: Agree there's not a hard line, but we can try to redirect to the right group. Some overlap between us and the other three (WG10, DCP and DCHP)  
  * Rick: Sometimes redirect to eIDAS process?  
  * Tim: Usually security, privacy and policy. Rarely technical.   
  * Nick: Agree clearer documentation would help, most frustrating is when redirects occur in loops and nobody takes responsibility  
  * Wendy: Hearing consensus that the layering described on digitalcredentials.dev will guide our responses to questions and try to be helpful to people who are looking for answers that should come from other groups.  
  * Heather: Yes and we should make sure that when we redirect elsewhere, elsewhere agrees they are the best forum

#### Next steps for the WG

* Will update the issue


### [Privacy and security: outstanding issues and design requirements](https://github.com/w3c-fedid/digital-credentials/issues?q=is%3Aissue+state%3Aopen+label%3Aprivacy-tracker+OR+label%3Aprivacy-considerations+OR+label%3Aprivacy-needs-resolution) **(14:30–15:00, Tara/Simone)**

*  Tara: starting with Privacy and focusing on the ones where next steps are unclear  
* [\#139 — Selective disclosure](https://github.com/w3c-fedid/digital-credentials/issues/139)  
  * Lee: issue of responsibility layering. Would prefer the browser could answer this one but the unsatisfying answer is the browser is deferring the answer to the wallet. The Wallet does have enough information.  
  * We can only say in the abstract sense that we're trusting wallets to be another user agent and do the right thing.  
  * In practice, there are other controls in the ecosystem — e.g., wallet certification. But we can't normatively spec this.  
  * Tara: so document this as known risk  
  * Nick: thought we could have a safer web with a clear presentation of different risk levels.  Sounds like users are not in a position where they can make a clear distinction? Maybe we should be clear that DC API is not great for low risk scenarios?  
  * Lee: Two issues: is the user adequately informed of what's being shared, how good is the tech of selective disclosure?  
    * Nick: yes also Ben has filed a separate issue (\#?)  
  * Marcos: selective disclosure isn't really selective — not optional  
  * Rick: In Chrome and Android we are doing work to help users understand the risk level — to visually and recognizably differentiate very different classes. Should our spec encourage platforms to do this?  
  * Mamir: \#252 should spec define what's shown in the permission prompt?  
  * Lee: have to do it post credential-selection — can't be just in the request.   
  * Nick: we could have designed the request to define what was going to be revealed. Maybe we can say that while you can't tell from the request, it puts added responsibility on the wallet to indicate that more information than was requested is being returned. We should be honest  
  * Hicham: Even very simple requests, only the wallet layer can understand what's being requested. E.g., in some countries there is no separation between the first and last name and if you request one you get the whole name. Can't promise at the browser level that we'll inform the user exactly what's being shared.  
  * David: privacy is a property of the whole system  
* Tara: We have a lot more to go through, how should we best handle it?  
  * Tim: should we setup a dedicated meeting — define contacts  
* [\#208: require in-context in-content explanation and an element for user-initiated presentation](https://github.com/w3c-fedid/digital-credentials/issues/208)  
  * Rick: Is this potential future work? Declarative entry points?  
  * Lee: Does RP validation help create accountability here?  
  * Marcos: Don't think we can make progress here, needs to be at the legislative layer  
* [\#266](https://github.com/w3c-fedid/digital-credentials/issues/266) registration of and commitment to a particular use case and purpose  
  * Will tag Marcos and Mohamed to answer implementation questions on this  
* [\#267](https://github.com/w3c-fedid/digital-credentials/issues/267) reporting abuse of credential requests  
  * All 3 editors will meet with Tara and Nick on all of these

#### Next steps for the WG

* Tara will update the issue ([\#139](https://github.com/w3c-fedid/digital-credentials/issues/139)) to be clear about the limits of what can be promised. Won't fully resolve it.   
* All 3 editors will meet with Tara and Nick on all of these

\[BREAK\]

### Leveling and CR

* Proposed: Levels (webauthn-style), with a big red box on the outdated version 

### 

### [Wallet selection binding during issuance — \#382](https://github.com/w3c-fedid/digital-credentials/issues/382) **(15:30–15:50, Lee)**

*  Rick: propose all of issuance is level 2  
  * Lee: as long as we start working on level 2 now  
  * Mohamed: issuance is very interleaved within the spec, will be quite some work  
  * Tim/Lee: want issuance still in level 1   
  * Rick: Can we get to rec with issuance in the spec but only impl in Chromium?   
  * Group: No  
  * Rick: Is there a plan to have issuance in WebKit by any particular time?  
  * Marcos: No  
  * Rick: So then we can't have issuance in level 1 \- will block us from REC indefinitely  
  * Heather: mark as at risk for CR and remove for REC  
  * Tim: can leave the framing \- API is supported at still targeting issuance.   
* Heather: we're going to remove issuance from the spec at level 1  
  * Then we will move to CR  
  * Lee: mechanically we'll make a branch for level 1

#### Next steps for the WG

Hold for future work

### [Invocation context and clientData — \#574](https://github.com/w3c-fedid/digital-credentials/issues/574) **(15:50–16:10, Tim)**

*  Tim: this is needed for the new protocol  
  * But as long as we can put it into L2 branch, its not needed for L1  
  * Mohamed: Marcos do you need topOrigin in L1?  
  * Marcos: Yes, but don't need the broader solution in L1  
  * Hicham: clientData will not be a short discussion  
  * Lee: then I think topOrigin can't be in L1  
  * Lee: clientData is just some data added by the platform as K/V pairs and it gets hashed. Doesn't impact the lower protocol. RP doesn't need to understand it.  
  * Hicham: why can't we do topOrigin without clientData?  
  * Tim: experience from WebAuthn suggests we shouldn't just keep adding things as one-off.   
  * Hicham: we can't decide here, affects other layers  
  * Tim: no, just a hash. Only affects PXP  
  * Marcos: Just want to be able to say we must show both origins when doing cross-origin.   
  * Mohamed: WebKit has a different architecture, webkit will draw it.  
  * Marcos: I need \#[512](https://github.com/w3c-fedid/digital-credentials/pull/512) for privacy \- doesn't need to change the response  
  * Lee: If \#512 is display only and just a recommendation, it doesn't hurt to have it in L1

#### Next steps for the WG

* Punt \#574 to L2  
* Take \#512 in L1 and discuss precise wording

### [Conditional invocation — \#587](https://github.com/w3c-fedid/digital-credentials/issues/587) **(16:10–16:35, Malli)**

* Helen: Malli created [\#596](https://github.com/w3c-fedid/digital-credentials/issues/596) to enable loading the paypal iframe and immediately invoke DC  
* Mohamed: Believe they need both  
* Lee: But if this is payment-specific then DCPM may solve it  
* Mohamed: This will take time to solve, take it out of L1  
* Marcos: Agreed

#### Next steps for the WG

* Leave comment in 587 saying we think it's superceded by 596, to confirm  
* Move 596 to L2

### Decisions, actions, and next steps **(16:35–16:45)**

* Mohamed: \#512 as L1 CR blocking  
* Marcos: We need to go through open PRs and check which ones  
* Wendy: The privacy ones are the big ones, we need to take Nick's concerns seriously and even if they can't be mitigated we need to add text documenting it.  
* Heather: \#565 is a CR blocker assigned to Tim  
* Tim/Mohamed: [\#520 is important](https://github.com/w3c-fedid/digital-credentials/pull/520): Specify protocol validation \+ enforce encryption- \#520  
  * Marcos: Could split these two parts out. Enforcing encryption is CR blocking.  
  * Mohamed: Seems fine directionally, need protocol expert to review  
  * Marcos: Martin has reviewed Annex-C and said it was fine  
  * Lee: I will review OpenID4vP parts offline, but looks fine  
  * Lee: we're not validating the whole request, just "enforcing encryption"  To just say "the OpenID4VP response mode must be one of the following"  
  * Marcos: Yes certainly possible to do it that way. I can abstract it back down.  
  * Mohamed: That will make this non-controversial  
* Heather: [Discuss \#506](https://github.com/w3c-fedid/digital-credentials/pull/506) Add security considerations on forged credential chooser request  
  * Approved in Series B, not covered in Series A call  
  * Marcos: This is a security consideration that burned us \- be resilient to compromised rendering process  
  * Tim: Approved  
  * Mohamed: Approved  
* Mohamed: [PR \#531 \- return array](https://github.com/w3c-fedid/digital-credentials/pull/531)  
  * Rick: Would need a way for the RP to indicate they support multiple responses  
  * Lee: Today array is in the OpenID4VP level when they come back from the same wallet. If they come back from two different wallets then the array has to be as the higher level for the encryption. Android now has the UX for returning multiple credentials from multiple wallets.   
  * Lee: Can't support in iOS since it does wallet selection  
  * Hicham: Has other implications \- responsibility on wallet to choose most privacy-preserving response. Not just about UX and encryption.   
* Wendy: High-level from this meeting  
  * We will try to address the outstanding privacy issues  
  * Will do triage to label everything as L1 or L2  
  * Marcos: Can we ask filers if they still consider the issues relevant?  
  * Heather: Yes but if no response we still need to triage ourselves  
  * Wendy: Have horizontal reviews, eg. Simone on security, Tara on privacy, accessibility, testing  
  * Marcus: Believe we can ask to mark accessibility as complete until they give us any specific text they want us to include  
  * Mohamed: Do not branch as long as we have L1-blocking issues, right?  
    * Group agreed

---

## Transcript-based supplementary summary

*Source: in-person/remote meeting transcript supplied with these notes. This section supplements rather than replaces the contemporaneous notes above. The transcript is an imperfect automated transcription: terminology has been normalized using the agenda and existing notes, and statements are attributed to individuals only where the original notes provide a reliable attribution. Discussion points are not characterized as formal resolutions unless the meeting explicitly reached a conclusion.*

### 1. Opening, progress toward Candidate Recommendation, and joint-meeting debrief

The chairs framed the session around a practical question for each issue: **what needs to be done, and when?** The intention was to distinguish work that must be completed before Candidate Recommendation (CR), work suitable for a subsequent level, and requests that need explanation or referral rather than a change to this specification. Where possible, each topic should end with an actionable disposition rather than another open-ended debate.

The first process discussion exposed a tension between getting a stable specification through CR and keeping dependent protocol work moving. The WebAuthn model of independently identified specification levels was offered as a way to continue landing and discussing new features while a prior level is under review. Others preferred a living specification because multiple versions can confuse developers and make maintenance harder. A GitHub branch by itself was considered an inadequate public explanation: dependent communities need an identifiable document and a clear account of which features belong to which release. The chairs deferred a concrete proposal until after the break (see **Section 4** below).

The debrief of the joint meeting with WebAuthn, Web Payments and the Verifiable Credentials Working Group addressed two feature requests associated with payments:

- **Multi-turn payment and credential flows.** Participants questioned whether a payment-specific multi-turn requirement might be served by work on the Payment Request API and the proposed Digital Credentials Payment Method (DCPM). The more general question of presenting a credential and then issuing something back to the same wallet, including a receipt-like result, remained distinct and was not resolved.
- **Interaction URLs and verifier identity.** The proposal discussed would let the DC API invoke a wallet, which would then use an interaction URL to complete presentation outside the API response path. Participants observed that this resembles an OpenID4VP mode previously considered unsuitable for the DC API. Using the URL's TLS certificate or WebPKI alone as the verifier identity was considered insufficient to address the more specific identity and accountability requirements of credential verification. Participants acknowledged they were interpreting the proposal and invited its proponents, including Manu, to bring a more precise use case and design into the Working Group.

A recurring concern was that external discussions sometimes treat the DC API as if it encompassed the whole digital-credential ecosystem. That concern led directly into the architectural-layering agenda item.

### 2. Architectural layering and responsibility — [issue #589](https://github.com/w3c-fedid/digital-credentials/issues/589)

The group supported using the layered architecture described at [digitalcredentials.dev](https://digitalcredentials.dev/) as a **shared reference for explaining the DC API's responsibilities and those of other layers**, without necessarily copying that entire architectural model into normative API text. The purpose was not simply to exclude work from the Working Group: it was to help reporters of issues find a forum that could actually address their concerns. Redirects should be checked with the receiving group to avoid sending stakeholders around a circle of organizations that each deny responsibility.

Participants also challenged any claim that the layers are completely isolated. The current DC API intentionally constrains particular protocol behaviors in order to meet privacy and security requirements: the discussion cited prevention of unwanted mdoc “phone-home” behavior and enforcement of encrypted responses for OpenID4VP. These constraints were described both as possible *layering violations* and as an intentional consequence of narrowing the API to defined protocol bindings rather than operating as an entirely opaque transport. The relevant architectural question is how to express these constraints cleanly—ideally through explicit supported options or profiles—rather than through ad hoc inspection and patches in the API specification.

The meeting did **not** establish a rigid rule that all privacy or security concerns belong exclusively to downstream protocol or wallet specifications. Participants recognized overlapping duties across the browser, wallet, protocol and ecosystem governance layers. They also noted that the explanatory architecture may need updating: the existing description of the API as wholly protocol-agnostic no longer accurately captures the current design.

**Outcome / follow-up:** Use the layering model to guide responses to issues, correct outdated architecture descriptions, and update #589 to record the group's guidance. Where work belongs elsewhere, identify and engage the appropriate owner rather than merely closing the request as out of scope.

### 3. Privacy and security issue review

The privacy session focused on issues whose *resolution path*, rather than only their technical merit, remained unclear. A central theme was the difference between **what the browser can know at invocation time**, **what the wallet can know when selecting a credential and preparing a response**, and **what governance or certification can require of ecosystem participants**. Privacy assurances can depend on the whole system; the DC API alone cannot guarantee the behavior of every component.

#### [Issue #139: selective disclosure](https://github.com/w3c-fedid/digital-credentials/issues/139)

The discussion distinguished selective-disclosure mechanisms from meaningful user comprehension of the information actually released. Participants stressed that a request may not reveal the final set of claims disclosed; format, credential structure, matching and wallet behavior determine what is ultimately sent. Even seemingly simple fields can differ across jurisdictions or document models—for example, a request for one part of a name might disclose a complete name. A browser prompt shown before credential selection therefore cannot reliably enumerate all released information.

Several participants argued that this places an especially important obligation on the wallet or platform UI **after credential matching or selection**, when the concrete disclosure can be identified. There was concern that the API might be presented as privacy preserving without providing users sufficient information to recognize different classes of disclosure and risk. Platform UI and ecosystem measures such as wallet certification may help, but the group cannot guarantee such controls normatively through the DC API specification alone. The browser could potentially help distinguish broad categories of risk, but there was no agreement on specific normative UI requirements.

**Outcome / follow-up:** Tara will update #139 to document the limits of what the API can promise, the residual user-information risk, and the respective responsibilities of wallets and platforms. The issue was **not fully resolved** by the discussion.

#### [Issue #208: in-context explanation and user-initiated presentation](https://github.com/w3c-fedid/digital-credentials/issues/208)

This issue raised whether websites should explain *why* they are asking for sensitive credentials and whether the API should offer a structured, user-initiated entry point. Nick emphasized that users may otherwise be asked for a driver's license or passport with no useful explanation of purpose. Others noted that arbitrary webpage explanations or unverified free-form purpose strings are weak safeguards: a malicious requester could supply persuasive but misleading text. Standardized request templates or purpose categories might be more meaningful but could be hard to define and scale.

Participants considered whether some elements were better treated as authoring guidance, later declarative APIs or broader regulatory obligations rather than current DC API requirements. Verified requester identity, signed requests and potentially signed statements of purpose were raised as possible ways to improve accountability, particularly after the fact. These were **possibilities, not adopted solutions**. Purpose-specific APIs, such as those under discussion for age-related use cases or payments, may address some narrower scenarios; the general problem of explaining requests for full identity documents remains.

**Disposition:** The group did not agree on a specific Level 1 mechanism. It discussed retaining this as potential future work while making the privacy trade-off and any available guidance clear. The transcript records disagreement about whether leaving an issue open is useful if there is no plausible commitment to implement a remedy.

#### [Issue #266: registration, use case and purpose](https://github.com/w3c-fedid/digital-credentials/issues/266) and [issue #267: reporting abuse](https://github.com/w3c-fedid/digital-credentials/issues/267)

These issues concerned accountability for requests, including possible commitments to stated purposes and a way to report abusive or excessive requests. The discussion treated them as closely connected to trust infrastructure, enforcement and regulatory processes, rather than as straightforward browser API requirements. Participants questioned whether the DC API is the right place to define a mechanism for reporting to data-protection authorities or policing requesters.

**Outcome / follow-up:** The three editors will meet with Tara and Nick to review these and related privacy issues together, taking account of changes to the specification since the issues were originally filed. Marcos and Mohamed were identified for implementation questions on #266. The meeting discussed arranging that focused review within roughly the next two weeks; this was an intended follow-up, not evidence that it occurred.

#### Wider privacy-review implications

The group recognized that **documenting a known risk, narrowing a guarantee, referring to another specification or assigning future work can be a legitimate issue disposition**, provided it is reasoned and recorded. However, this is not a substitute for addressing substantive privacy concerns. Near the end of the meeting, the chairs reiterated that the outstanding privacy issues remain a major part of the CR work: issue reporters' concerns must be considered seriously, and unresolved limitations may need explicit Privacy Considerations text even if no normative API mitigation is practical.

### 4. Specification levels, issuance, and [issue #382](https://github.com/w3c-fedid/digital-credentials/issues/382)

Following a discussion during the break, the chairs proposed **WebAuthn-style levels**: a stable Level 1 could progress through CR toward Recommendation while work on Level 2 continued. The older recommended level would prominently direct developers to the current level under development, while giving regulators and other parties a stable, identifiable W3C Recommendation to reference. The proposal was accepted as a workable compromise, not necessarily every participant's preferred publishing model.

This decision changed how the Working Group triaged features. Rather than resolving the detailed wallet-selection-binding design immediately, the group first asked whether **issuance itself could be included in Level 1**. Participants observed that issuance is interleaved throughout the draft, so removing it would be editorially and mechanically significant. Some wanted to preserve it, especially if Level 2 could be developed immediately. The critical constraint was implementation support: there was no stated plan for WebKit issuance support, and participants did not consider a Chromium-only implementation sufficient to advance issuance to Recommendation. The discussion also noted that the relevant European regulatory requirement did not require the API to support issuance.

**Outcome:** The meeting's working direction was to **remove issuance from the Level 1 specification** and continue its development in Level 2, allowing Level 1 to progress toward CR once other blockers are resolved. The precise branching sequence and mechanics still required editor coordination. The transcript makes clear that **removing issuance does not mean abandoning or stopping its development**, and the detailed #382 design discussion was accordingly held for subsequent work.

### 5. Invocation context, `clientData`, cross-origin display — [issue #574](https://github.com/w3c-fedid/digital-credentials/issues/574) and [PR #512](https://github.com/w3c-fedid/digital-credentials/pull/512)

The proposed `clientData` model would give the platform a structured place to state invocation-context information and have it cryptographically bound through a hash, drawing on a design pattern familiar from WebAuthn. Supporters argued that this would avoid an accumulating series of one-off additions whenever the API needed to convey another property of the browser or request context. They also argued that lower-level protocols could bind the hash without needing to understand or revise every individual field.

Others questioned whether the model's semantics and security assumptions transfer cleanly to digital credentials, whether relying parties can verify all proposed fields, and how such a change interacts with the protocol and format layers—particularly cross-device flows and the work of DCHP. The group also discussed **where trusted client data would be constructed** and the need to guard against a compromised rendering context forging it. The transcript reflects a substantial unresolved cross-layer design debate, not agreement to introduce the whole model immediately.

A narrower Level 1 requirement was treated separately. WebKit needed the ability to convey/display the **requesting and top-level origins** for cross-origin use. PR #512 was understood as a recommendation about showing the user both origins in the relevant UI, **not** a change to the cryptographic response format. That narrower form could be advanced without deciding the full `clientData` model.

**Outcome:** Defer #574 and the broader `clientData` design to **Level 2**; retain **PR #512 in Level 1**, with its precise wording still to be agreed. This was also identified in the closing discussion as Level 1/CR-blocking work. No consensus was reached on the full scope or content of `clientData`.

### 6. Conditional invocation and user activation — [issues #587](https://github.com/w3c-fedid/digital-credentials/issues/587) and [#596](https://github.com/w3c-fedid/digital-credentials/issues/596)

The discussion clarified that the original request bundled more than one problem. One was a **conditional or passive user experience**. Another was loss or absence of **transient user activation** when a payment-related flow creates or navigates to an iframe and wants to invoke the DC API immediately, without requiring a second click inside that frame. These are not identical requirements. Participants described possible distinctions between iframe invocation, same-origin navigation and cross-origin navigation, with different implications for the platform's user-activation model.

The newer #596 was understood to capture the more concrete iframe/activation use case, while #587 might no longer express the main problem. The group wanted the requesters to confirm the intended use cases and whether the remaining conditional-experience requirement is independent. Participants also observed that some payment cases may ultimately be served through DCPM or related Payment Request mechanisms, but did not establish that those efforts solve the general browser-platform problem.

**Outcome / follow-up:** Comment on #587 to confirm whether it has been superseded by #596; treat #596 as **Level 2** work rather than a CR blocker. Further clarification and platform design discussion are required.

### 7. Closing triage, open pull requests and CR readiness

The chairs returned to the remaining work needed to make a defensible CR transition. They emphasized that a Level 2 label should not be used to dispose of privacy concerns without analysis. The group needed to revisit open issues and PRs, identify Level 1 blockers, ask issue filers for updated views where helpful, and still make its own disposition decisions if no reply arrived. The chairs also noted ongoing horizontal review, implementation, accessibility and testing work.

Specific pull requests and issues discussed:

- **[PR #520 — protocol validation and response encryption](https://github.com/w3c-fedid/digital-credentials/pull/520):** Enforcing response encryption was treated as **CR-blocking**. Participants considered separating this narrow requirement from broader request validation. In particular, the API might specify permitted OpenID4VP response modes rather than appear to define complete validation of the underlying protocol request. The goal is to prevent unacceptable behavior, including unwanted phone-home behavior, without unnecessarily taking ownership of full protocol validation. Review of the mdoc Annex C portion had reportedly occurred; Lee offered to review the OpenID4VP portion offline. Further editing and review were needed, not an unconditional approval of the entire PR.
- **[PR #506 — forged credential chooser request security considerations](https://github.com/w3c-fedid/digital-credentials/pull/506):** Revisited because it had been approved on a Series B call but not addressed on Series A. The issue concerned resilience when the rendering process is compromised and protection of the integrity of credential chooser requests. The contemporaneous notes record approval by Tim and Mohamed. The transcript discussion was supportive of landing the security considerations.
- **[PR #531 — returning an array of responses](https://github.com/w3c-fedid/digital-credentials/pull/531):** Multiple credentials from **one wallet** can be represented within one protocol response; credentials from **different wallets** introduce a higher-level array of responses because they can have different encryption contexts. Android's credential-selection model makes this newly useful, while iOS's wallet-selection model creates a different implementation constraint. Participants noted potential compatibility problems for existing JavaScript callers, the possibility of an opt-in or new return type, and a further privacy question about who chooses the least-disclosing combination across wallets. The feature was regarded as **future work rather than a settled Level 1 change**; the precise API shape was left open.
- **[Issue #565](https://github.com/w3c-fedid/digital-credentials/issues/565):** Identified as an outstanding CR blocker assigned to Tim; described in discussion as comparatively small or largely editorial, but still requiring resolution.
- **[PR #512](https://github.com/w3c-fedid/digital-credentials/pull/512):** Remains Level 1 work; exact wording on cross-origin UI display needs agreement.

The group reiterated that CR readiness requires more than a small functional feature set. Open privacy and security concerns require documented responses; outstanding PRs must be classified; horizontal reviews and process requirements must be completed. The transcript also records positive remarks about internationalization review, the state of accessibility review, and tests accompanying PRs, while noting remaining procedural work on status and change descriptions. **The group agreed not to cut the Level 1 branch while Level 1-blocking issues remained unresolved.**

### Consolidated follow-up checklist (from both records)

- [ ] Update [#589](https://github.com/w3c-fedid/digital-credentials/issues/589) to document the agreed architectural reference, realistic layer boundaries and referral approach; correct obsolete “protocol-agnostic” explanations.
- [ ] Tara to update [#139](https://github.com/w3c-fedid/digital-credentials/issues/139) with limits on disclosure assurances and residual risks.
- [ ] Arrange a focused review by the three editors, Tara and Nick of the remaining privacy issues, including [#208](https://github.com/w3c-fedid/digital-credentials/issues/208), [#266](https://github.com/w3c-fedid/digital-credentials/issues/266) and [#267](https://github.com/w3c-fedid/digital-credentials/issues/267); identify changes, documented risks, future work and external ownership as appropriate.
- [ ] Triage every open issue and PR for Level 1/CR blocking status versus Level 2, recording a reasoned disposition even when no specification change is required.
- [ ] Plan Level 1 removal of issuance and continued Level 2 development; agree branch and publication mechanics after Level 1 blockers are resolved.
- [ ] Advance [PR #512](https://github.com/w3c-fedid/digital-credentials/pull/512) with agreed Level 1 cross-origin UI wording; defer broader [#574](https://github.com/w3c-fedid/digital-credentials/issues/574) `clientData` work to Level 2.
- [ ] Seek confirmation whether [#587](https://github.com/w3c-fedid/digital-credentials/issues/587) is superseded by [#596](https://github.com/w3c-fedid/digital-credentials/issues/596); address #596 in Level 2.
- [ ] Revise and review [PR #520](https://github.com/w3c-fedid/digital-credentials/pull/520), preserving the CR-blocking encryption requirement while clarifying the scope of validation; obtain the remaining OpenID4VP review.
- [ ] Complete disposition of [PR #506](https://github.com/w3c-fedid/digital-credentials/pull/506) and [issue #565](https://github.com/w3c-fedid/digital-credentials/issues/565); return to [PR #531](https://github.com/w3c-fedid/digital-credentials/pull/531) for future API design and privacy analysis.
- [ ] Confirm status of horizontal reviews, testing, and required CR transition documentation.


