# FedID WG Telecon \- DC API Series A, 2025-10-06

* Moderators: Heather

* Scribe: Gemini transcript / Heather to revise

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (10 minutes)  
* DC API Issues & PRs (40 minutes)  
  * [Define interaction between platform credential chooser and the user agent \#306](https://github.com/w3c-fedid/digital-credentials/pull/306)  
  * [Wallet Selection Binding during Issuance \#382](https://github.com/w3c-fedid/digital-credentials/issues/382)  
  * [Relax the User Activation Requirement \#377](https://github.com/w3c-fedid/digital-credentials/issues/377)  
  * [Is a registry needed? \#345](https://github.com/w3c-fedid/digital-credentials/issues/345)  
* Any Other Business (AOB)  
  * [Preventing Abuse of Digital Credentials](https://w3ctag.github.io/prevent-credential-abuse/) \- Draft TAG finding  
  * TPAC Agenda Building  
    * [Breakout Sessions](https://github.com/w3c/tpac2025-breakouts/issues) due by 22 October

# Notes

### Ecosystem Updates (10 minutes)

* Mohammed: Chrome warning interstitials for custom schemes  
  * Chrome is implementing transparency and control for users regarding identity usage online  
  * Warns when government credentials are likely being used on websites  
  * Digital Credentials API allows the browser to reason about risk levels  
  * Custom schemes don’t provide the same risk assessment properties  
  * Expected outcome: encouragement toward DC API adoption, though not the primary motivation  
* Rick: Primary goal is user transparency and control over privacy trade-offs

## DC API Issues

### [Define interaction between platform credential chooser and the user agent \#306](https://github.com/w3c-fedid/digital-credentials/pull/306)

* Heather: Marcus blocked on feedback for this issue; requires input from Mohammed and others  
* Mohammed: Feedback provided on PR today  
* Tim: Will approve once Mohammed signs off

### [Wallet Selection Binding during Issuance \#382](https://github.com/w3c-fedid/digital-credentials/issues/382)

Lee: This is a critical security issue with real government issuer concerns. Attack scenario:

* User has legitimate phone but installs malicious wallet app  
* Malicious wallet takes pre-authorization code, forwards to attacker-controlled device  
* Code injected into legitimate wallet (e.g., Google Wallet) on attacker’s device  
* Results in credential issued to trusted wallet but on attacker-controlled device

Lee: Four proposed solutions:

* DC create call returns package name of selected wallet  
  * Awkward due to asynchronous issuance  
  * Privacy concerns always returning wallet info  
  * Exposes OS internals to web  
* Issuer provides allowlist of native wallet package names  
  * Leads to fragmentation and allowlist maintenance issues  
  * Doesn’t scale with certification bodies  
* Binding key approach (preferred option)  
  * Issuer adds random binding key parameter to DC API call  
  * OS generates HMAC of key \+ selected wallet package ID  
  * Wallet sends HMAC to issuer with attestation  
  * Issuer verifies HMAC matches expected wallet  
  * Works for Hybrid flows  
  * Doesn’t pre-filter wallets but catches attacks post-selection  
* PKI-based allowlist using root certificates  
  * More standardized than option 2 but complex implementation

Strong support for option 3 (binding key approach)

* Consistent with trust framework approach on presentation side  
* Leaves trust decisions to protocol layer rather than API specification

Rick: Three seems like it has a better properties the way you've presented this lately and I think I agree. But I just want to challenge my own thinking here. To decide if they trust this wallet implementation. Right? But it might not just be a list of package names, it could just be that. It could be the root cert of the attestation, like who's signing the attestation. So it could just be like, the attestation is signed by the EU, so I trust it. It is not necessarily a hard-coded list of package names.  
So maybe there's similarity here with the design. Think of the design principles of the DC API, right? A bunch of the Trust framework is considered above isn't part of the DC API itself; it's considered part of the protocol level. And so it feels like maybe the key difference between two and three is that two is maybe a layer violation in the sense that we're asking for some of the wallet issuer trust information to somehow be standardized in our spec. 

Lee: Correct. Or 3 gives us a way of letting that be plumbed through, consistent with how we're approaching trust from an RP perspective as well, and saying that it's solved by the underlying layer and whatever mechanism it wants to use. Sometimes that'll be a package whitelist, sometimes it'll be a PKI system, whatever. I like three a lot better because I think it's consistent with how we're thinking about the trust framework on the presentation side as well. Both two and four try and make it forces us to make some decisions about the trust framework. Either we make it, we force it to package names, or we force it to PKI. And three leaves this agnostic to both of it. We just leave it to the upper layer, basically.

Matt: Two quick questions \- Option 3 the last sentence of it this doesn't really work for Hybrid, though. When we talked about it last Wednesday, didn't we have an idea that this may work with Hybrid because the platform, as the recipient of the Hybrid or as the negotiator of the Hybrid ceremony on the mobile device. Would be in a position to know the secret value and still not pass it through to the wallet.

Lee:  I think on the last call we did decide it probably does work for Hybrid. I need to think about it a little bit more. Take the bug to say that, but I think probably 95% sure it probably does work. Hybrid now.

Matt: I was thinking about it as potentially a privacy violation there if a wallet identifier is somehow factored into things. But the bigger question I think might be like if the issuer, if the HMAC is computed over the selected wallet identifier, is there any opportunity for the wallet. To misrepresent itself to the issuer such that it might still satisfy. You could hash the same value when the issuer and the wallet are talking. Is there an attack vector there by using selected Wallet identifier, if that's something just associated with an app. Could a malicious app still be present in a good wallet? I don't think so, because this is generated by the OS, right? The OS is reading the selected packaging, creating this hmac. In this case, they have to forward it to attack this wallet so they could afforded the pre auth code and they could forward this HMAC generate Hmac. So now they're going to say on Google Wallet but the HMAC is going to say on bad wallet and they'll fail. They will match.

Tim: I think the fact that it doesn't help with the upfront selection is okay, because  we don't have that for anything else, right? I think that is. Yes, it's a downside, but also I don't think it should be in scope for the solve it. If we had solved it, great. But it doesn't matter so much. It's more of a nice to have.

Wendy:I think this is very interesting to read the threat and if you substitute for malicious wallet, a user selected wallet that does things differently from what other parties to the conversation might like. It's going to be important for us in describing all of this, to make sure we lay out who the parties to the interaction are. And what control they do and don't have. And this is taking away some powers from the user that we may all agree. The user doesn't get to have those powers because they don't get to choose unrestrictedly into what wallet the credential is issued; it should be clearly spelled out.

Tim: I agree with Wendy. We have to make sure we can explain this well, but it doesn't actually change anything because there's no expectation that the response or any of that is handled yet today. It is always the wallet directly to the issuer. So I think it's terminology and we will need explanations. These are all DRM-related things, right? Like what you've seen with passkeys and credentials.

### [Relax the User Activation Requirement \#377](https://github.com/w3c-fedid/digital-credentials/issues/377)

Helen: Current requirement: user must click before DC API can be triggered, but that’s a problem because it creates UX friction in legitimate flows such as Two-factor authentication scenarios, Post-login credential verification, and Payment authentication flows. WebAuthn has set a precedent by relaxing requirements, with some rate limiting. 

Matt: I think I suspect us trying to reach parity with web authentic behavior in terms of how freely the API can be called is probably not a good direction for us to aim for because the use cases like passkeys are so tailor made for a single specific use case that has an authentication flow. We've taken some liberties collectively as an ecosystem over the years to sort of streamline that. But credential presentation necessarily has a much wider range of possibilities of what you're aiming to achieve by asking for credential presentation. I wonder if we wouldn't just. I wonder if we wouldn't just run into too many, we would end up spinning our wheels so much on the user privacy question as a result of that, if we tried to make it like too permissive on when to call it. I want to also plus one what Lee was saying about doing this on page load, I don't think is a good way to do it. Not only because on certain form factors, the system prompt, the platform prompt could hide most of the page UI explaining why you're being requested to ask for driver's license or whatever. You know, there's just very real UX challenges in that pattern as well, where like modals are not going to give users a chance to read what's behind it to explain what's going on. So I do think there would need to be some sort of middle ground between the permissiveness of WebAuthn and require a click every time.  There's got to be possibilities where, as long as the user has interacted with the page in some way, then surely you can be a little bit more permissive where you're clicking, like log in and then recover your account or whatever, and then that pop up. The user is interacted and engaged with the page in some way. The only thing I might offer is I wonder, say out loud to see if anybody this resonates with anyone else. Part of the problem. I think if I remember correctly, part of the reason why Webauthn the requirements on requiring user interaction were loosened, or rather one of the pain points felt, was that it was difficult to understand when a browser slash platform is going to require that user gesture. And, you know, whatever the solution we had we got rate limiting or whatever to simplify that. If we were going to go this direction with DC API as well, could we define its operation in a way that when a user gesture was required because, for example, the user didn't trigger a hard page navigation or whatever, we could return an error that goes user generate your user gesture required, which would then allow the RP to, you know, wire up an actual button that you then click because the conditions hadn't been satisfied. 

Tim: given the wild direction this issue went very quickly, we should close this issue and create a new one explicitly for really, the title that I put in chat.

Ryan: We've been looking at payment pass keys, and so there are scenarios where, like, we wanted to replace passkeys with, you know, digital payment credentials. And so we have scenarios where we want to get to a first party context. And then invoke the passkey, we may want to do the same thing. With digital payment credential. So we may need a first party context before we invoke the digital credentials API. And then that would mean we have to stop and ask the user to click again. So it's likely. You can imagine checkout scenario on the merchant page. I click, you know, authenticate button, you open up a brand new window and then we would today immediately go past key authentication after going and looking things in local storage or cookies or whatever. Right. If we do this with digital credentials, we're gonna have to stop and say, oh, no. Please click here. To use your digital connection where we didn't have to with a passkey.

Heather: Group consensus to for the chairs to close current issue and Helen to create new one focusing on  “post-navigation page load” scenarios, not general page load from address bar or search. Same-site navigation only as potential middle ground. 

Helen: That totally makes sense, right? Don't think when we raise this, we had to achieve feature parity, right? But sounds like we are kind of on the sort of consensus that page load is a bit too aggressive, which makes sense. And we are fine like just enabling all this use cases where it's mostly just.

Marian: that's exactly the point. I wanted to talk about a bit because doing this for like your full driver's license makes me a bit nervous because it's such a sensitive thing to share and I can imagine all sorts of abuse cases where sites use these Post navigation things to get you into a situation where this suddenly pops on you and you have no idea what's going on. Right. And unfortunately, I'm not sure how helpful the UI that we have today is going to be in those cases. Right. I think one of the principles for how we think about this in Chrome is that we want to encourage sites to provide ample context for people for why this is happening, and allowing them to do this without user interaction seems to be a signal in the wrong direction, at least for some of the more sensitive credentials that go over this API. So I would feel a lot more comfortable with this if this was scoped to granular have a much lower privacy risk.

Rick: With push permissions I think is a good example. And camera and geolocation are all in this place. I'm also open to the idea that maybe there are certain flows that should be different than the normal governor credential flows. But yeah, it seems problematic to me given all of the concern. Right? I mean think of what we're going to write in our privacy consideration section. Is that needs the API doesn't have to get the purpose, for example, because we expect sites to get the purpose. Before invoking the DC API to explain the purpose before exposing the DC API. But then how would that be consistent with an API that can be invoked without the web page showing these or anything before the API is invoked? That makes sense.

Tim: Would be its Post navigation Same site only. Which would address all of, I think the phone number use cases, most of the step up type things. Generally you're taking someone to subdomain like verify, but it would break the crossing to first party for payments. But that would, I think, help a little bit with some of the concerns. It's better than I think it's better than not. But maybe we should start aggregating those. On the new issue is like, what is the positives and minus, pluses and minuses of each of those. Because. Maybe the payments thing could be an iframe, right? Maybe. And what restrictions are on an iframe? And we've had the same conversation around user activation and iframe. So anyway, it might be interesting to look at that because I believe actually someone else commented on the issue saying, what if it was same site.

Mohammed: I'm a bit confused about like Marion’s and Rick's comments like are we assuming good intent from websites or not? Because if you assume good intent, then before navigation they would show the context and the purpose and like meaningful use interaction.And if they don't, we can trick the user into clicking any button that say click here to do whatever, and then the invoke the API. Malicious website can find a way with even with user activation requirement to trick the user into click button here. Like, scroll down to read the list. Like, I mean, you know, so I don't think that it will fix it. Like, I see that the risk. I agree But for that. But I don't think huge acceleration by itself. Will help that much here.

Helen: Well, I think I'll definitely create the new issue. It would be nice if we could allow all the. Maybe we'll keep discussing it Sounds like there are still question around how much relaxation we allow. The degree of that. So reckon we can keep discussing those. I don't think it provides a huge amount of protection, but it might actually hurt legitimate websites doing legitimate things. So I'm not really protecting against malicious websites doing anything. But I do kind of buy also what everyone's saying. So why don't we capture this in the issue? We can create a new issue, too. I think the other one went off track a bit, so maybe we should create a new one with Tim's framing.

Rick: Let’s include info on PEPC ([https://github.com/WICG/PEPC/blob/main/explainer.md](https://github.com/WICG/PEPC/blob/main/explainer.md)) and info related to frames capability delegation [https://github.com/WICG/capability-delegation](https://github.com/WICG/capability-delegation) in the new issue.

### [Is a registry needed? \#345](https://github.com/w3c-fedid/digital-credentials/issues/345)

Heather: This remains open until we figure out how to resolve the question. Does the draft TAG finding on Preventing Abuse of Digital Credentials give us any new information that would help us come to a resolution on this one way or the other?

## Any Other Business (AOB)

### [Preventing Abuse of Digital Credentials](https://w3ctag.github.io/prevent-credential-abuse/) \- Draft TAG finding

Rick: Related Martin's comments here (for Mozilla not TAG) [https://github.com/mozilla/standards-positions/issues/1003\#issuecomment-3212917334](https://github.com/mozilla/standards-positions/issues/1003#issuecomment-3212917334)

Lee: Is there anything that we're doing that would conflict with this?

Heather: Chair hat off: My interpretation of reading this was that the W3C's advisory group really wanted to think about what the W3C specs can control, can be responsible for, can influence. And in several of our cases with the DC API, we've said things like, this isn't our problem because this is something that VCI should handle or the wallet should handle. And my reading of that finding was that the TAG isn't going to accept that because there's a certain expectation of. Well, no, you can't trust the other things to be behaving in a constrained enough manner. Therefore, we're going to have to do something.

Wendy: That may be what they are saying. It might also be read as if you're not taking account of that. You need to explain very clearly why not? And so make sure that someone taking responsibility. Or you can point to where the responsibility is taken, not just a passive voice. Something bad was done. And none of us can do anything about it. So I think it's a reinforcing to us that the concerns that have raised been raised by objectors and the concerns that some of our participants have been raising, that there be dragons here, these are potentially dangerous interactions. And it's important to the health of the web and its users that we know who's responsible for helping the user to protect themselves at each sTAGe.

Lee: I was going to say something like kind of a similar. I think it highlights all the issues that we should be aware of. However, upon reviewing them, I believe that each one of them, we are aware of these issues and have attempted to address them in some way. Or at least we sort of acknowledge each one of these things. We've discussed each one of these things, and I think we have answers to how our API attempts to address them. Is there anything in it that seems like what we're doing as at odds with these guidance? I think we agree almost with everything or probably everything in this document. Right. And I think we've tried to do things in a way that addresses these things. May not all be like the web browser does all of this. Maybe some it's the wallet or the certifications, like eIDAS and all these type of things at different levels of all this stuff. But I would say that I would hope that we'd at least have some answers to these things. So I guess my question is, do we have to do anything here like this? Is there anything in here that would tangibly change what this working group does, that we have to change the stack or change the wording?

Wendy: Procedurally, the TAG is responsible for the W3C's architecture reviews, and so we can expect that they will be looking at the spec. From the perspective expressed in their findings and if they find it inconsistent, they will push back on pieces of our work. It's another place for us to have dialogue with them about we are consistent with what you see as the architecture of the Web. And how we work together to make sure that our API is meeting concerns expressed here.

Matt: Also another way to engage with the folks who have not explicitly been participating in this work, but are represented among the TAG are important and constituents of what we're doing.

Matt: I have a procedural question. Suppose TAG seems takes the position that digital credential presentation on the web is bad because it limits user mobility on the web, basically. Objectively speaking, like, yes, that's true, but also DC API is trying to make it not so bad because there are outside forces that are forcing companies hands to implement this stuff. And you can do a custom schemes or you can do DC API and like I wonder if the TAG is allowed to take a nuanced position like that. Something along the lines of yes, we don't like DC API. We think it's bad because it's going to turn everything into ‘show us your government ID to access this website.’ We all collectively think that that's awful. But it can be even worse if it's custom schemes. So I wonder if the TAG is allowed to take that nuanced position or if they have to be like, entirely 100% idealistic according to the W3C's which it seems like this document has been drafted for and isn't really allowed to consider an alternative viewpoint like that. Also, I wanted to ask, when TAG puts out stuff like this, is there ever like an outcome where the API can no longer be worked on in W3C because it's so goes against the organization's mandates for browser API design? Something like that seems like a nuclear option, but if it ever happened. But is that something that could happen such that Fed ID is no longer allowed to work on DC API and we have to go find another home for it?

Heather: Okay, that is a nuclear option. I don't think we are going to get there from here. I will note that this is. While the TAG participants think is mostly finished, it is still considered a draft, so you should comment on it. [https://github.com/w3ctag/prevent-credential-abuse/](https://github.com/w3ctag/prevent-credential-abuse/) 

Lee:  I think it's either we go through this document and we try and figure out and predict if it's going to, if, if our current spec is problematic and we're going to hit some problems down the line. Or can we flip it around and say to the tag folks given this document, Do you have any problems that you're going to raise with our API, Right. And then they could just come here and tell us, and then we could, we could have the debate, because otherwise we're just sort of predicting if we might not. If they might not agree with what we like. Maybe something we can do at TPAC

### TPAC Planning

Heather: make sure to submit for [Breakout Sessions](https://github.com/w3c/tpac2025-breakouts/issues) by 22 October

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* David Waite (Ping Identity)  
* Matthew Miller (Cisco)  
* Wendy Seltzer   
* Tim Cappalli (Okta)  
* Rick Byers (Google, Chrome)  
* Lee Campbell (Google, Android)  
* Helen Qin (Google, Android)  
* Henna Kapur (Visa)  
* Simone Onofri (W3C)  
* Mohamed Amir Yosef (Google, Chrome)  
* Bjorn Hjelm (Yubico)  
* George Fletcher  
* Marian Harbach (Google, Chrome)  
* Ryan Watkins (Mastercard)  
* Suresh Potti (Microsoft)  
* Tejas Dhagawkar  
* Brian Campbell (Ping Identity)