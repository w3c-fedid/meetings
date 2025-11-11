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

Q&A

* Tobias: So what's the secret key for the hmac? The issuer just passes it in the dc API create call right? So the os, the browser, and the OS see it, but then we don't pass it to the wallet. 
* Lee: We get it as a standalone, like at a top-level parameter. We get it, we compute the HMAC and pass it to the wallet. But we don't pass this actual token to the wallet, so the wallet never learns it.
* Tobias: It doesn't learn, correct? 
* Lee So is that known to the browser and the issuer or just to the issue? It's known to the issuer, and it will be known to the browser and the OS, but not to the wallet. And then the issuer can compute this HMAC and compare it as well, right? If it doesn't match the attestation, then they know that a different wallet was picked.
* It sounds like you're trusting the payload, and the HMAC is the browser, because the browser's in the position to know what package is invoked, right? 
* Lee: That doesn't give to the wallet. So there only gives the HMAC to the wallet. The wallet, then sends it to the issuer back end as part of getting the credential. And the issuer backend can recompute this Hmac itself because it knows the expected package name and it knows the secret. So it computes the Hmac. And if they don't match, then they know a wallet man in the middle of it.
* Matt:  Yeah. So this doesn't protect from the malicious browser extension case that Tim's also talking about. Right. As well, you've got Dominic. You're probably right.
* Tim: Don't want to go down a rabbit hole here, but this is yet another reason that if we were to pick the solution to protect Navigator credentials in the browser. I'm all for anything that would lead. This doesn't protect against an extension. Extension can create this HMAC and still man the middle lip. No additional protection. It relies on the browser having integrity of that call.
* Matt: Which an extension breaks that. Well, so here's a question that I have. The HMAC is over the binding key and selected wallet identifier, but if the attacker is using the same wallet as the victim, And figures out some other way to man in the middle things.
* Lee: So if the user picks a good wallet app, then we're all good. The attacker can't use a good wallet app on their phone. It has to have a bad wallet app on the attacked phone and then a good wallet app on the attackers phone.
* Matt: Who is determining which identifiers are good and which are bad?
* Lee: In non-EUDI use cases, every issuer has to keep track of every single wallet identifier. If you allow any wallet, then by definition, you allow the malicious wallet. You could still verify this Hmac to know that it hasn't at least man in the middle. And then just accept the wallet anyway, couldn't you? You could verify that a malicious application isn't in use, because I think that what this does, you could deny list. You could take a deny list approach. Because there's probably gonna be fewer malicious wallets than legitimate wallets.
* Tobias: If you select the good wallet, on the attacker's device, you're assuming basically the DC API can reliably get to that application. We're assuming OS integrity, which would mean you can't steal the payload. The way you're stealing the payload is getting the user to pick the malicious wallet app. And we're saying that you can't steal the payload by the User picking a good wallet app. You could if the OS was compromised. Or they're saying the OS is goodm the phone is not rooted and not compromised. The browser's good, the OS is good. So under that model, the only way you can steal the payload is if you pick a bad wallet.
* Lee: But you have to assume that the origin isn't compromised as well, because if you steal the authorization but come back to the browser before it sends to the DC API, you could take it out of there and then play it on another to the good wallet on another device. It's like you're trying to get your MDL stored on your phone in Google Wallet. I steal the pre auth that and I install it on my phone and Google Wallet. That's the attack we're doing. We're just saying that there's an attack here; a malicious wallet can get it.
* Tobias: Same if you can inject JavaScript like on the origin, it's authenticated the user, right? Because you're already an authenticated state on that page. So if you can still like the cookies for that authenticated page, or you could inject JavaScript into that decay page, you would have the ability to get the pre auth token anytime you can get into that authenticated context. You could get this token, too, and then you could then just inject it into a good wallet. We could protect against that by creating a response in the pre auth that you then send to the server.
* Lee: The good instance of the web session that actually invoked the API, then has to send to the back end in the context of those cookies. Then you could. That's option number one, isn't it? The DC call returns something like I'm a hybrid of your solution. So you use the HMAC solution on the way through, but then if you send a response from the DC API and issuance, that comes from the wallet that's unique to that wallet instance. This is an unrelated threat to what we're discussing anyway, but it is a threat if you compromise an authenticated session and authenticate a TLS session with the browser and steal the auth tokens.
* Lee: If we picked this malicious wallet, what can we do about it? I think three does kind of solve the problem, except that it's a little bit complicated and a bit messy, which is not great. But also it doesn't look over hybrid at all, really. I don't think.
* ??: If you have the browser on the on the phone making the call, you're not going to pick a package; you're going to pick hybrid. So at this point, you can't generate the hmac. You would have to send over the binding to the key over the platform to HMAC and report back.
* ??: But then why do you need a report back? The HMAC computation is done wherever the device is, where the actual wallet applications are installed. So in hybrid, you just kick it one step further.
* Lee: No, not sending it back. Sending it to the client that scans the hybrid code and has a wallet. Maybe this works. I think what you're going to do is you're going to pick the other device, right? You're going to have to send this thing over in the hybrid call. Hybrid can't release it to any wallet, which it wouldn't do. And then on this, on the other phone at the other end, it's going to replay that, create request. The OS could generate their hmac for the wallet that does get picked. Then the platform is taking the place of the browser and the hybrid ceremony. So it has the same security properties, arguably. Which means the binding should be safe. Maybe that works.
* Tobias: Because at the end of the day, even over hybrid, the only thing you have to trust is that transport has kept confidential for that binding key, which means. Which we assume. Right. Still. Yeah. We're assuming that both the devices here are trusted. Because they're both user devices that they control and trust and everything the one way. Okay, so as we're thinking about Hybrid too, we also have to. Do we have to think about the technology powering hybrid, because we're also. Now we're talking about wifi direct, we're talking about ultra wideband.
* Matt: If we assume confidentiality and integrity of the transport technology that hybrid users use to transmit the binding key, I think we're okay because we're still trusting the end device. Even in the cross-device flow lead, to provide the package that we were talking about, the certificate, thumbprint? Like whatever in device where you pick the wallet that's still responsible for providing the origin. The whole point is the wallet that gets picked by the user can't learn this key. They don't learn it as long as the phone they pick does this correctly. As long as it's not the wallet that is like implements hybrid. And then you get the user. The user's phone is good, right? Like, the desktop's good, the phone is good.
* Lee: I think this works. Can anyone think of where it doesn't work? I thought initially it doesn't work because when you pick the package on the source side, You don't have a package to sign, and then you have really no idea where it's going after that. You have no real trust. But this is. There's no signing here. This is just an hmac, over the hmac. You can't do the HMAC on the source device.
* ??: Isn't it the same problem? Because you can't afford the origin on the source device as well, you have to do that on the destination device. The bug we were talking about in Android the other day. You wouldn't have the certificate thumbprint of the install package identifier. 
* Lee: (describing option 4)
* Matt: Are we afraid of digital credentials turning into a one wallet per credential type thing that we've been trying to avoid with WebAuthn because if you allow. If you allow issuers to basically dictate which wallets they'll issue into, would you have a situation like an insurance company requires you to issue to their insurance wallet? Kind of exists with the DCS, though. you can only put your European ID card in certified European wallets. So they already inherently have some allow list. So then this would be, this would be something to help the platform s omit options to users that would automatically fail because the issuer is saying they wouldn't accept that wallet. 
* ??: Standardized PKI than it would be to use things like package names, which are both. No, the package names disappear. It's now just like certs, and you just say, if you route to this cert, you're good. And that's more standardized than, yeah, package names and package certs, all that sort of stuff. 
* Lee: You'd have to standardize this attestation, everything, and, you know, be a whole bunch of work. This is a much bigger thing to solve, but it probably would solve both problems.
* Tim: So I have no issue with the technical solution. I fear the current state of affairs. The optics of the OS enforcement and there being another entity that's not the specific entity will not be good. I think this is a later solution; this seems more like a UX optimization right now.
* Lee: We're just providing a mechanism to enforce this. Users don't get dead ended and click like the wrong apps and then just kind of go, what happened? They can also not use this and still do the attestation check. They'll just get the same behavior as today, right? It just fail later.
* Matt: But it's just a hint. We should call it hint. :-)  And you can be package identifiers.
* Matt: So I think there's a difference between, like, if the wallet cares, it can have it, versus it's always returned whether or not the use case requires it. And so that's another downside of number one. That it would always reply it back and maybe you don't always want to leak it. I'm wondering how the issuer is going to get these selected wallet identifier that it's ultimately issuing to but during issuance.
* Lee: It would be. This would be a value that the issuer would get from the wallet at issuance time to then compute the HMAC and check with what the browser reported. It assumes that the wallet the issue is going to get an attestation. This one would involve VCI to be extended so this HMAC can be provided as part of the asset. It's probably going to be passed along with the attestation, I would say.
* Matt: Does DC API actually get any info about the issuance? Like the wallet that responds to the issuance request? I thought DCAPI was pretty much going to early return.
* Lee: It doesn't today; this is proposal to change that. I don't want to do number one. I'm just saying it's an option. nd it would change the return value of the DC API from what it is today. And it would always leak the reflected wallet. I don't think it's a good option, but it would work.


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

