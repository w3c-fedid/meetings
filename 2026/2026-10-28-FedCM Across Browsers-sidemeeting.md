# **FedCM Across Browsers: What Would It Take?**

## Status of FedCM

Chair Slides: [FedCM Across Browsers: What Would It Take?](https://docs.google.com/presentation/d/1DF8Hs28cISsHWkVtYgguP-sfxsdgpLgx_XBKYMcfgHw/edit?slide=id.p#slide=id.p)

Sam: FedCM is currently shipped in Chromium and is being used by Chrome and Edge. Firefox had an early implementation but has paused the implementation. Safari has never implemented.  For Identity Providers who have deployed this: Google, Facebook, Shopify, Microsoft is working on adding features to Edge to support their identity servicesi. Some search engines and IdPs in Japan, Times of India. From a social login perspective, we’ve mostly saturated the market. From a website perspective, accounts for about 300-400k websites calling the API. From the user’s perspective, federation is about half of how users are logging into websites. (The other half are using username/password.) Might be overcounting that since this includes OAuth. Passkeys are eating into the password pie, but not the federation pie. For social login, we’re extending FedCM n various ways, email verification most notably is being done as an extension of FedCM. There are a lot more email providers than identity providers. Working with atproto community. More forward-looking, so not production use.

Sam Goto: FedCM requires a lot of entities to change. Users, websites, browser vendors. Implemented in Chromium. Chrome and Edge ship it. I don't believe Brave or other Chromium browsers ship it. Firefox had an early implementation a few years ago, has since paused. Safari has never implemented. Identity providers: Google, Facebook, Shopify, Microsoft (Edge is working towards implementing what Microsoft needs, hasn't implemented yet). Email providers, some search engines.

Yi: Some IDPs in Japan. Gaming.

Sam: Times of India too. From a social login perspective (buttons you see on websites), we think we've saturated the market. Twitter's missing. From a website's perspective, it's north of 3-400k websites calling the API. From users' perspective: federation is about half of the login events we see. Might be an overcount, as it's more broadly OAuth rather than pure federation, so take as an approximation. Passkeys are eating into the password pie, but not the federation pie. This seems true for head and torso sites.

...: Extending FedCM in interesting ways. Email verification, for instance. Lots more email providers than social login providers out there in the world.

...: Actively working with decentralized social networks, atproto, etc. Forward-looking, not production traffic yet.

## Questions and discussions?

Wilander: Original FedCM proposal had a privacy benefit: IDP didn't learn about the RP. Along the way that was removed. I was excited about that aspect of the original proposal. Could we bring that back? As optional? Some redline saying folks won't use the API without that information. Also, single sign-out? I don't think that should be a think with federated sign-in, but maybe it is a thing? IMO, logging out of the IDP shouldn't log you out of sites using it.

Sam: Good question, easy answer: we're all excited about that variation. We've implemented it in Chrome, you can flip a flag. Delegation oriented variation of FedCM: has the property that it doesn't tell the IDP the specific RP you're logging into. Not resilient to collusion between the IDP and RP, would require zero-knowledge proofs, but it does make it possible to log into a website with a Google account without telling Google that you're logging into a specific site. Has really good properties, UX is more or less indistinguishable from the regular version. I think we know how to solve the incentives for IDPs. Having Safari only implement that variant could create incentives. Chrome, supporting both, could still steer users in that direction.

...: We haven't heard pushback from folks telling us not to pursue that direction.

...: I've heard requirements for knowing the RP and signing users out in the Enterprise case: you're signed out of your work account, you shouldn't have access to the enterprise services.

Heather: Also education. Security properties associated with knowing the RP is a specific location/

Sam Goto: One more note: EVP works exactly like this. Today, verifying an email address in Chrome does not reveal the website to the email provider. Blindness is less compelling for email, as RP is going to send you emails, but the protocol remains blinded.

MT: Three-party credential model: Meta was very clear that they want to know where the credentials are being used. That's one reason we ended up in this situation. Helpful to report to users where credentials are being used, allows revocation. Also: these are identifiable credentials. If the RP and IDP are willing to talk to each other, they'll have a shared understanding of your identity.

Sam: Social login is different than email. Different norms.

MT: Linkability is out of your hands once you've used FedCM or email verification.

Sam: Should be explicit that we're not resilient to collusion, but still value in not requiring unblinded.

MT: May be compelling to note that the delegated version doesn't require the IDP to be online when you sign in.

Sam Goto: I got similar feedback from Facebook (Brad Hill). But as of the last year, things seem to have changed at Facebook, as they now expose themselves as a FedCM provider. I don't think they're opposed to it. Browser UI can steer the user towards less scary options. Safari could just implement the delegated version, etc. I don't believe there's opposition from social login providers (for the consumer market).

Wilander: I think I draw the line at the browser helping with cross-site identification. Collusion is on the RP/IDP, not the browser.

MT: Yup.

Sam Goto: There is a ZKP construction that could deny linkability. Social login is less useful: often giving name and email address, but just wanted to raise the ZKP variation that might be possible. One step past the delegated model.

