# W3C TPAC 2026 — Federated Identity WG/CG: FedCM

**Date:** Thursday, 29 October 2026  
**Scheduled time:** 09:00–12:30 UTC (as stated in the supplied agenda)  
**Location:** Ground Floor, Munster Suite, TPAC 2026  
**Meeting:** Joint Federated Identity Working Group / Federated Identity Community Group session  
**Chairs:** Heather Flanagan and Wendy Seltzer  
**Source:** Supplied agenda and automated meeting transcript (no separate contemporaneous meeting notes)  
**Meeting information:** [W3C TPAC calendar](https://www.w3.org/events/meetings/12acdd89-4ae5-470c-878d-d1bac82f2416/)

> **Editorial note.** These are reconstructed, substantive minutes rather than a verbatim transcript. The transcript frequently splits sentences into fragments, mishears technical terms (notably FedCM, Credential Management/CredMan, OAuth, IdP, RP, and SD-JWT), and assigns inconsistent speaker labels. Terminology has been normalized where the surrounding discussion supports the interpretation. Speaker names are retained only when clear from the conversation. Comments, demonstrations and proposals should not be read as formal Working Group resolutions unless explicitly characterized as such. No attendance roll or confirmed resolutions list was supplied.

## Agenda

1. Administrivia (chairs, 09:00–09:10)
2. FedCM today: core, dependencies and extensions (Sam Goto, 09:10–09:40)
3. Deployment and implementation roundtable; browser implementations and interoperability (open discussion, 09:40–10:30)
4. Break (10:30–11:00)
5. FedCM spec editing, issue/PR review (spec editors, 11:00–11:30)
6. Unifying mediated credentials: FedCM, Digital Credentials API and email verification (Sam Goto, Lee Campbell, Helen Qin, 11:30–12:20)
7. Wrap-up, actions and next steps (chairs, 12:20–12:30)

**Agenda adjustment:** Following the break, the chairs used the time reserved for general specification editing to revisit the previous day's *FedCM Across Browsers: What Would It Take?* discussion. A line-by-line issue/PR review did not take place in the portion of the recording reviewed.

## Summary of outcomes

The session highlighted both FedCM's substantial real-world deployment in Chromium-based browsers and its continuing interoperability problem: meaningful advancement toward Candidate Recommendation requires engagement and independently implementable commitments from other browser engines. Participants regarded the previous day's discussion with Apple and Mozilla as encouraging, but there was no reported commitment by either vendor to implement the present specification. There was disagreement over whether the best approach is a **smaller normative core** or an **incremental implementation sequence**; browser user-interface and product-strategy costs may matter as much as protocol complexity.

The technical centerpiece of the latter part of the meeting was a prototype for **OAuth-based platform mediation**, intended to make FedCM-style identity-provider sign-in work from Android native applications and to explore common infrastructure for FedCM, the Digital Credentials API, and email verification. The group identified promising architectural reuse, but also significant unanswered questions about consent, token scoping, endpoints, IDP migration, API layering and the appropriate standards venues. The chairs offered to convene a cross-area task force, with privacy specialists involved early.

These are **directions for follow-up, not adoption of a new architecture or changes to the specifications**.

---

## 1. Administrivia and meeting framing

The chairs welcomed Working Group and Community Group participants, guests and observers, reiterated the W3C Code of Conduct, and reminded attendees to keep disagreements focused on the work. Zoom transcription served as the primary scribing mechanism. The chairs noted the intention to create edited, non-verbatim minutes from the recording and requested presenters' slides for inclusion with the meeting record.

The agenda was framed around the current state of the FedCM specification and incubation pipeline, deployments and UX experimentation, the practical possibility of cross-browser support, and future architectural work across mediated credential APIs.

## 2. FedCM today: core, dependencies and extensions

### 2.1 Maturity stages and document status

Sam Goto described a working mental model for proposals, borrowing stage terminology from TC39. He expressly presented this as an explanatory model rather than a new formal decision:

- **Stage 0:** An idea or problem being explored, potentially beginning as a GitHub issue, without a threshold for demonstrated support.
- **Stage 1:** A proposal the Community Group considers worth incubating, normally with a dedicated repository, explainer and issue discussions; the primary task is understanding the problem and requirements.
- **Stage 2:** A concrete, technically plausible approach that has moved beyond exploration, generally with enough agreement to warrant Working Group specification and implementation effort.
- **Stage 3:** Independent implementations and the kind of cross-browser validation needed for Candidate Recommendation progress.
- **Stage 4:** A completed mature specification / Recommendation-stage outcome in this model.

Sam indicated that FedCM had work in Stages 0–2 but no proposals at Stages 3–4. That absence of independent implementations is a major part of the later browser-engagement discussion. He distinguished proposal repositories, the editor's draft (including work not necessarily agreed by the full WG), and the Working Draft, which represents the group's agreed specification direction. The First Public Working Draft reflects the Stage 2 baseline, not every incubating extension.

### 2.2 Features in the Working Draft

The current baseline includes the structural FedCM API and a number of additions promoted from incubation, notably:

- The **Login Status API**.
- **Active mode**, which supports an explicitly initiated, modal sign-in flow.
- **Continuation-related functionality**, including account labels, parameters and mode.
- **Multiple identity-provider support**.

Sam described these as features deployed in stable Chrome and Edge, with other Chromium-derived browsers likely also benefiting. The claim was about shipped Chromium-family functionality, **not independent implementations in different engines**.

### 2.3 Deployment snapshot and cautions about the numbers

Sam cited significant social-login adoption, naming Google, Facebook and Shopify as prominent examples, with Microsoft developing further IdP support. He gave rough deployment-scale figures of **approximately 3% of Chrome page loads** and **hundreds of thousands of sites (roughly 300,000–400,000 or more)**; he also cautioned that Shopify accounts for a large share of the footprint. These figures were spoken estimates, not independently audited metrics presented with methodology in the recording. He characterized consumer login choices as roughly divided between passwords and social login, with passkeys presently affecting primarily the password side of that comparison. The discussion did not claim this generalizes to enterprise or education identity deployments.

### 2.4 Stage 1 proposal pipeline

Proposals mentioned as actively incubating, at differing levels of readiness, included:

- **Accounts Push API**, from ideas previously described as *lightweight FedCM*, allowing IdPs to push account information toward the browser rather than relying solely on browser pulls.
- **Open-world / IdP registration**, making it possible for users to select providers beyond a list preselected by the RP.
- **Delegation / privacy-preserving federation**, intended to reduce or change when the IdP learns about a user's interaction with an RP. The transcript's phrasing of this feature is imprecise and should not substitute for its explainer.
- **Identity Handler**, championed in particular by Microsoft, to accommodate IdP-specific handling and proof requirements.
- **IdP-initiated functionality** (the term itself was later questioned as potentially confusing to identity practitioners).
- Possible **HTML-based login entry points**, **approved-site or agentic login mechanisms**, and **native-app IdP support**.

Stage 1 should not be interpreted as a commitment to incorporate each proposal into the Working Draft. The stage and implementation-readiness of individual ideas differ.

## 3. Deployment, integration and implementation roundtable

### 3.1 Linked Web Storage / Solid compatibility

A representative of the Linked Web Storage work described FedCM as potentially useful at the boundary where an application obtains an identity credential, while making clear that the LWS specification does not itself depend on FedCM. Conventional federation with known governance and providers was seen as relatively straightforward. The **open-world** model, including Solid-like decentralized deployments, creates additional challenges.

A central problem is **cold-start discovery across RPs**: a user who has logged in with a provider on one site may have to rediscover that provider at every subsequent RP. IdP registration could help. **Handle resolution**, however, was identified as a remaining gap, including questions about validating or resolving provider and RP identity without allowing spoofing across contexts.

The group also discussed **brokered OpenID Connect providers**. A broker that exposes the necessary FedCM endpoints can potentially perform the downstream redirect or authentication chain itself. But a more complicated case—an IdP broker using FedCM while its downstream IdP also tries to invoke FedCM—was identified as needing investigation. No conclusion was recorded that nested FedCM invocations are supported.

### 3.2 Microsoft Edge and Identity Handler

An Edge participant explained why some enterprise IdPs need an Identity Handler: Microsoft's IdP can require **device-bound or device-specific proof** in addition to session-cookie authentication, which the ordinary FedCM request path does not readily attach.

The proposal uses a **service worker** associated with the IdP to mediate the relevant handling, including cases where the user has not first visited an IdP page. Doing this reliably requires service-worker lifecycle and registration/unregistration hooks. Rather than inventing incompatible service-worker behavior inside FedCM, the implementers were coordinating changes with the Service Workers specification. One relevant change was described as merged and others as under review; no definite completion date was given. Subsequent work would include browser implementation and testing against actual Microsoft IdP requirements.

The discussion also raised whether the proposal's mention of **OAuth DPoP** corresponded to a complete, workable DPoP use case or merely to more general proof-of-possession signing. A participant questioned where the relevant private key would reside and whether an IdP-context handler could meet the relying party's needs. The presenter did not settle that point and undertook to check the DPoP-specific claim. These should remain open technical questions.

### 3.3 IdP discovery and deployment constraints

Discussion of educational/research federations emphasized that many IdPs do not control the apex domain or the deployment environment sufficiently to publish required `/.well-known/` material. Some federations already distribute metadata through federation operators, but that approach introduces questions of staleness, configuration and discovery. Hosted enterprise IdPs can encounter analogous constraints. The group discussed possible approaches but did not agree on a universal solution.

**Follow-up:** Participants acknowledged at least one known mismatch or awkwardness in the current well-known/discovery approach and requested a GitHub issue if one was not already filed, to ensure the problem is tracked. This is not a recorded resolution of the discovery design.

### 3.4 Chrome: active and passive modes

Chrome's implementation presentation illustrated the distinction between two interaction models:

**Active mode** is triggered by an explicit user action, such as clicking *Sign in with Google*. The browser can present a relatively prominent, modal account-selection interface in the RP's context. A key usability goal is to complete the initiated sign-in journey even when the user first needs to authenticate with the IdP or select another account. Mediation avoids some top-level redirects and popup flows, and may be more resilient to bounce-tracking mitigations.

**Passive mode** may be invoked as a page loads without a specific click. Chrome's browser-owned interface can present an available account without handing information to the RP until the user acts. Because it is unsolicited, the browser must be free to **suppress, delay, quieten or disable** prompts. Closing a prompt may trigger increasingly lengthy quiet periods; users can also disable passive prompts in browser settings. Consequently, passive mode does **not** promise successful sign-in on every invocation.

### 3.5 Less intrusive UX, account selection and multi-IdP behavior

Chrome described production experiments or deployments that substitute a **quieter omnibox/toolbar chip** for the more prominent passive account prompt in circumstances where the user is less likely to engage. The implementation was described as using signals including prior engagement and site-level information to choose an appropriate presentation. Participants questioned how any such ranking could be transparent, predictable and genuinely nonintrusive.

Chrome also demonstrated or described **ambient credential selection**, with a browser-controlled place for users to find federated accounts, passkeys and passwords. Account-creation prompts could be more subdued for new users, while previously used accounts might be shown more prominently on return visits. The UI could expand to reveal additional credentials and IdPs, including cases where a site requests more than one provider or credential type.

Important caveats from the discussion:

- Some demonstrated UI was **prototype/Canary work**, not a final standard design or a shipped behavior across browsers.
- An expanded, persistent prompt while a user scrolls was criticized as intrusive; the group discussed collapsing or dismissing it based on engagement.
- Presenting a chip branded with one IdP raises **discoverability** questions when other providers are available.
- How the RP specifies providers, how the browser chooses which account to foreground, and how open-world IdP registration interacts with both remain open UX considerations.
- Participants asked how a passkey belonging to an IdP would be represented alongside a federated account and how to prevent confusing duplication.
- Chrome indicated that FedCM-specific state was **not currently synchronized through Chrome Sync** in the way questioned during the presentation.

The examples illustrated browser implementation choices; they were not put forward as normative UI requirements for FedCM.

### 3.6 Agentic sign-in and trusted browser UI

A demonstration considered an AI-assisted browser flow in which an agent encounters a need to sign into a site and the browser surfaces a **trusted account chooser**. Participants questioned whether an account-selection interface displayed near an agent conversation would be distinguishable from agent- or webpage-controlled UI, and how a user could recognize the security boundary. The presenters said the account chooser in the demonstration was browser-controlled, not content the agent could manipulate.

Questions also concerned what happens if browser, assistant and IdP come from **different vendors**, rather than all being supplied in a single bundled environment. The presenters said those combinations, and the corresponding UX conventions, were not settled. One participant noted that the slides had already shown several different places where browser-controlled sign-in UI could appear, reinforcing the need for a coherent user mental model.

The roundtable also raised delegated authority and parental approvals for children or teenagers using agents. The immediate browser-login demonstration assumed an existing account rather than an account-creation or approval flow. Participants acknowledged the importance of broader agent authorization and consent, but did not treat it as solved by FedCM sign-in.

---

## 4. Multi-browser support and interoperability (replacing the scheduled general issue review)

The chairs shifted this agenda slot to a debrief of the prior day's TPAC meeting with representatives of **Apple/Safari and Mozilla/Firefox**, whose participation in the current FedCM implementation effort had been limited. This session did not include the absent representatives speaking again; it was a discussion of how participants interpreted their earlier feedback.

### 4.1 Encouraging re-engagement, but no implementation commitment

Sam Goto reported hearing encouragement that the work was not proceeding in an obviously unacceptable direction and that further conversation could be productive. He identified interest in **privacy-preserving delegation**, with **open-world provider choice** also appealing to some participants. Those impressions were expressly provisional; the group intended to confirm them directly with the browser representatives before publishing a summary.

### 4.2 Small mandatory core versus implementation sequence

There was a meaningful difference of interpretation about what non-Chromium vendors needed:

- One view was that they wanted a **sequencing strategy**: a tractable order in which to implement and evaluate FedCM features.
- Another was that they were seeking a **minimal interoperable, mandatory core**, with some functionality explicitly optional or deferred so that a browser could be conformant without committing to the full existing surface.

These approaches overlap, but are not identical. A sequence does not by itself resolve what an implementation **must** support for conformance. The discussion did not settle the question, and it would be inaccurate to describe a reduced FedCM core as approved.

### 4.3 Why UX is an interoperability constraint

Participants emphasized that implementing the protocol may be less costly than securing the necessary **browser interface surface**. Small-looking changes to the address bar, permission dialogs or account chooser can entail substantial browser product, interaction and privacy review. Different browsers already make very different choices about the presentation of ordinary permissions.

A suggestion was made to publish **non-normative UX patterns or reference wireframes**, without dictating a single visual design. This could help other engines evaluate the interaction costs. Others cautioned that current UX knowledge is disproportionately based on Chromium and would need careful framing to avoid becoming de facto Chrome guidance. The discussion also touched on broader **ecosystem strategy**, including how improving federated login relates to browsers' investment in passkeys and account systems.

### 4.4 Follow-up with Apple and Mozilla

The chairs proposed to prepare a **written synthesis** of the previous day's discussion, not merely circulate raw notes, and to share it with the Apple and Mozilla participants for correction and agreement. Participants expressed a desire for recurring engagement **between annual TPAC meetings**. The earlier discussion reportedly included offers to join further calls, though timing and participation had not yet been arranged.

**Action direction:** Draft a summary of the browser feedback; ask the relevant browser representatives to verify that it accurately reflects their constraints and interests; arrange a follow-up conversation. No exact date or implementing commitment was agreed in this session.

---

## 5. Unifying mediated credentials: FedCM, Digital Credentials API and email verification

**Presenters:** Helen Qin, with Lee Campbell and Sam Goto. This was presented as a combination of a relatively concrete **platform-to-provider mediation proposal** and a less-developed **problem statement** about unifying application-facing credential APIs. The two parts should not be conflated.

### 5.1 Immediate motivation: FedCM in Android native applications

FedCM's current browser-centric approach authenticates interaction with the IdP partly by relying on **IdP cookies in the browser**. Android's operating-system credential mediation cannot simply assume it owns or can use the browser's IdP cookie jar. Native apps and embedded WebViews also create security and UX problems when an IdP is asked to authenticate within an app-controlled environment. Some IdPs restrict those environments, and passkeys or other phishing-resistant authentication may be unavailable or unsafe in them.

The design goals presented included:

- Support for **native apps and WebViews**, not only browser pages.
- Safe, platform-controlled authentication at the IdP, including use of passkeys.
- A trusted process isolated from the calling application during IdP sign-in.
- A usable flow when the user is not yet signed in or lacks a native IdP application.
- Reuse of an existing **IdP authentication session** without bypassing **per-request consent** for a different RP or app.

### 5.2 Proposed OAuth-based platform mediation

The prototype replaces cookie-dependent platform-to-IdP interactions with **OAuth-based authorization and token exchange**. A trusted platform uses the IdP's authorization and token endpoints to establish a platform-held credential (called a **platform broker token** in the presentation). It then uses that relationship to obtain suitably scoped tokens or credentials for individual requesting applications.

The proposal's intended boundary is significant: **the platform broker token is not an RP token to be shared among apps**. The first user sign-in can be reused to avoid repeated authentication, but each RP/app obtains its own scoped response with an appropriate consent step. This distinction was clarified only after participants pressed for it during the demonstration.

The presenters described a **display metadata endpoint** that would provide account or credential display information to the platform, analogous in purpose to FedCM's account endpoint. Participants asked whether existing OAuth or OpenID Connect metadata or UserInfo facilities might provide the necessary function. The endpoint's semantics and whether a new standard is actually necessary remain to be determined.

### 5.3 Android prototype and consent questions

The demo showed a native Android app requesting federated sign-in. On first use, the platform initiated an IdP authorization flow in a trusted surface, allowed passkey authentication, and separately asked the user to approve the app's use of the resulting identity assertion. Subsequent sign-in could avoid repeating the IdP login ceremony while still presenting RP-specific permission.

A participant challenged the description of a reusable token, using the example of one app attempting to access another app's data. The presenters clarified that a reusable **platform-to-IdP session** does not confer cross-app access: an app-specific token cannot simply be used by another app to access the first app's resources. The group also questioned whether the two visible steps—authenticating to the IdP and approving disclosure to the RP—could be expressed more naturally to users. The presenters stressed that the demo's UI was exploratory, not an endorsed final user experience.

### 5.4 Extending the mechanism beyond FedCM

The presenters proposed using the same underlying platform-to-issuer mechanism for related credential flows, including the Digital Credentials API and email verification. They argued that each can, at a broad architectural level, involve an issuer providing a signed statement or credential via a platform mediator. OAuth infrastructure, supplemented where needed by credential-issuance protocols, could support the exchange of different tokens or formats from issuers to the platform and then to the RP.

This **common backend** was presented as a plausible path to reducing duplicated mediation plumbing. It was **not** a decision that FedCM, DC API and email verification share identical trust models or can be reduced to a single token type. The transcript does not establish an agreed mapping of every existing API or protocol to the proposed mechanism.

### 5.5 Application-facing APIs: a separate and less-developed question

The second part of the presentation asked whether today's separate entry points for FedCM, the Digital Credentials API and email verification create unnecessary complexity for RPs. Examples of common journeys included sign-in, sign-up, account recovery, authentication and payments. The speakers identified three classes of problems:

1. **UI intent is inferred from the API used.** A request through FedCM tends to imply sign-in, whereas a Digital Credentials API request tends to imply information disclosure. In practice, the credential type does not always tell the browser the RP's purpose, producing increasingly overlapping UI designs.
2. **Common capabilities are defined in individual APIs.** Examples included representing the verifier/requester consistently, request signing, response encryption, cross-device operations, challenge handling and other features useful beyond one credential type.
3. **Layering and duplicated selection semantics.** Credential-format query languages can express combinations and alternatives among credentials while the platform's Credential Management API may also choose between FedCM, digital credentials or other sources. Likewise FedCM active/passive modes and higher-level mediation parameters may overlap.

The presenters suggested examining whether an application should be able to express **what credential formats or assertions it can accept and for what purpose**, leaving the platform to select an appropriate mediator. They did **not** offer a finished API design or request an immediate normative decision on this frontend unification.

### 5.6 Standardization, deployment and ownership questions

The presentation prompted several substantive questions:

- Which parts already have equivalents in **OAuth or OpenID Connect**, and where would new specifications or extensions be justified?
- What exact endpoints and other changes would existing **IdPs** have to implement, and could migration be incremental?
- Can **RP behavior** remain substantially unchanged, as intended, while platform and IdP interactions change?
- Which capabilities properly belong in **FedCM, DC API, Credential Management, OAuth/OIDF protocols or other standards groups**?
- What limits should apply to platform-held tokens, profile boundaries, consent and cross-app reuse?
- How will the proposal behave across **different browsers, operating systems, identity providers and credential formats**?

An IdP implementer from Shopify expressed interest in reducing user friction but requested a much clearer migration story before assessing the work. Emelia S. offered OAuth expertise and help with possible Internet-Draft work. These were offers to collaborate, not endorsements of a specific standard.

### 5.7 Proposed cross-group task force

Heather proposed convening a **focused cross-area task force** including FedCM, the Digital Credentials API, IdP implementers and relevant OAuth/Credential Management expertise. Its task would be to clarify the architectural proposal, identify specification-level impacts, and formulate precise requests to the responsible working groups instead of allowing overlapping changes to grow independently.

A participant asked that **privacy experts be involved at the beginning**, particularly regarding multiple user profiles, information segmentation, user consent and the potential privacy effects of reuse. The chairs agreed with that approach. **No task-force charter, membership roster, schedule or adopted technical solution was finalized in the meeting.**

## 6. Additional discussion: delegated authority, parental consent and assurance

At the close, a participant working on delegated authority at the OpenID Foundation raised parental consent and verified parental responsibility, including scenarios involving children, high-assurance records and AI agents. Others urged care in distinguishing **age-attribute/age-threshold claims** from **proof of a parental relationship and delegated authority**. Requiring relationship or identity proof in cases that need only an age-threshold assertion could unnecessarily disclose sensitive information.

The chairs emphasized that the Federated Identity Working Group's charter is not intended to define **identity-assurance levels or assessments**. FedCM and the Digital Credentials API may be relevant transport or mediation layers for assertions developed elsewhere, but the group should not take ownership of defining the underlying assurance or delegation policy. The group encouraged finding the appropriate standards venue for the substantive delegated-authority work, while retaining the opportunity for API-level coordination as concrete requirements emerge.

---

## 7. Decisions, conclusions and open questions

### Agreed directions / conclusions reflected in the discussion

- Use the meeting to prioritize **cross-browser support** rather than conduct the originally scheduled general issue/PR review.
- Produce a **checked synthesis** of the previous day's Apple/Mozilla conversation and seek continued engagement before the next TPAC.
- Treat proposed OAuth-based platform mediation as **a promising subject for coordinated exploration**, not as adopted FedCM or DC API architecture.
- Explore a **cross-group task force**, including privacy expertise early, to determine ownership and concrete standards requests.
- Preserve the distinction between **platform session reuse** and **application-specific token issuance/consent** in further design work.
- Allow the chairs to adjust the cadence of subsequent meetings around travel and IETF/OAuth scheduling constraints.

### Not decided

- A minimal mandatory FedCM core, conformance profile or staged adoption roadmap for non-Chromium engines.
- Any commitment from Apple or Mozilla to implement FedCM.
- Publication of FedCM as Candidate Recommendation or advancement of a particular proposal to Stage 3.
- Adoption of the Android/OAuth-based mediation design or a specific new OAuth endpoint.
- Merger or replacement of FedCM, DC API and email-verification entry points.
- Final UI patterns for ambient sign-in, agent sign-in, IdP registration or application consent.
- Ownership of delegated authority, age assurance and parental approval semantics within FedID.

## 8. Action items and follow-up register

| Priority | Proposed action | Owner / participants as stated | Status at close |
|---|---|---|---|
| High | Draft a substantive summary of the TPAC cross-browser conversation, validate it with Apple and Mozilla participants, and arrange another conversation | Heather offered to take the pen and coordinate; Sam and other participants to contribute | Planned |
| High | Convene an exploratory cross-area discussion/task force for OAuth-based platform mediation and credential API unification | Heather offered to coordinate; presenters, FedCM/DC API experts, IdPs, OAuth and CredMan contacts | Proposed |
| High | Include privacy specialists early, addressing profile boundaries, consent and cross-app reuse | Task-force organizers / privacy specialists | Requested and supported |
| High | Identify what existing OAuth/OIDC standards already cover (including display metadata) and which new specifications, if any, are required | Helen, Sam and interested OAuth experts, including Emelia | Open |
| Medium | Clarify IDP migration effort and implementation feasibility with relevant providers, including Shopify, Microsoft and Facebook/Meta representatives | Proposal presenters and willing IdP implementers | Open |
| Medium | Progress Service Worker registration/lifecycle changes needed by Identity Handler and test actual enterprise IdP requirements | Edge/Identity Handler and Service Workers contributors | In progress; timing uncertain |
| Medium | Clarify whether the Identity Handler proposal really supports OAuth DPoP as described, including key ownership and execution context | Identity Handler implementers | Open |
| Medium | Track the discovery / `/.well-known/` deployment problem, creating an issue if needed | Participants in discovery discussion | Issue requested; number unconfirmed |
| Medium | Investigate nested FedCM in brokered IdP scenarios and handle-resolution gaps for open-world federation | Interested LWS/Solid and FedCM contributors | Open |
| Medium | Explore non-normative cross-browser UX guidance without assuming Chrome's design is the universal pattern | Interested WG/CG contributors and browser vendors | Suggested, not assigned |
| Administrative | Share presentation slides for association with the minutes | Presenters; chairs to collect | Requested |
| Administrative | Publish edited meeting notes from the Zoom transcript | Chairs | Planned |
| Administrative | Review future WG/CG meeting dates for conflicts with IETF and OAuth sessions; consider skipping the immediately following week | Chairs | To be scheduled |

## 9. Points to verify before treating these as official minutes

1. **Attendees and speaker names:** The transcription has inconsistent numerical labels, and no independent attendance list was supplied. Most statements are deliberately attributed by role or left unattributed.
2. **Presentation references:** Several diagrams and demonstrations are referenced orally but cannot be reconstructed precisely without slides. They should be linked when received.
3. **Cross-browser debrief:** These notes record participants' interpretations of the previous day's separate conversation, not direct commitments from its absent Apple/Mozilla attendees.
4. **Proposals and maturity:** The stage model, deployment figures and status assessments were presenter descriptions made during the meeting; check proposal repositories for publication-grade or time-sensitive claims.
5. **Scope of the new mediation proposal:** The exact exchange-token design, endpoint naming and relation to existing OAuth/OIDC specifications need review by the presenters before incorporation into technical specifications.

**Source materials:** `2026-10-29-TPAC-FedCM-agenda(1).md` and `transcript-15.txt`, provided for this summary. No external sources or documents were used to infer additional decisions.