Q&A

* Helen: The DC SPAC requires this user activation, basically, on the browser to trigger this DC API, you need to perform a kind of click before the DC API can go through. Otherwise, the DC API will just silently fail; user activation is required and all the websites cannot call this DC API upon page load.
* Marcos: We wouldn't want to remove it for the high value cases. It's also to prevent annoyance when a site can just pop a thing up. Requesting credentials or issuing credentials and so on. But there is a proposal in WebAuthn called immediate mediation, which could be used for these cases, where you do have these verified credentials, but there are kind of low-value single-use things that you could, in theory, pass along. So that may be an approach in the immediate mediation stuff that is being proposed to Webauthn, and it is basically the use case that you said, where you want to have a login.
* Helen: Chrome and Safari have already relaxed this requirement.
* Lee: Well, I checked with the Chrome folks and they also said this is also what Safari did. Basically, they say you can make a normal passkey GET.
* Matt: I definitely think we should explore the idea of leaning on immediate mediation to make us to allow the API to be more comfortable with certain ways of requesting certain credentials. I would be really surprised if we could get past the privacy group or TAG. I'd be curious to see what they would say about completely silent.
* Lee: It's not silent. It still pops the exact UI up. It does exactly everything you expect. There's no change in ui. 
* Matt: Ys long as there's something that requires the user to interact with it to get a response kind of thing. 
Lee: API still shows the ui. It just means that you can't call the API on page load today. It flies with an error saying user activation required. And that's it. That's the only difference. We're just saying, could we relax that restriction like we're told we did for web authors, but we should confirm.


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
  