MT: Not sure that makes sense in this context. One of the things that concerns us most is that FedCM started with a modest core and then grew and grew and grew. We found our implementation was chasing a spec that never stopped growing. Then 3PCD rolled up, circumstances changed, and we reevaluated and found we couldn't ship, couldn't close the gap. Resourcing issue. Would be ideal to identify the kernel of the thing, perhaps that's the delegated model. If we can agree on that: super, super lightweight FedCM could be more realistic to ship.

Sam Goto: Curious to hear from you about the open world in which you allow anyone to bring an IDP to the system. Is that an important part of the thing? How do you reconcile that with growth.

MT: Multiple IDPs, perhaps willing to participate with any comer. We're kinda enthusiastic about that notion. FedCM had some opportunity to deal with the NASCAR issue, we've talked about that alot. A model in which websites give you a credential, perhaps with rules about where they expect it to be used, maybe we pay attention to those: if websites accept credentuals from anyone, that's a UX problem, not an API problem. Can't be open season for some sites, some constraints might be necessary or desirable for RPs, but many sites would accept credentials from a larger set of providers than they currently do because of screen real estate problems. Pushing that UX to the browser, showing only those the user has, could be valuable. That angle is worth exploring.

Emelia: Question on delegation. I don't think you can actually do this correctly in many setups, because many setups require the IDP to know the RP in order to assert something about the client ID. IDP needs to be able to revoke credentials.

Tim/MT: That's what you lose in this model.

MT: You break the dependency on the IDP.

Emelia: You use the trust/safety around that as well. A malicious individual can use your identity, and and the IDP can't help with that to keep you safe.

MT: Yes, that is correct. But there are many bad websites, and you give them your email address. This is not fundamentally different.

Emelia: Is this a good idea? Has T\&S implications, revocation, visibility?

MT: Presumes the IDP needs to be responsible for this. Pretty strong claim. We shy away from "I can't protect you if I don't know what you do." claims.

Emelia: Worth digging into more.

Tim: Delegated FedCM pushes T\&S concerns to passkeys, which is good.

Sam/MT: Thumbs up.

Tim: Folks who want IDP protection can still do that through traditional federation.

Sam: Useful for account creation, but not sign-in/returning.

MT: We have passkeys now.

Emelia: Why do you need to involve the IDP in these cases? If you don't care about the email, IDP, APIs associated with it?

Tim: The line blurs with email verification. Most accounts need to communicate with you, and want a name. Most people click sign in with google because they don't have to type anything.

Emelia: Doesn't autofill solve this?

Tim: Still need to click, roundtrip the email, roundtrip the phone.

Emelia: EVP?

Sam: Need to convince users. EVP catches \~50% of users, but 50% clicking on buttons.

Tim: Google's one of the only entities that's both email and IDP. User agent should help user reason though this, and pick the best path.

Heather: Bringing back to scope of getting FedCM in browsers.

???: Use cases where verifying email is verifying for more than one point in time. Just proving that at one point in time you have access to an email, then you get a long-lived passkey?

Sam: Let's make sure we let Safari and Firefox talk.

Wilander: Very interested in opt-out signals. Chrome has something in settings to opt-out of federated logins. Signals in some way to IDPs that user doesn't want this. I don't think we want a global setting, but let users say "I don't want to sign in with this IDP." Don't want a fingerprinting vector, should only be visible to the IDP, maybe as one bit in a cross-origin iframe.

Sam: I agree with your problem statement.

Tim: What is the statement?

Sam: paraphrasing: we call this "intrusion" in Chrome. when you go to a website, a million things pop up in front of you. Part of the problem has been caused by Sign-In with Google. It's very intrusive.

MT: It gets results.

Sam: It does. Still, agree with the problem. When you land on a website, popups are prevalant. Opting out of SiwG is can be helpful.

Wilander: Yes, and I want that to be read-only to that IDP.

Sam: The setting isn't framed that way, but I think if users actively click on such a button we'd allow the sign-in, but we'd suppress the pop up in front of the user,

Wilander: Sure, if users favor a given provider, we should show it, and maybe only that one.

Tim: Specifically intrusion when you're not in a login flow? If I say, "No SiwG\!" would I still not see it in a login flow?

Wilander: Maybe not if it's the only option. 

Tim: Right.

Wilander: Signal to IDPs. Well-behaved folks wouldn't show it unless necessary.

Sam: I think we can agree on something here. FedCM can really help here. Open to lots of options. One solution Safari could implement that would make those popups go away: passive mode. Load the website, which checks to see whether credentials are available, if so: FedCM, if not, frame. You could implement this in a way that suppressed login prompts with a no-op implementation of FedCM. This specific solution doesn't give the IDP a choice.

Wilander: Requires an implemented feature detection?

Sam: Requires an implementation in FedCM. Would love to work together to solve this problem.

Wilander: You send in the IDP as a URL?

