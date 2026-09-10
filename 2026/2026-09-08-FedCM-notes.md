# FedID WG/CG Telecon, 2026-09-08

* Moderators:  Wendy Seltzer

* Scribe: Phil

* Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/)&nbsp;

* Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html)&nbsp;

&nbsp;

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * [FedID CG/WG process](https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md)  
* Ecosystem Update (10 minutes)  
* Discussion (40 minutes)  
* AOB

# Notes

## Administrivia

* W3C Code of Conduct

## Ecosystem Updates (10 minutes)

* Wendy:  
  * Any updates?  
* Nothing

## Discussion

* Anything anybody wants to raise?  
* 113 open issues and 11 PRs: so maybe worth reviewing those issues or PRs  
  * Close, move, update, discuss, etc.  
* Anything for today?

  ### Email Verification

* Sam:  
  * On the Chrome side, concentrating on email verification.  
  * For this group, registration API is making progress. Emelia shared thoughts with the Bluesky community, seemed well received. Figure out next steps. Discussion with Microsoft and Meta.  
  * Progress on the native API (Android).  
  * Continuing to review items with Microsoft, service workers etc.  
* Christian  
  * Will EVP (email) be standardised in this WG, or elsewhere?  
* Sam:  
  * Does this fit the charter for this group?  
  * Do CGs have charters?  
* Wendy:  
  * CG has a scope, the WG has a charter.  
* Christian  
  * Eventually needs a WG for standardisation.  
* Sam:  
  * Maybe FedID fits, maybe … (PS did not catch the other group name)  
  * Any guidance, Wendy?  
* Wendy:  
  * CG does have a charter… [https://www.w3.org/community/fed-id/2021/11/10/community-group-charter/](https://www.w3.org/community/fed-id/2021/11/10/community-group-charter/)&nbsp;  
  * Do we have the right people to discuss and make progress toward standardisation for the work, and if not, would they be willing to join the WG?  
  * Prospects for standardisation: parties that are participating from the ecosystem, for multiple interoperable implementations.  
* Sam:  
  * Good questions, not sure there is an exact match in the existing groups.  
  * Is an extension of FedCM.  
  * Wendy, how do we go about this? (Process for getting it proposed to this group)  
* Wendy:  
  * Look back at the process steps and think about what stage the work is in. In interest, we should bring it to the group for discussion.&nbsp;  
  * [https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md](https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md)&nbsp;  
* Sam:  
  * Interested in finding a path to the WG.&nbsp;  
  * Shopify has been a big partner in developing it, too.&nbsp;  
  * Have spent a decent amount of time on email verification.  
    * Still working on FedCM; lots of that being done by Microsoft right now. Registration comes and goes.  
  * Email, can bring your own email provider. Useful for registration, too.  
* Wendy:  
  * Will discuss with Heather as co-chair.  
  * Each group needs to look at the work, see how it fits into their pipeline and process.&nbsp;  
  * Do not want to prejudge the WG decision; just looking at how to accomplish this going forward.  
  * Sam, link to that work so others can take a look at it.  
  * Can discuss in the various groups how to bring this forward most effectively.  
* Phil:&nbsp;  
  * How close is email verification to FedCM? Is it tightly scoped to receiving a verified email claim, in a FedCM-type flow? Or a different flow?  
* Sam:&nbsp;  
  * You got it right, a subset of FedCM. It’s primarily a declarative autofill API. You add parameters to a form, get back a token. The machinery — accounts endpoint, .well-known, service workers, Android apps — is a smaller subset of the FedCM prompts, similarly to active mode & passive mode; this is a declarative way to get email. Has the component we’ve been calling delegation in FedCM, using the browser as a holder. Does issuing and presentation separately. A different UX, from autofill. Login status is the same. We don’t use the ID assertion endpoint. We don’t reveal who the RP is to the issuer. There’s also a point of discovery that’s different. Discover issuer from DNS TXT record. From the email address, we get the issuer. I think it has properties academia might be looking for. RP accepts any IDP. I believe it can be used off the shelf in ActivityPub.&nbsp;  
* Bumblefudge  
  * Mastodon uses WebFinger, different but similar enough that you could extend WebFinger to do this. I’ve been arguing for WebFinger to be deprecated because it works like email, where you have an  account on a server. Works with Mastodon, more than ActivityPub.  
* Sam:  
  * You’re making an assertion only about ownership of a name on a server, not deliverability of email.&nbsp;  
* Bumblefudge  
  * WebFinger would support that pretty readily. Lookup&nbsp;  
* Sam:  
  * Not just that a name exists, but that the currently logged in user owns it. Alternative to email OTPs. Reuse the browser cookies with which you’re logged in to email provider to give a signed token similar to OpenIDP.&nbsp;  
* Bumblefudge:  
  * Thinking through that. I think this can be achieved with Mastodon, but not sure about ActivityPub spec.  
* Sam:  
  * My experience with ActivityPub servers is that you enter your handle into an input box, which fits well with this construction.  
* Bumblefudge:  
  * Yeah.  
* George:  
  * Curious, for people who do not. Only works if the user is already signed into your email provider?  
* Sam:  
  * No.  
* George:  
  * If I do not type in my email address, it needs browser cookies to know (PS. more about it)  
* Sam:  
  * Email address discovery can happen in a number of ways. Auto-complete works even when logged out of the provider. Synched across browser instances with your profile.. When you focus on the input field, the values you get come from a variety of sources including the OS.  
  * We can make it work with native email clients, e.g., Android app where you have your email client (so not just a web application).&nbsp;  
* George:  
  * Thinking about ProtonMail, etc. Does this work?  
* Sam:  
  * When using an IMAP client, we do not expect this to work.  
  * Working with Apple on OTP headers in email which complement this work.  
  * By email provider, I mean whoever is responsible for the MX DNS record.  
* Phil  
  * A similar thing in the academic space is student verification, e.g. for student discounts. Either do it by SAML verification or there are some services that exist that do an auth flow, extract “studentness” and pass it on more anonymously, e.g., [myUNiDAYS](https://www.myunidays.com/).  
* Sam  
  * I do think there’s a role the API can play in that use case  
* Phil  
  * Student-verified attribute, hooking into other processes. Currently, discounts often require a few steps, enter your email address, then follow other authentication steps  
* Sam:&nbsp;  
  * There’s a browser spec and an IETF spec for issuance that more precisely describes what we’re doing  
  * WICG on email verification: [https://github.com/WICG/email-verification](https://github.com/WICG/email-verification)&nbsp;  
  * IETF draft: [https://datatracker.ietf.org/doc/draft-hardt-email-verification/](https://datatracker.ietf.org/doc/draft-hardt-email-verification/)&nbsp;  
* Wendy:  
  * Chairs will discuss and come back to the proponents and groups

&nbsp;

## Any Other Business (AOB)

* &nbsp;

&nbsp;

# Queue&nbsp;

*  \<please use Zoom hand-raise\>

&nbsp;

# Attendees (sign yourself in)

* Wendy Seltzer (co-chair)  
* Christian Biesinger (Igalia)  
* Phil Smart (Shibboleth/Jisc)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* George Fletcher (Practical Identity LLC)  
* Yi Gu (Google Chrome)  
* Sam Goto

&nbsp;
