# FedID WG/CG Telecon, 2026-08-25

* Moderators:  Heather Flanagan

* Scribe: Phil

* Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

* Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * [FedID CG/WG process](https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md)  
* Ecosystem Update (10 minutes)  
* Discussion (40 minutes)  
  * [Cross-device/System-level FedCM Flows? \#817](https://github.com/w3c-fedid/FedCM/issues/817)  
  * [FedCM facilitates vendor lock-in \#827](https://github.com/w3c-fedid/FedCM/issues/827)  
* AOB

# Notes

## Administrivia

* W3C  Code of Conduct  
* For new folk, can check out the process at: https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md

## Ecosystem Updates (10 minutes)

* Emelia  
  * Tried to reach out to the ActivityPub folk, might have a call in the week with Mastodon, not sure yet.

## Discussion (40 minutes)

### [Cross-device/System-level FedCM Flows? \#817](https://github.com/w3c-fedid/FedCM/issues/817)

* Emelia  
  * Scott (Lanoue) had a demo worth bringing to the group, being able to sign in with cross-device or the OS will be worthwhile.  
* Scott  
  * Working on AtmosphereOS prototype. Use your atmosphere account to log in to other applications on your phone; (existing) default you can use your email but not your AtProto account.  
    * First improvement: store the account and credential on the device, and use that credential for other applications.  
    * (Showing demo via screenshare)  
      * Showing Pixel 6a accounts sections, can see their Atmosphere account which is stored in the Android credential manager.   
      * Showing Bluesky login via the Atmosphere account.  
      * Clicked on the device account, OAuth consented, then into the application.  
      * Shows the desired flow: Store credentials on the device and use them to log in to other applications  
* Tim:  
  * Good work. Looking at the wider identity stack, why prefer this over a passkey?  
* Scott:  
  * Good question; initial thought, your passkey would be used to log in to the Atmosphere account, and then you can use that Atmosphere account…  
* Tim:  
  * Can you expand on that? This seems to be competing, but losing some of the benefits of passkeys, e.g., privacy, one-tap, etc.  
* Sam:  
  * Response to Tim: I do not think it's an either/or. For Bluesky specifically, you want your ‘handle’ to be used. You want to prove you own a specific ‘handle’.   
* Tim:  
  * True for Bluesky, but is that important for other sites?  
* Sam:  
  * I think what Scott is going through is similar to email verification. Need to prove you are that specific handle? (PS. scoped to an Identity Provider)  
* Tim:  
  * Few cases that handle matters? (proving control of an identifier)  
* Sam:  
  * I have to prove I am from [Google.com](http://Google.com) for access to (PS. did not catch)  
* Tim:  
* Sam:  
  * Have to prove you are a member of a specific university.  
* Emelia:  
  * Identity is important; you carry it throughout the fediverse.  
  * Relationship between application and data.  
* Tim:  
  * (PS. Figman?) Uses the IdP to know where to route you to. Not an access thing. Needs the correct tenant.  
* Emelia:  
  * Where the user is from comes back in the JWT (and is important).  
* Joel:  
  * Tim, are you suggesting creating a user with a passkey?  
* Tim:  
  * Not about the Fediverse or Atmosphere eco-system. Different question.  
* Joel:  
  * The passkey problem in Shopify is a user experience issue.  
* Tim:  
  * Saturating the eco-system with 9 different ways of doing something.  
* George:  
  * Seems like a federation scenario: use my identity across multiple different services.  
  * This sounds like I want to present something off my device to another party.  
  * Sounds like a Verifiable Credential.  
    * Assert to the RP, this is who I am.  
  * So not looking at this as a substitute for authentication, but for federation.  
  * Could Atmosphere issue a Verifiable Credential to the device and then present that to the RP? (So we do not have yet another authentication mechanism)  
* Emelia  
  * Yes, FedCM is more of a federation protocol, than an authentication protocol.   
* George:  
  * Agree with Tim about not creating more ways to do the same thing(s), but perhaps we should move that scenario to a Verifiable Credentials scenario, rather than layer that on top of FedCM.  
  * (Seems like a Wallet/VC system to me.)  
* Emelia:  
  * Counter that with. If passkeys and VCs can do what FedCM can do, why are we working on a FedCM spec?  
* Tim:  
  * Brought this up many times: what is the value of consumer federation? That has gone down since passkeys.  
  * Users want a one-click option, so sign-in with Google was the easy option, but now consumers can just use a passkey.  
* Emelia:  
  * So passkeys have not solved the issue for cross-ecosystem flows?  
* Tim:  
  * Think it has?  
* Heather:  
  * We are far ahead of the curve, and there is a long tail of people not ready for passkeys, so we need something safe for them to use.  
* Tim:  
  * People are doing federation, but they are not doing FedCM.  
  * Users just want to sign in a privacy-preserving manner.   
* Emelia:  
  * What we want is the things that come with the sign in.   
  * (describes a New York Times flow that needs more than just authentication, but also identity and attributes/claims)  
* George (from chat):  
  * ‘I think having worked at RPs for many years, most RPs want user claims at time of “registration” and once those claims are verified to the RPs satisfaction before allowing the user to associate an authentication credential.’  
* Tim:  
  * People have limited resources, and the experience you describe could be wrapped using existing mechanisms today.  
* Emelia:  
  * Passkey just gives you authentication, not identity. FedCM gives access to an extended ecosystem around identity.  
* Nicolás:  
  * My understanding is, there are two apps, and you fetch accounts and then show an account selector to the application.  
  * We have a prototype for this in Chrome.  
  * Most users are not logged into the IdPs in Chrome.  
  * Looking at FedCM in Chrome specifically.  
* Emelia:  
  * Have shown the cross-device FedCM flows to a friend who can talk to the Gnome Portal accounts folk.   
  * When I go to [iCloud.com](http://iCloud.com), it uses my device credentials to sign in. Could we do this for other accounts?  
* Tim:  
  * I am in favour of ‘getting out of the browser’ — not storing things in the browser, but outside.   
  * Do you want ephemeral access or a bootstrapping step?  
* Emelia:  
  * See it as a bootstrapping one.  
* Tim:  
  * Can bootstrap your account right now.  
  * Extended (PS. I think WebAuthn)  
* Emelia:  
  * Both are valid.  
  * One of the problems with FedCM is how to bootstrap the accounts. Not yet signed into an IdP, but landed on a service, so I need to get to the point of authenticating to an IdP through that flow.  
* Tim:  
  * This leads to where these work hand-in-hand.  
  * Do not want a solution that throws sessions around without trust.  
  * Use passkey to bootstrap the account, then use that.  
* Emelia:  
  * How authentication is performed is not yet standardized in these eco-systems.  
* Sam:  
  * Question to Scott: Why did you use GrapheneOS and how much have you changed it?  
* Scott:  
  * Wanted to strip out Google, and then try to get Atmosphere accounts into the OS.   
  * Originally forked GrapheneOS, but now I just use the mainline GrapheneOS and the credential manager.   
* Sam:  
  * What is the difference between GrapheneOS and Android  
* Tim:  
  * Similar without GMS.   
* Sam:  
  * Interested to see if we could do this in native Android  
* Scott:  
  * Plausible to move this across to an Android implementation from GrapheneOS

From Zoom Chat:  
      
2026-08-25 08:13:26 From Emelia S. to Everyone:  
    I can also respond  
      
2026-08-25 08:17:02 From Phil Smart to Everyone:  
    We do need that, based on the ‘scope’ e.g. an affiliation to a University  
      
2026-08-25 08:19:56 From Nicolas Pena Moreno to Everyone:  
    could you see it as a signup then?  
      
2026-08-25 08:21:16 From Scott to Everyone:  
    In full transparency, I prototyped this because there are already some Passkey solutions for ATProtocol PDSs — but I hadn’t seen anyone else implement this on-device flow, so I wanted to see if it was possible  
      
2026-08-25 08:24:01 From Phil Smart to Everyone:  
    e.g., a Trusted Research Environment needs to know your affiliation to a trusted organisation.  
      
2026-08-25 08:27:38 From Nicolas Pena Moreno to Everyone:  
    thats a separate topic.  
      
2026-08-25 08:29:49 From Phil Smart to Everyone:  
    Attributes  
      
2026-08-25 08:30:45 From George Fletcher to Everyone:  
    I think having worked at RPs for many years, most RPs want user claims at time of “registration” and once those claims are verified to the RPs satisfaction before allowing the user to associate an authentication credential.  
      
2026-08-25 08:31:30 From George Fletcher to Everyone:  
    So I would see this flow as present a VC and then if accepted, associate a passkey.  
    Tim Cappalli (Okta):💯  
      
2026-08-25 08:35:21 From Tim Cappalli (Okta) to Everyone:  
    and that's the converged flow that many want, that I've been trying to get moving but it hasn't been prioritized by browser folks  
      
2026-08-25 08:35:27 From Tim Cappalli (Okta) to Everyone:  
    because of competing priorities   
      
2026-08-25 08:35:57 From Tim Cappalli (Okta) to Everyone:  
    this was the getAndCreate method proposal   
      
2026-08-25 08:36:15 From Heather Flanagan (she/hers) to Everyone:  
    Replying to "this was the getAndCreate method proposal ":  
    Proposal in FIDO?  
      
      
2026-08-25 08:36:38 From Tim Cappalli (Okta) to Everyone:  
    Replying to "this was the getAndCreate method proposal ":  
    nope. at tpac  
    Heather Flanagan (she/hers):👍  
      
2026-08-25 08:37:15 From Nicolas Pena Moreno to Everyone:  
    Replying to "this was the getAndCreate method proposal ":  
    do you know if is this prototyped in chrome?  
      
      
2026-08-25 08:43:26 From Tim Cappalli (Okta) to Everyone:  
    Replying to "this was the getAndCreate method proposal ":  
    no. it was essentially dismissed   
      
2026-08-25 08:47:29 From Phil Smart to Everyone:  
    Replying to "So I would see this flow as present a VC and then ...":  
    The service might need re-authentication (fresh information) and would be required to manage the passkey and not the IdP (and passkey loss/recovery)?  
      
2026-08-25 08:48:14 From Tim Cappalli (Okta) to Everyone:  
    Replying to "So I would see this flow as present a VC and then ...":  
    yes. you only need an identifier at account creation time   
    Phil Smart:👍  
      
2026-08-25 08:48:24 From Tim Cappalli (Okta) to Everyone:  
    Replying to "So I would see this flow as present a VC and then ...":  
    you're only using the IdP for verified source information   
      
2026-08-25 08:48:37 From Tim Cappalli (Okta) to Everyone:  
    Replying to "So I would see this flow as present a VC and then ...":  
    you get a much more privacy preserving result  
      
2026-08-25 08:49:17 From George Fletcher to Everyone:  
    Replying to "So I would see this flow as present a VC and then ...":  
    That inverts the flow and what happens from a UX perspective if the user creates a passkey and then can’t actually create an account.  
      
2026-08-25 08:49:28 From Tim Cappalli (Okta) to Everyone:  
    Replying to "So I would see this flow as present a VC and then ...":  
    but it's even better if you have the federated assertion as a VDC  
      
2026-08-25 08:49:33 From Tim Cappalli (Okta) to Everyone:  
    Replying to "So I would see this flow as present a VC and then ...":  
    then you have zero privacy issues   
      
2026-08-25 08:49:35 From Phil Smart to Everyone:  
    Replying to "So I would see this flow as present a VC and then ...":  
    You might want to know you are ‘still’ a student.  
      
2026-08-25 08:49:53 From Tim Cappalli (Okta) to Everyone:  
    Replying to "So I would see this flow as present a VC and then ...":  
    then you can request the VDC again  
      
2026-08-25 08:49:57 From Tim Cappalli (Okta) to Everyone:  
    Replying to "So I would see this flow as present a VC and then ...":  
    just in time  
      
2026-08-25 08:49:57 From Isaiah Inuwa (Bitwarden) to Everyone:  
    Replying to "@Emelia S., I'm interested in the GNOME Portal dis...":  
    Sent you an email, with a meeting invite, if you've got a few minutes now  
      
2026-08-25 08:50:02 From Tim Cappalli (Okta) to Everyone:  
    Replying to "So I would see this flow as present a VC and then ...":  
    just like age or any other proof   
      
2026-08-25 08:50:05 From George Fletcher to Everyone:  
    Replying to "So I would see this flow as present a VC and then ...":  
    What Tim said :)  
      
2026-08-25 08:50:14 From Phil Smart to Everyone:  
    Replying to "So I would see this flow as present a VC and then ...":  
    Right yeah, or you could just re-auth using OIDC or SAML  
      
2026-08-25 08:50:19 From Scott to Everyone:  
    Thank you all for having me and discussing this work, I really appreciate the opportunity and the conversation\! I’ll introduce myself to the email list after this meeting  
    

### [FedCM facilitates vendor lock-in \#827](https://github.com/w3c-fedid/FedCM/issues/827)

* No time today. 

## Any Other Business (AOB)

* 

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Phil Smart (Shibboleth/Jisc)  
* Nicolás Peña Moreno (Google)  
* Emelia Smith  
* Sam Goto (Google)  
* Scott Lanoue  
* Wendy Seltzer (co-chair)  
* Tim Cappalli (Okta)  
* Joel Antoci (Shopify)  
* George Fletcher  
* Isaiah Inuwa (Bitwarden)  
* Yi Gu (Google Chrome)