Sam: Correct. No return values, etc. `mode=passive` called when page is loaded. You could choose to implement that as not showing UI at all. Chrome has an implementation we can talk about more tomorrow in broader discussion on intrusion. We think something subtle in the URL bar is good enough. Pill in address bar. We call it "ambient UI".

MT: I'm not jazzed by this arrangement. Walks towards the reasons we weren't able to ship. Requires understanding of more modes, more complexity. Cautious about that. But SiwG is a plague. Brave blocks it entirely. We've talked about it. But some people really want those options, we don't want to take that away from them. But it's a terrible user experience.

Wilander: Common complaint for us too.

Sam: Us too. We can address the amount of spam by inverting the defaults. Could say we only support that a low-visibility mode is the only thing in the spec with an extension for passive mode, etc.

MT: Possible to say that folks who don't want to see Google logins don't see them, deemphasized. I don't want to leak more bits to these entities. Tracking.

Wilander: Zero-bit solution would be idea.

Sam: You can solve this in a single patch today, would be a valid implementation.

Wilander: The passive mode thing.

Sam: Yes.

Tim: do you see a world where the browser can help the user understand they *did* use that in the past, but then forget and can't sign back in?

MT: We can remember they used one of these things. Unless that UX is triggered, we don't have the chance to help the user. Maybe passive UI could be an opportunity? In our UX, we'd highlight credentials you'd used on the site in the past to make it simpler for them to sign back in.

Wilander: Often when we're faced with a mature thing shipping in Chrome, and think there's a version we want to ship, it turns out that Chrome-specific things that weren't known as dependencies that make it not work in Safari. Cross-site cookies might be a problem here.

Sam: Yes. We've always had the absence of third-party cookies as a requirement. We believe that's maintained in our implementation. Further: I think we've also made FedCM resilient to link decoration mitigations.

Emelia: FedCM isn't using cross-site cookies. Only using SameSite cookies with the IDP's origin. Browser is mediating the interaction.

Wilander: What I;'m fearful of is that it looks like things work, but there's some final stage in which login assumes cross-site cookies and tries to do some extra thing.

MT: Doesn't break in every website, but some.

Emelia: FedCM doesn't use cross-site cookies.

Wilander: Right. But sites might have subtle extra dependencies on cross-site cookies.

Sam: Only way to prove that is to implement it. Nothing I'm aware of that would break that assumptions. It works in Chrome without cross-site cookies. Incognito, users that disable.

Wilander: NASCAR thing and opt-out signals. Are we getting to a place where users see only options they favor.

Sam: Yes. These are all browser UI choices. Large social login IDPs are all exposing themselves as FedCM IDPs. Sites call FedCM, and we show a picker. We rank based on your past choices. Purely browser UI choice, allowed by spec in a unified account chooser.

MT: You don't need to spend screen real estate to enable more IDPs.

Sam: We don't show accounts where you're logged out of an IDP. Which gives smaller providers a boost.

Wilander: I might still want to use an IDP where I'm logged out.

Sam: Affordance for that.

Heather: Can we capture additional questions? Running out of time.

Emelia: Does the work we've done on decentralizing FedCM make vendors more or less likely to implement FedCM?

MT: It's been a major concern we raised early on. But I think it's been addressed. No systemic bias in the design towards a single large entity. So that's not a reason not to ship.

Emelia: So we've correctly addressed your problems and it's the right direction for vendors? If there's something we need to change or need feedback on, I want that feedback.

MT: On this point, no remaining concerns from us.

Wilander: FedCM has favored federated logins. There's something there. Aren't passkeys a better solution? Should you have powerful IDPs? Is that the great bright future? That's still on our mind.

Bumblefudge: EVP, those are a little different than authenticating to a website. Might have different sematics. Passkeys are a weird fit for atproto. Is there still a role for IDPs after passkeys? Migth be a role for other kinds of IDPs. Passkeys don't obviate the concept of an IDP completely.

Heather: Sounds like a different conversation.

Mike Jones: To the extent that organizations have multiple properties... Google has GMail and other things, need federated signin and SSO on the web, sign into the IDP with a passkey.

Wilander: Two remaining things: 1\. Browser UI being required by the spec is sensitive. Want to provide our own experience, want to suggest passkeys, etc. Want to engage on that, know what's mandated. 2\. Enterprise story, different requirements. Browsers don't know whether the flow is consumer or enterprise, etc.

Sam: Sounds good.

Tim: Given convergence and different motivations: would be good to write down: "Passkeys are a self-issued IDP for a single site. Then there are \[other models the scribe missed\]." FedCM is a beautiful use case for enabling bubbles, but maybe that's where consumer usage ends.

MT: The same-party distinction isn't meaningful to us. Certainly the structure of the API enables the creation of those bubbles. Shopify used across several sites. Not stopping that from happening, but the design doesn't line up with organizational boundaries.

Heather: Future of FedCM is Thursday morning. Happy to continue this conversation there.  
[https\://www\.w3.org/events/meetings/64b54806-62fd-44fc-a3b0-345706c0a184/](https://www.w3.org/events/meetings/64b54806-62fd-44fc-a3b0-345706c0a184/) 

\[fin\]