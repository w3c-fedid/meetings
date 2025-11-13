# W3C TPAC 2025 \- Federated Identity WG/CG \- FedCM

# Agenda

* Administrivia \- 10 minutes  
  * Scribe volunteer(s)? Sam Goto, Darius Kazemi  
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Implementer’s report  
  * Shopify (Joel Antoci) \- 30 minutes  
  * Axel Springer \- 30 mins  
    * How we are planning to support Android Apps IdPs (e.g., gmx.de and web.de are email clients that are native apps rather than web apps)  
  * Microsoft Edge Browser / Microsoft IdP: Enterprise consent, workforce browser profiles, and other use cases (Emily, Suresh) \- 45 minutes  
  * Google Chrome Browser / Google IdP (Irene Chang, Nick Watson \- OAuth) \- 75 minutes  
    * Status  
    * Unification  
    * FLUX: unifying passwords/passkeys/federation for returning users: [https://github.com/w3ctag/design-reviews/issues/1092](https://github.com/w3ctag/design-reviews/issues/1092)    
    * Passkey Creation API \+ Verified Emails: [https://github.com/w3c/webauthn/wiki/Explainer:-WebAuthn-requestUserInfo](https://github.com/w3c/webauthn/wiki/Explainer:-WebAuthn-requestUserInfo)  , [https://github.com/WICG/email-verification-protocol](https://github.com/WICG/email-verification-protocol)    
    * Intrusion: How Chrome is dealing with Intrusion with quieter UIs (omnibox and ML models)  
    * Interception (deploying FedCM by changing IdPs but not RPs for OAuth redirect flows)  
    * An early discussion on how we’ve been exploring how FedCM can assist with Agentic Browsers  
* Any Other Business (AOB) \- 20 minutes

# Notes

- Administrivia  
  - Heather  
    - Use the [slack channel](https://app.slack.com/client/T010EGK9PQE/C02J6KB1ATC), IRC not to be used  
    - Code of Conduct reminders  
    - Go over implementation experience  
    - Shopify, Axel Springer, challenges with enterprises, as well as consumers  
    - Roughly 20 mins buffer in case we go over

- ## Shopify

  - Joel  
    - Identity team, Shopify  
    - Use of FedCM   
    - How we think it is useful for small/medium sized business  
    - Feedback that we’d like to share  
    - Millions of merchants  
    - The SMB identity disadvantage: competitive disadvantage with other marketplaces as far as identity is concerned, having rich data and signed in users, perpetually furthering their advantage.  
    - You run into [orage.com](http://orage.com), add a product you are excited to buy to a cart, then go onto a computer. Cart syncing, continuing from another device. We see a role that FedCM can play: if the user is logged in, it is easier to go across devices.  
    - Not a problem for large aggregators, because the user is always logged in to the marketplace.  
    -  Another use case: let’s say you have completed a purchase, and the merchant wants to offer you a discount on your second purchase.  
    - The merchant usually offers a login icon to offer a personalized discount, on a high intent login experience, where you want to sign in to the page.  
    - This is a small merchant, no longer needing to create an account in every merchant, by re-using your shopify account to log in to them.  
    - All of these problems could be solved with third party cookies, and in browsers that support third party cookies we do leverage them. Challenging for not being widely available, privacy-preserving, or future-proof. We are seeing more people opting-out of third party cookies than opting-in. That’s also where FedCM could also help.  
    - Contextually, for the merchant, where we could bring the inline experience. It is sometimes hard to have a user understand why they need to sign in.  
      - (goes over what a PEPC-like user experience could look like)  
    - Trade-offs  
    - Other improvements  
      - Input autofill  
      - Modal UI  
      - Theming  
      - Multi-get  
      - Better metrics  
    - Shows your shopify account in the autofill options  
    - For high-intent sign-ins, we like the modal UI, especially on desktop, similar to passkeys, the user is taken to a browser-mediated UI that’s central to the browser screen; we would like that to be done in a passive mode, without a user gesture; we would like that for high-intent sign-ins, being louder. We also see users cancelling the passive mode, misunderstanding, and confused users thinking this might be a sign-in with Google.  
    - We would like better branding options, hard for users to distinguish between a sign-in with Google and a sign-in with Shop. In dark mode, we don’t have the ability to control the color of the button.  
    - The browser makes high contrast decisions in dark mode. We would like the ability to provide branding for both modes.  
    - Multi-get when you have different identity providers, today the first one wins. I think it would help our merchants, who have multiple identity providers, to benefit from multiple get APIs.   
    - Ultimately, we could use better metrics. We have worked hard to improve conversion over our third party cookies. I’m not going to share metrics today, I don’t have a great way to get sign-in conversions, or to find better ways to get.  
  - Wendy  
    - Would you be able to make these slides available?  
  - Emelia Smith  
    - On the multi-get point, could this be solved by being identity provider agnostic? This was something that I think was being able to allow different cases of social media. I just want “an identity provider” — I don’t care who. (I was thinking of [https://github.com/w3c-fedid/idp-registration/issues/1](https://github.com/w3c-fedid/idp-registration/issues/1) )  
  - Nicolas  
    - I think you are talking about IdP Registration there, not sure if it can solve the problem for the shopify use case. I believe what they have right now, merchants who want to use sign-in with Shop, as well as sign-in with Google.  
    - I don’t think the merchant wants any idp, could potentially work, but i don’t think it would necessarily work.  
    - The multi-get, on the other hand,    
    - Question for Joel: do you have any mocks for the modal UI? You go to the login page and you want to show the modal UI? Seems heavy handed? Is Shopify the only login option?  
  - Joel  
    - There would be a vanilla option, username/passwords. The merchant has full control over the site, they can configure other providers, but when they do not, i do think that the modal UI would guide the buyer more successfully toward a sign-in. What I like about the modal UI is that its UI is contextual, in the sense that it renders where the user’s attention on the screen is, full and centered, ideally i’d like to get full customization, but the full screen UI…   
  - Sam:  
    - Re: IDP registration, Emelia’s question. It hadn’t occurred to us that we could solve the problem through registration. Thanks for raising that. Mechanically speaking, registration would work by being a single call, and having the account chooser show the accounts you’re logged into. But you might also be logged into a Mastodon or Bluesky account, and question whether Shopify would take those accounts with the same meaning/trust.   
  - Joel  
    - If the merchant wishes to accelerate with Sign-in with X, Y and Z, it is Shopify’s app. I don’t see at first glance a concern from the Shopify part. Given that this is the agency.   
  - Sam  
    - I have an intuition that merchants will accept any provider to get more people in the front door, in the same way that they will accept any email provider to create an account with usernames and passwords. The analogy is, it just becomes a fancier autofill. Emelia, I don’t know if you’d call it a fancier email autofill.  
  - Emelia  
    - I think I agree. It’s similar to a magic link sign-in. From a shop perspective they probably wouldn’t care which identity provider you use. They might if they are doing a special campaign or something but the point around trust levels would be primarily a point for if you wanted to connect say a payment method on top. In that case you’d have an enumerated list of accepted payment providers, versus just any identity that tracks login and viewing, putting things in a cart. Those are different levels of trust.  
  - Phil Archer  
    - I was buying a book, and I clicked a button and it was nice and easy.  
    - And then I went to another shop.  
    - I might have said yes.  
    - Having had the experience, I think that worked.   
  - Joel  
    - As a developer, if I had the ability to say, “why you are seeing this?” if I could explain to the shopper “why you are signing-in”.   
  - Phil  
    - I don’t use google pay. I didn’t realize I was doing anything other than checking out at a merchant.  
    - My reading (points at screen) is that I’m signing-in to that specific website.   
    - I got to the end very quickly, it worked very well.  
    - I signed-up for something across retailers. And I’m happy. But the second time I was shocked.  
    - It is not a complain, it is a congratulations, but I do feel a little bit cheated, but afterwards,   
    - 

- ## Axel Springer

  - Thomas Bergemann, Axel Springer  
    - I’m the team lead of login and authentication at Axel Springer.  
    - Registration and login is an extremely important part of the ecosystem.  
    - Axel Springer is a portfolio of journalistic brands, with an advertising business, a price comparison platform, and more.  
    - We came to this situation where our registration and login situation was a home page with a button, register via our menu or via articles(?). We have multi-IdP solutions, and we have here the possibility to have an advertising ID in the back that we use to sell our ad inventory well.  
    - FedCM is a better solution because there’s a possibility to show the people they can log in with one-click via their email address directly. We need this registration. We are normally not a login and registration portal as the main internet portals, so we need this to come in place.  
    - For us, we want a trustworthy solution, multi-IdP is really important so that we can choose as many IDPs as we want. We are looking to add new IdPs.  
    - Registration is part of our core subscription model, but also to stabilize the user and understand how user flows are working.  
    - For us it’s really surprising that the lower risk implementation we had was FedCM. With limited developer resources, it was pretty easy to implement. When with a normal login flow we have extremely spammy email addresses, and normally we have many fake emails and fake credit card registrations we have to filter, it’s good to have FedCM as a service that limits that.  
    - Now we come to some numbers. Short notice: current status, Welt is fully implementing FedCM. We are talking to the classified business and other businesses inside Axel Springer, and they are interested in implementing.  
    - For the numbers, we have 14x more monthly registrations with FedCM comparing a Jan-May period to Jun-Oct period. It’s extremely successful, no other strategy works as well for stable logins. Of course, right now it’s only Google Chrome but we want other browsers to join and have even higher impact.  
    - We do have some problems. The situation with multi-IdP is a problem on mobile. Most IdPs we use do not have direct browser sign in solutions. NetID is using an Android app and not the browser. For us, that’s extremely painful. 75% of NetID users use it on an app basis. This brings us to the need for a workaround to bypass the third party app to sign in on a browser basis.  
  - Joel  
    - I just went to Welt and saw a FedCM prompt, which was cool. Then I went to a dedicated login page and I don’t see the FedCM prompt there, I only see it on the home page. Does that track with your implementation knowledge? Can you share the reasoning?  
  - Thomas  
    - That’s correct, it’s part of the user flow that we have behind it. We have a lot of traffic coming from google and other social media, and there are other processes behind the registration flow, and we have a better flow for the credit card with direct login.  
  - Joel  
    - We think there is value in showing FedCM on the login page. Maybe not via the current UI. I was interested to hear a different take.  
  - Thomas  
    - Of course, we can use FedCM directly in our pages, but it’s not possible to integrate FedCM directly in our current registration flow. We have special registration login pages; it’s not so important for us. When users see too many popups, the users are more estranged (?) to what they can use now.  
  - Sam  
    - If you could go back a few slides, there was a graph of distribution between websites and apps. There was one I couldn’t read. I understand “App” and “Desktop” but not “MEW”.  
  - Thomas  
    - It’s “Mobile enabled web pages”, our HTML web pages on mobile. Nearly 70% of people are using mobile pages.  
  - Sam  
    - Oh, this is the RP, not the IDP? This is Bild and Welt traffic.  
  - Thomas  
    - Yes, it’s extremely different from the registration part. We have more registrations from desktop. From our portals we have a lot of Safari traffic, and in Germany Mozilla sees a lot of use.

- ## Microsoft Edge Browser, MS IDP 

  - Emily Lauber  
    - Talking about composed web experience. Relevant FedCM issues are [782](https://github.com/w3c-fedid/FedCM/issues/782), [729](https://github.com/w3c-fedid/FedCM/issues/729), [725](https://github.com/w3c-fedid/FedCM/issues/725), and what to do with iframes  
    - I’m referring to a host app embedding other apps via iframes. These have same-site and cross-site scenarios.  
    - For our users, users don’t often see or understand the difference where iframes are involved  
    - I’m using a generic example of a composed page. The top site is platform.cloud.com which is a generic productivity app. Then there is a third party app embedded, a user generated content iframe embedded, and a first party agent site embedded. Plus hidden iframe code for something like telemetry that doesn’t involve anything the user sees.  
    - Examples of this in the wild include Outlook, which embeds Zoom for scheduling purposes; and Salesforce which embeds Word for contract templates. You could theoretically imagine a future where agents might act as a platform app that embeds iframe content from a bunch of different pages  
    - On these composed pages, identity can get pretty hard. If we want a silent flow, we might rely on cookies or shared storage for login hints and session management.  
    - We block redirects in iframes to prevent clickjacking. They fail on silent flows and have to do multiple popups instead.  
    - The ideal experience I want from FedCM is an iframe permission policy that is set by the top origin. The options, for which I’m not married to these names, include things like a “no auth” policy (user generated or unauthenticated content); and a “same auth” where you lock the iframe identity to the same as the origin. My argument is that the top origin knows which iframes they are embedding and want to lock identity to. Then there’s an “any auth” that allows iframes to embed using their own identity.  
    - In practice, if I go back to my generic platform productivity app we see a traditional FedCM login. In my user generated one, there is NO AUTH; first party is SAME AUTH; and for the third party app, we use ANY AUTH. If we click and log in, we see Elisa is logged in for the SAME AUTH iframes, but maybe the third party wants its own login and prompts a different account. Sometimes when people don’t want to pay for something they use shared accounts, and in the case of this third party app maybe the user logs in as herself for the top level, but uses a shared account for the specific third party app.  
    - I’ll end on the final pitch. I think FedCM can simplify identity, composed experiences are everywhere and the top-level app should manage this. At MS, we have custom logic and platform specific SDKs for this. If we can have FedCM manage this for us, it allows the locked-auth experience where relevant and unique auth where needed.  
  - Nicolas  
    - I have a question about how you see the “Same Auth” scenario, which is the only scenario we don’t support today at Google Chrome. I noticed in your demo that there is no UI for the “same auth”, so my question is how do you see this working from the browser perspective? Do you see the browser automagically granting a token to the same auth iframes? How does it work?  
  - Emily  
    - Suresh, can you help talk this through? It does depend on other scenarios. If the user has already visited the first party agent or the hidden iframe and has already authed with the RP & IDP relationship, I imagine it could silently succeed via reauth calling the FedCM API. If it’s the first time, a user might need to see consent dialogs, but the only available account(s) would be the one(s) logged in to the origin. If the UX needs to be shown, then only the one account on the top level is shown even if in theory there are 3 or more that *could* be shown.  
  - Nicolas  
    - You don’t want any UI for the same Auth?  
  - Emily  
    - Correct. I don’t want any UI, but I have experienced pushback. I’m okay with some UI, as long as it’s the same account. I picked a first party agent in my demo to show scenarios. If Outlook is embedding Zoom, the assumption is you have to use the MS account to OAuth with Zoom, so the assumption is you’re using the same account here.  
  - Joel  
    - Can you use the trust signal for storage access API that you get after the FedCM prompt on the top frame to get the first party iframe to talk to the IDP?  
  - Emily  
    - I don’t know offhand.  
  - Yi (in zoom):  FYI [https://privacysandbox.google.com/blog/fedcm-saa-integration-chrome-131](https://privacysandbox.google.com/blog/fedcm-saa-integration-chrome-131)   
  - Joel  
    - You basically get the third party cookie after the FedCM prompt after the user consents to FedCM… The other question I had as a web citizen, it sounds like in your desired UI, you’ll see two FedCM prompts, back to back. One from the top-level and then one from the third party iframe. Wouldn’t I be surprised, if I don’t even know what the third party domain is?  
  - Emily  
    - I think it depends on the platform app itself. There could be scenarios where the platform app only allows same-auth, and other scenarios where the platform app allows some kind of federation to different apps. I argue it’s up to the platform app to figure this out  
  - Joel  
    - I am concerned that we dilute the FedCM experience and we risk antagonizing the experience. But I haven’t though iframes invoking FedCM much.  
  - Emily  
    - I would argue that I want to minimize prompts as much as possible, but in scenarios where it’s unavoidable and the browser needs a signal that a user has consented to an RP and IDP relationship, I’m okay with it. My ideal is that it’s the RP and IDP that need to know that, but if the browser is the middle, there might need to be some prompt considerations. I’d also argue that the FedCM UX of multiple logins in one is better than multiple popups that would otherwise happen.  
  - Yi from Chrome  
    - For Same Auth, you were expecting something like no UI to re-auth. That’s a valid feature request; we can start a github issue and work on that. We’ve heard it from other partners. When auto-reauth happens, we still show some UI. But I had a question about the demo. For same-auth, I can understand the first party same-auth, but the hidden telemetry iframe is still a cross-site thing. Same-auth doesn’t mean same-site, right? It means the same account across multiple sites. Where do you imagine an account would be stored between those? The browser doesn’t know where a user is logged in from, just the top frame.  
  - Suresh  
    - I think it would be stored in the browser.  
  - Yi from Chrome  
    - So the browser would store IDP and other information. For the same auth, we would maybe just look up whether it’s a top frame IDP binding and use that account? Is that what you’re thinking?  
  - Emily  
    - I think yes? Mostly I just wanted to describe my use case rather than the technical details of storage. I’d defer to Suresh.  
  - Yi  
    - What if the user is not logged in to the top frame, and the APi is called from an iframe? Do we just ignore the policy?  
  - Emily  
    - I hadn’t considered that. Why would the top frame set a same-auth permission if it’s not logged in?  
  - Yi  
    - It’s still possible.  
  - Emily  
    - I suppose if you log out of a platform app, a user would not assume they are logged out of a third party CRM. User expectations would differ there, I think; some would say they should be logged out, others would not. Maybe I’m rabbit holing too much on the logged out scenario. Say they were logged in to crm.example on a different tab, and opened platform.cloud with the iframe in a different tab, what would happen? I had just been thinking about this platform scenario and things are logged in, but haven’t thought about the logged out scenario.  
  - Johann  
    - What you essentially want is that the identity returned is delegatable by the top level. The top level has some kind of token that gets returned by the API when it’s called, and the iframes get the same token?  
  - Emily  
    - I don't want just the same token — it could be tokens appropriate for the clients — but I want it locked into the federated top level account. I don’t want the iframes to impersonate the top app, but the iframe gets a token from the account at the top.  
  - Johann	  
    - So they would get different tokens from the central IDP?  
  - Emily  
    - The assumption is that the central IDP supports federation across multiple apps.  
  - Johann  
    - How does the IDP know which identity to give out to different iframes using same-auth? What’s the mechanism for it to understand that? You’re assuming the iframes don’t have 3P cookies and sessions, so how does this work at a high level?  
  - Emily  
    - We use login hints today in the silent flow. I’m trying not to get into the custom SDKs we do today, I want to focus on what we could do in the future. My expectation is that the one set with the same auth, in the message to the IDP would communicate a login hint from the platform app making the call. Actually I don’t know if same auth needs to go to IDP or to the browser itself in terms of limiting the identities served.  
  - Nicolas  
    - It’s the browser, the browser would know which is the ID they need to use.  
  - Johann  
    - It’s not a different IDP right?  
  - Nicolas  
    - Yes, and this is assuming the top level uses FedCM. We know what accounts were chosen, and then we can send the same accounts to iframes.  
  - Johann  
    - Without 3P cookies, this is broken right now?  
  - Emily  
    - We can make it work without 3P cookies, but it’s very complicated and uses custom SDKs, requiring the user or the IT admin to set up a relation, use OAuth to set up the federation, going to the first party, approving apps, and so on. It’s very click intensive. My preference would be that we can leverage browser APIs, if you already know, please let us just use that.  
  - Johann  
    - The iframe wouldn’t set same-auth right? That’s the top level?  
  - Emily  
    - Yes  
  - Nicolas.  
    - Same-auth would have to be set at the top level for it to be meaningful and acceptable.  
  - Emily  
    - I would want the platform app to set these policies on the top level.  
  - Johann  
    - I think that sounds okay from a privacy perspective.  
  - Emily  
    - If you’re curious about how we do this, I link from the presentation some examples of Outlook and Zoom, along with Salesforce and Word. You can see the ten steps we have to do today.  
  - Emelia Smith  
    - I have a feeling this may introduce a lot of security issues in that if the top frame misconfigures what it allows, then it could allow any iframe on the page to access the credentials of the top frame without the right intent. As for the matter of getting a separate credential… There is [RFC 8693](https://www.rfc-editor.org/rfc/rfc8693.html) Oauth 2.0 token exchange RFC, that allows a resource server to send a request to the auth server and say, "I would like to request a new access token", creating a token that gets delegated. Perhaps something similar to that would work in this case where the top frame is responsible for creating the authentication and then for the iframes you’re just requesting up to the top frame, not to the IDP. Essentially rather than the top frame saying at authentication time, "these are the iframes I trust, and this is how you should allow this FedCM session to be shared with sub-iframes", I think it would be better to have an API that allows the iframe or the third party app to request a token from the top frame, and then the top frame has logic that says. "this domain is requesting a token", and sends that across to the IDP. So the top frame is always the one talking to the IDP, rather than the child frames. So the top frame is the intermediary between the third party app and the IDP, so the top frame is the trust domain. The iframes are essentially saying, "I would like to request auth from the current frame", whatever that is, and then having on the current frame, code that says, "do I want to confirm this request", and then if so the token mediation happens.  
      - NOTE: Emelia [wrote up her comments here](https://github.com/w3c-fedid/FedCM/issues/782#issuecomment-3524767224)   
  - Emily  
    - What you’re describing is kind of what we do for the scenarios we have now. One of the custom SDKs is called our nested app authentication, which is very similar to where the iframe makes a call to the parent frame to get a token identity on the iframe’s behalf. We say the parent app is brokering for the child. The important part is the parent has some code to do this on behalf of the iframe. I would argue it is simpler to have the browser do that rather than the platform app. Your approach is valid but it comes down to which is simpler and which more secure. From your perspective the concern is the platform app misconfiguring their permissions policy and so to you the more secure pattern is the platform calls the IDP and the IDP decides on tokens getting returned rather than the platform configuring. I’m not sold that it is more secure, though it can work.  
  - Emelia  
    - I’m not suggesting that, just that the FedCM API exposes a method for the iframe to request a mediated token or whatever term. And the top frame receives an event that is an instance, "hey, you’ve received a token. Do you want to trust it?"  
  - Emily  
    - So you’re still using FedCM?  
  - Emelia  
    - Yes, but once the browser takes over, it does a token mediation where if you weren’t logged in at all, the iframe did a request, the top frame would ask you to sign in, once you sign in to the top frame, the browser would automatically based on the result of that say that the iframe can request a token.. then the browser says to the IDP “hey I know we are signed in, I want to pass this along” and there’s no shared token but tokens are bound to specific origins. The top frame gets to decide who gets access  
  - Emily  
    - Can you put that that proposal in issue [\#782](https://github.com/w3c-fedid/FedCM/issues/782)? Same auth was a first pass attempt, and I am open to what you’re proposing  
  - Heather  
    - It would be great to get this documented in the repo. We have one other person in queue  
  - Sam  
    - Can Edge be willing to prototype this? Is this just from MS Identity or is Edge involved?  
  - Sid from Edge  
    - Yes  
  - Emily  
    - One other thing I’m a broken record on for enterprise applications of FedCM, is that for enterprise apps, it’s not often the user that is consenting, but it is the IT admin who is consenting on behalf of the user in an enterprise scenario. We’ve handwaved enterprise policy away as an implementation detail, but that’s an important thing to continue to keep in mind.

- ## Google Chrome Browser / Google IdP (Irene Chang, Nick Watson \- OAuth) 

  - Irene: (product mgr, Web identity for chrome). 2025, 26, and more. 3 highlights of FedCM in 2025\.   
    - Active mode: when users connect via the login…  
      - Now, bottom-sheet experience, rather than redirect on mobile.  
    - Addressing intrusion of login prompts, ML models for optimizing conversions  
      - Concerted investment in balancing user experience, user intent, and scaled back UX when intent is less clear.  
      - User research: the unexpectedness of the popup was an opportunity for improvement.  
      - Don’t make the web noisy and annoying as compared to app walled gardens.  
      - ML modeling to see what signal thresholds we’d want to reach before showing the user the UX (with expectation they’d click through).  
      - Looking at ways to refine UX without intrusion, presenting FedCM in context closer to the user.  
    - Launched multi-IDP support, more login choices for our users.   
      - Better choice for users, websites, IDPs, as Axel Springer showed.  
    - Looking ahead to 2026\.  
      - Email verification protocol, unified sign-in, Navigation interception API.  
      - Email verification, Sam presented a breakout yesterday, cryptographic proof of email possession. Provide verification without switching context.  
      - Unified Sign-in: Consolidating types: passwords, passkeys, federated logins. Reduce the mental load of determining what they used last time.   
      - Navigation interception API.  
  - Nick  
    - Navigation Interception API: current status. You know we have our fair share of documentation and APIs. GSI (authn \+ authz) fully migrated to FedCM. OneTap (corner widget), also migrated to FedCM, opt-out to be removed soon. Button-flow is opt-in.   
    - The most common way to sign in with Google is still using OAUTH/OIDC and redirects. This pulls the user out of context, to a Google page; can be awkward on mobile.   
    - Interception API is needed because many RPs are currently using redirection, and it’s hard to reach them all to ask them to change. Can the browser do more? not entirely on its own. Interception is the idea that the IDP can return a header to the browser showing an equivalent FedCM request. Allow the browser to proceed with FedCM rather than navigation.  
    - Benefits: keeps the  user on the site, makes it clearer they’re signing in to a 3d party; better on mobile; protects against future link decoration mitigations.  
    - Could play a role in agentic space.  
      - Agents do better with tools, structured API agents can call. Allows agents to use federation as a tool at scale. Sign into websites.  
  - Irene: Q\&A   
  - Tim: Interception is a terrible name, but I like the feature. I like the agentic client-side, getting developers over the line to FedCM.  
  - Emelia: In an agentic context, wouldn't an agent be engaging with a browser through puppeteer or another headless driver?   
  - Johann: They have tool calls.  
  - Arnar: The biggest win is avoiding giving the LLM access to full cookies at the IDP. Agent harness, rather than LLM, gets the cookies in this tool.  
  - Sam: Right now, many agent interactions are through unstructured APIs. Proposal to augment pixels with a structured API.   
  - Emelia: The OAUTH WG is also working a fair bit on agentic access in their context. May be an opportunity for crossover.  
  - Mike Jones: Question about how it works and implementation status. How it works: When the redirect goes back to the RP, are you sending the OIDC token in addition to saying you can do FedCM call?   
  - Nick: For our prototype, from the IDP side, we’re running the request as is, and additionally returning the header. Needed for backward compatibility anyway  
  - Mike: Implementation status? Testing  
  - Nick: Pretty new, code is still in progress. Expect we’ll be able to try with some real RPs in the next few weeks.  
  - Mike Jones: Is the intent, if this looks promising, to add it to the spec?   
  - Sam: Chrome has sent an intent to prototype with an explainer; have a raw behind-flag implementation in Chrome Canary. If it works, then we’d hope this group would accept it as a contribution to the spec  
  - Joel: Who is the RP in this case?   
  - Nick: The agent is acting on behalf of the user to do a task  
  - Emelia: Why is this necessarily related to FedCM? Isn’t it, I’ve got a form, here’s how you’d submit it. Why is FedCM taking over the FedCM request? Taking OAUTH and stepping up to FedCM  
  - Sam: FedCM is OAUTH-agnostic; it serves many OIDC flows. Exposed through params.   
  - Nick: You mentioned PAR (push authorization request) should also work here. Need to translate. The authorization server is still going to get all the same parameters it would otherwise get.  
  - Joel: PKCE was mentioned. Shopify is interested in protection from exfiltration by a malicious agent. How do I know where clicking a button would go, so I know what I need to pin?  
  - Sam: The goal is that the RP doesn’t have to change anything. Indistinguishable from a 302 on both ends.  
  - Yi: You don’t get a promise back.   
  - Sam: ID assertion endpoint sends back “redirect to” RP. You lose state as with a navigation.   
  - Christian: If you don’t want to lose state, make a FedCM call.  
  - Emelia: One concern I have here is that this changes the interaction model that users of browsers have with regard to FedCM. Potentially lacking consent. Allowing a remote party to trigger a FedCM call, rather than on user button-press. I think that will lead to user confusion.   
  - Sam: re user expectations, we’ve already migrated a good chunk of the sign-in with Google buttons from javascript to FedCM.   
  - Nick: I don’t think this is a new problem. An RP could change its flow and present a new UI to the user.   
  - Sam: We expect to deploy at a larger scale without breaking user expectations.   
  - Christian: A way for RP to opt out  
  - Emelia: When the RP makes a change, they are in charge of the popup showing; if the authorization server makes a change, they are directing a change in UX without RP necessarily being aware.   
  - Christian: You think this is substantially different from the IDP changing?   
  - Emelia: If authorization server changes, the user is on that domain, knowing whom to attribute a prompt to. It's a permission prompt without context, versus an application telling the user to expect a prompt. This wouldn’t work with DPOP, private key is well protected by the client and doesn’t leave the client.   
  - Nick: This should look the same as if they 302’d.  
  - Emelia: But FedCM doesn’t know about the DPOP key.   
  - Sam: Could be passed through params.  
  - Christian: There is a proposal to let credential requests go through a service worker.  
  - \[discussion goes deeper than scribe can note-take\]  
  - Nick: Token endpoint is out of scope of FedCM, all backchannel.   
  - Emily: Echo potential UX concern. We have many RPs, many would be happy about updates without having to make changes; others would be upset or find jarring to see a prompt on their origin.   
  - Nick: For now, we’re just talking about agentic space; if we were moving it toward end-users, there’d be an announcement and more, such as an opportunity to opt out.   
  - Johann: What happens if people reject the prompt?  
  - Sam: What happens when a user cancels?   
  - Nick: if they cancel, return/redirect   
  - Johann: Concern with web compatibility if the site expects navigation and none happens. Consider potential security issues, breakage…  
  - Emily: E.g., pre-prompting.  
  - Emelia: Could also break automated testing. In some cases, you’d end up at a dead-end flow on the authorization server, where the authz server doesn’t have a redirect.  
  - Nick: On the google side, we check for matches immediately, return invalid if not. And we’ve promised to uphold the protocol, and not the UI.   
  - Emily: I’d argue it’s the responsibility of the authz server to communicate to RPs if there are changes.  
  - Emelia: I’d say authz server can change its UI, but because you never get to their UI, it’s a bit different here, where it looks like the RP’s problem. Concern that they’d now be getting support tickets about a popup they didn’t start. (Emelia said she was fine with moving on)  
  - Heather: Let's move on for now.  
  - Irene: Intrusion. We’ve made some some changes, invite feedback.  
  - Sam: Choice of UX. We want to match the volume of the UI to the user’s intent. Modal is very in-your-face, works fine if the user is likely to sign in. But where we expect user intent is low, cool-down. Two things we’re introducing. ML models to understand user intent and make predictions. Trying to give the ML model more options for volume, e.g., the omnibox chip you’re seeing on this slide, quieter than the widget.   
  - Joel: \+1 to that, we can’t bring context that the user is signed in to IDP when 3d party cookies aren’t available. User reaches the page and might not realize they have accelerated sign-in opportunities. We could show the modal UI once the user signs in. Inform the user they don’t have to complete a less secure, higher friction sign-in. Endorsement of a louder FedCM UI when intent is clear.   
  - Sam: It’s too loud in some places, and too quiet in others.   
  - Wendy: wondering about the user expectations when a page changes appearance based on features they don’t know about  
  - Joel: not dissimilar to the passkey pattern  
  - Sam: Nina, can you share whether user gesture requirement is common?   
  - Nina: Passkeys, you must have created one for the origin already. FedCM doesn’t have that. Websites won’t invite the terrible experience of a webauthn prompt on every page, because if you get a QR code you can’t follow, it’s bad. Think the semantics are different enough.   
  - Joel: today, you can force the passkey prompt with an iframe.   
  - Nina: Without 3d party cookies, the iframe doesn’t know if there’s a passkey for the user, so it would be risky for them to call navigator.credentials.get.   
  - Joel: I keep pushing FedCM and passkeys to be in the same bucket. Similar action, user wanting to sign in, different tools at user disposal.   
  - Tim: They’re fundamentally different privacy models.   
  - Nina: if you unify, then the barrier to using the API will be the highest among the choices.   
  - Tim: A user controls their passkey  
  - Heather: where is $this getting written down for WG consideration?  
  - Sam; delegation, privacy preserving version of delegation, is written down  
    - Email verification   
    - Autogranting of passkey conditional create. Use federation fro sign-up and passkeys for sign-in.   
    - What Joel is asking for, finding a way for the modal to show up on login page without user gesture.   
  - Tim: I hate the webauthn popup on web page load, but we did it because there was the argument that apps could do it.   
  - Joel: From dev perspective, popup without user gesture allows more users to sign in more securely.   
  - Tim: long-term, it would be helpful to get one big image of all these UXes.   
- Heather: we have regular meetings. Let chairs know if you’d like to attend but need different timing. Tomorrow, another WG meeting, on DC API. 


# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Sam Goto (Google Chrome)  
* Christian Biesinger (Google Chrome, virtually)  
* Heather Flanagan (Spherical Cow Consulting, co-chair)  
* Darius Kazemi (Harvard Applied Social Media Lab, non-member observer)  
* Elaine Wooton (IDxQD)  
* Joe Andrieu (Legendary Requirements)  
* Nicolás Peña Moreno (Google Chrome)  
* Siddhatrtha Pandey (Microsoft Edge)  
* Simone Onofri (W3C)  
* Wendy Seltzer (Invited Expert, co-chair)  
* Hiroyuki Sano (Sony)  
* Yi Gu (Chrome)  
* Lionel Basdevant (Criteo)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Anna Weine (Mozilla, observer)  
* Tatsuya Katsuhara (Digital Agency, gov of Japan)  
* Emily Lauber (Microsoft Identity)   
* Natalia Markoborodova (Chrome DevRel)  
* Arnar Birgisson (Google IdP)  
* Joel Antoci (Shopify)  
* Irene Chang (Google)   
* Nick Watson (Google)  
* Nina Satragno (Google)  
* Suresh Potti (Microsoft Edge)  
* John Bradley (Yubico)  
* Tim Cappalli (Okta)  
* [Emelia Smith](https://hachyderm.io/@thisismissem) (Independent)

# Observers

* Denken Chen (Ministry of Digital Affairs, Taiwan)