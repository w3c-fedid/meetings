# FedID WG Telecon — DC API Series A, 2026-08-10

* Moderators: Heather

* Scribe: Matt

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)? [Matthew Miller](mailto:mattmil3@cisco.com)  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (10 minutes)  
* DC API Issues & PRs (45 minutes)  
  * [Add requestOrigin attribute to DigitalCredential \#567](https://github.com/w3c-fedid/digital-credentials/pull/567)  
  * [Classify validation failures into specific exception types \#515](https://github.com/w3c-fedid/digital-credentials/pull/515)  
  * [Add document origin to request context \#512](https://github.com/w3c-fedid/digital-credentials/pull/512)  
  * [Require support for both mdoc and signed OpenID4VP protocols \#454](https://github.com/w3c-fedid/digital-credentials/pull/454)  
* Any Other Business (AOB)

# Notes

### Ecosystem Updates (10 minutes)

Lee: Android launched verified email as a digital credential. Also available on the web. So now Android has verified phone number and verified email as VCs. Developer doc: [https://developer.android.com/identity/digital-credentials/email-verification](https://developer.android.com/identity/digital-credentials/email-verification) 

## DC API Issues & PRs (45 minutes)

Heather: many of these were discussed last call, with the outcome, think more: [https://github.com/w3c-fedid/meetings/blob/main/2026/2026-08-05-DCAPI-B-notes.md](https://github.com/w3c-fedid/meetings/blob/main/2026/2026-08-05-DCAPI-B-notes.md) 

### [Add requestOrigin attribute to DigitalCredential \#567](https://github.com/w3c-fedid/digital-credentials/pull/567)

* Matt: What stumped me last call is that this request origin wouldn’t be protected in any way, so don’t see why we would add it unless we added encryption/signing to the call itself and not just the data. Even the instructions in the PR are to not trust the value. As proposed, I don’t think the PR goes far enough to justify this as a feature.   
* Tim: Two things to think about: where the origin gets passed to the platform, so this could get serialized into what gets passed to the platform. We have a new protocol that can sign over the origin. We should tackle this more holistically, with something like clientDataJSON.  
* Lee: I agree, let’s do client data. We could add it to the protocols. It would allow the clients to do anything they want with it. topOrigin, calling origin, anything else; it can grow. I think we’ll get some pushback from folks who think the session transcript can be constructed without client input; you should only use shared information to independently create it. But don’t worry about it; it’s what we do in WebAuthn, and it’s not the end of the world.  
* Matt: \+1 to client data/JSON thing. This feels like the beginning of that. If it’s not a huge obstacle, we should push for this. See the old [PR 95](https://github.com/w3c-fedid/digital-credentials/issues/95).   
* Tim: There was heavy consensus on this two years ago aside from a *very small* minority of the group.  
* Heather: Do we follow the path of either 95 or 567?  
* Matt:   
* Lee: You could just use client data instead of Marcos’ proposal. You could get the origin from there.   
* Matt: Then client data JSON would be a feature only of the harmonized protocol  
* Tim: Two uses, one to provide context, and the other to sign over. e.g., the platform or CM wants to show the origin.  
* Lee: The CM doesn’t necessarily see client data. On Android, CMs only get the hash. Native apps just create the client data themselves. Android would have to change the AP to pass the origin as a top-level parameter.  
* Tim: So let’s think about copying WebAuthn directly, or evolving it for DC API. There might have been some debate on the utility of arbitrary JSON data when CBOR encoding is in play.  
* Heather: Let’s tag [PR 95](https://github.com/w3c-fedid/digital-credentials/issues/95) back on the agenda to revisit next week.  
* Tim: With the caveat that some of the stuff in there won’t be up to date.  
* Mohamed: To confirm understanding, origin would remain a top level value, and then client data?  
* Lee: No, origin would go into client data. There’s no backwards compatibility, the existing protocols continue to work as-is. It’s only a problem when you go to use the client data hash in those protocols. The harmonized protocol can use the hash as the ideal behavior.

### [Classify validation failures into specific exception types \#515](https://github.com/w3c-fedid/digital-credentials/pull/515)

* Tim: I think all of my feedback was addressed. Need to review.  
* Matt: As far as client errors go, these are probably fine for verifiers that will be using this to understand why it failed. As long as the user agent and platform allow it through, the rest of the errors come through the protocol response, this is probably all we can do with errors. 

### [Add document origin to request context \#512](https://github.com/w3c-fedid/digital-credentials/pull/512)

* Heather: Doesn’t seem to have been a lot discussion on this.  
* Tim: This seems fine at a glance.  
* Matt: This won’t turn into the user agent providing another value that isn’t protected from spoofing?  
* Tim: Looks like a better way to provide existing values.

### [Require support for both mdoc and signed OpenID4VP protocols \#454](https://github.com/w3c-fedid/digital-credentials/pull/454)

* Matt: Is there a way to fix the diff? The entire doc is deleted and then restored, which makes it hard to review.   
* Ted: This is happening in a lot of groups I’m involved in, looking like line endings being changed from CR to CR/LF.   
* Matt: We probably have an actual issue this is more about. This topic makes me want to ask, now that we’re mandating response encryption, we have to also require request signing. The signing of the request is what protects the encryption values.  
* Lee: If you accept self-signing, it’s irrelevant and provides no protection. We do not need to mandate signed requests.   
* Matt: I don’t disagree that is snowballing into a super-complex API to use, but this would require the verifier to have a protocol-level understanding of how the keys are used to protect encryption without signing. If signing the request would devolve into self-signing, where is the protection?  
* Lee: If we have client data, that will help. You can put the public key you used for encryption there. IF the browser generates the client data, it’s awkward, but if you can sign over the key the wallet used, the RP can detect if the key was switched on them. The credential format would have to put the session key in the format; not all do.   
* Matt: It feels like there are a lot of attack scenarios still possible here. But request signing isn’t going to solve most of them.  
* Tim: There’s been conversation recently about making mdoc optional since it’s not a free spec. I would support that.  
* Heather: Did that come up? I don’t see it in the notes.  
* Wendy: That did not come up in the last call.  
* Tim: Looks like the original comment was in February that Brian commented on.  
* Brian: I think that would be a good direction to go.  
* Tim: That would line up with the formal objection. Verifiers that buy the spec can implement it.  
* Brian: I think those decisions were made by in-market players who could push for those decisions. But I think making mdoc optional instead of mandating it acknowledges the reality that mdoc isn’t free and frees up spec writers to continue referencing freely available specs.  
* Lee: It helps with layering. We have two, soon three protocols. Wallets are mandated to implement all of them, but verifiers can pick which ones they want to support. Verifiers can signal   
* Matt: It is interesting thinking that wallets have to implement all the protocols, but RPs don’t.  
* Lee: Only for EU certified wallets; they, by law, have to do that. No one else has to.  
* Matt: I think that’s still a sizeable number of DC API deployments that would give us information on what protocols verifiers want to use.   
* Lee: We have data on Android where we support both; most are OpenID4VP. Verified phone, verified email, mDL, the vast majority of VCs on Android are presented through OID4VP. Japan uses Annex C exclusively.  
* Heather: Chair hat off. I think Australia is Annex C only?  
* Lee: In our data we don’t see any Annex C usage above being noise in the data. They might on Apple platforms. But in places where wallets support both there’s very little reason not to support VP. The only reason to support Annex C would be to support Apple platforms. As a verifier, there’s very little reason to use Annex C unless it’s mandated.  
* Heather: Second question: given that there’s work on the harmonized protocol, would we want to say that OID4VP is required, Annex C is optional, but then switch that around to make the harmonized protocol required and the rest optional?  
* Lee: I think there’s three levels: the browser, which DC API cover, the platforms, and the wallets. I think for the browsers it makes sense to pass through everything. It’s a fragmenting force to not do that. I’d say pass through everything. If we want to do what Brian says, make Annex C optional, it’s likely that verifiers would probably make both requests. But DC API would offer a signal that it’s preferable to use VP.  
* Christian: I agree that passing everything through especially for cross-device is the way to go. There are signs of Apple starting to implement VP support in WebKit.  
* Matt: This only requires signed OpenID4VP protocols?  
* Lee: We would need to require all.  
* Christian: The "openid4vp-v1-unsigned" protocol is added once its DCQL request parsing lands.  
* Matt: This PR specifically says, “signed OID4VP.” What about unsigned OID4VP? If we accept that signed requests are not mandatory then we don’t need to have carve outs for signed vs unsigned OID4VP.  
* Tim: The way we did the protocols, the identifiers are types.   
* Brian: I think Matt’s asking why we’re only mandating changes to signed OID4VP.  
* Mohamed: I agree with Matt, we have the four protocols we say we support, it doesn’t make sense to only mandate support of the signed versions of OID4VP.  
* Heather: So it sounds like we need to continue to review 454\.  
* Tim: What was our opinion on the first part, Annex C being optional?  
* Heather: Anyone object? …Hearing none, we’ll bring this to Series B call. The Series A group didn’t have any problems with that.

## Any Other Business (AOB)

* 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Matthew Miller (Cisco)   
* Sami Tikkala / Visa  
* George Fletcher (Practical Identity LLC)  
* Wendy Seltzer (co-chair)  
* Ryan Watkins (Mastercard)  
* Marie Jordan (Visa)  
* Mohamed Amir Yosef (Google Chrome)  
* Lee Campbell (Google Android)  
* Helen Qin (Google Android)  
* Tim Cappalli (Okta)  
* René Léveillé (1Password)  
* Brian Campbell  
* 

