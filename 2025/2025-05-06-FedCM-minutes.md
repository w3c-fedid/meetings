# FedID CG/WG Telecon, 2025-05-06 

* Moderator: Wendy Seltzer

* Scribe: Phil

Call-in details: see [https://www.w3.org/groups/cg/fed-id/calendar/](https://www.w3.org/groups/cg/fed-id/calendar/)

Charter: [https://github.com/w3c/fedidcg](https://github.com/w3c/fedidcg)

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Community Group Membership](https://www.w3.org/community/fed-id/) or [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates   
  * IdP/RP implementations   
    * (tentative) Lightweight FedCM demo  
* FedCM issues  
  * [FedCM "core": break Web Platform tests between "core" and "extensions" \#704](https://github.com/w3c-fedid/FedCM/issues/704)  
  * [Decide on a format for phone numbers \#722](https://github.com/w3c-fedid/FedCM/issues/722)  
* FedCM IdP Registration  
  * [Do we need a prompt for registration? \#21](https://github.com/w3c-fedid/idp-registration/issues/21)  
* Any Other Business (AOB)

# Notes

* Wendy:  
  * Introductions, call information, W3C reminders.   
  * Agenda is eco-system updates with lightweight FedCM demo  
* Erica:  
  * Development version of Chrome  
  * An [explainer](https://github.com/fedidcg/LightweightFedCM/blob/main/README.md) exist that describes three main pieces, accounts push, optional endpoints, and config push  
  * Demo only implements only the id-assertions endpoint, no others described  
  * Login just calls login.setStatus (on the IdP endpoint)  
  * On the RP (calls lightweight FedCM), it fetches the manifest but nothing else until user selects the IdP (the accounts are pushed, the RP does not query the accounts endpoint when the dialog is shown) and calls the id\_assertions endpoint.  
* Elf:  
  * How does it work with IdP registration  
* Erica:  
  * It should work with IdP registration, but not yet tested  
* Elf:  
  * Can somebody else test this yet?  
* Erica:  
  * This is an internal build at the moment. The accounts push partially works right now.   
  * Some plumbing to make this work right now.  
  * But there is a flag that will allow you to start testing this.   
  * (PS, at least in Chrome it appears to be chrome://flags/\#fedcm-lightweight-mode).  
* Sam:  
  * Does it get the login\_url if logged out  
* Erica:  
  * Yes that works like full FedCM  
* Sam:  
  * Few more questions:  
    * What do you specify as the config url  
    * (Erica) normal config URL  
    * IdP still exposes config URL and well known file?  
    * (Erica) for now this is just accounts push. Config file only specifies assertion and login URL right now.  
    * Are you going to remove that dependency going forward  
    * (Erica) Do not require well-known for IdP registration, so that is the first step. Then the config push section of the explainer will remove the need for a config. So get to the point the RP only needs the base URL for the IdP and then it uses the matching IdP config that was pushed.  
* Wendy:  
  * Thanks\! File issues if required.  
  * Any other eco-system updates?  
  * Issues:

[https://github.com/w3c-fedid/FedCM/issues/704](https://github.com/w3c-fedid/FedCM/issues/704)

* Nicolás  
  * Wrong issue. The correct one is [https://github.com/w3c-fedid/FedCM/issues/703](https://github.com/w3c-fedid/FedCM/issues/703). features having separation between them. Single repo for extensions and individual shared files (HTML) for each separate extension.  
  * Any objection?  
* Sam:  
  * Single bikeshed for core and individual ones for each extension?  
* Nicolás:  
  * Single repo for all extensions  
* Sam:  
  * Do we not have a specific repo for the fields API?  
* Nicolás and Sam:  
  * Maybe not.  
* Sam:  
  * Reason for asking, one of the benefits for individual repos is that you can file issues per feature.  
* Nicolás:  
  * Different from feature incubation  
* Sam:  
  * Specific repos get closed once they transition to the extensions repo.   
* Nicolás:  
  * One repo per feature is making it hard to find everything, and the permissions are harder. It is not working well. So one repo for extensions seems better.  
  * Can also use labels if required.  
* Sam:  
  * Figure out what happens to repos after incubation. Fields API some disuccsions were things are incubating, but then others might happen in the extensions repo later on. So do we want issues in both repos? Moving to one is better.  
* Nicolás and Sam and Christian  
  * (PS a bit of a summary, please check) Move to a place people can have a discussion without figuring out all the places is best  
* Nicolás:  
  * Extensions do not mature. The main question was, one repo for all extensions or repo per extension. Going for one repo for extensions with many HTML documents.  
* Wendy:  
  * Check that everybody is happy

[https://github.com/w3c-fedid/FedCM/issues/722](https://github.com/w3c-fedid/FedCM/issues/722)

* Ben:  
  * Tel needs to have a proper format, or leave as a fully open String? I’ve no great opinion.   
* Christian and Ben:  
  * We do not valid email addresses. Should the browser validate it, or the IdP?  
  * (Ben) I agree, leave it open with no particular validation  
  * (Elf from Chat): There is also the tel URI for Telephone Numbers [https://www.rfc-editor.org/rfc/rfc3966.html](https://www.rfc-editor.org/rfc/rfc3966.html)  
* Sam:  
  * Feedback from the TAG to align with HTML autocomplete taxonomy.   
  * Align with claims from OpenID connect, or SAML (PS, there are various schemas people use)  
  * Or, Align with HTML5.   
  * We want to connect some of this data with autocomplete.  
  * Allowing a freeform field will not corner us, but good to check.  
* Wendy:  
  * Any other questions or comments on 722?  
  * … none

[https://github.com/w3c-fedid/idp-registration/issues/21](https://github.com/w3c-fedid/idp-registration/issues/21)

* Sam:  
  * From TAG, do we need a prompt for IdP registration?  
  * Prompts are awkward. Changes the user flow. So find a way we do not need a prompt. But if no prompt, risk of abuse and spam.   
  * Do we want to prompt the user? Maybe we can start with a prompt and see what people think.  
  * Martin in the TAG was suggesting different ways…is more an abuse issue than privacy.  
* Nicolás:  
  * Know from IdPs or RPs. Is the API more or less useful with the registration having a prompt?  
  * RPs surprised to show IdPs they did not expect (they were registered by the user visiting an IdP without the prompt).   
* Elf:  
  * The initial reaction, explicit reaction, is to require prompt.   
* Sam:  
  * Without the prompt, any site can register without the user knowing.  
  * Can you expand, Elf, on why you prefer the original over no prompt  
* Elf:  
  * From Solid IdP perspective, we require IdP is part of the rest of the eco-system  
  * Spamming also an issue  
  * Slows down the adoption  
* Ben:  
  * Makes sense *not* to have the prompt.   
  * The constraint of accepting the registered IdP is in the pre-registration. Search string ‘any’ or ‘indieauth’. No security or privacy gain of requiring the browser API prompt. Keep it in page content.  Abuse angle, but that is an eco-system problem for federated identity.  
* Sam:  
  * Not mutually exclusive. May both are valid.  
* Nicolás:  
  * Both is not beneficia (PS, not a good idea)l.   
* Elf:  
  * Maybe I was too cautious. User only accepts IdPs that  
* Phil:   
  * Initially agreed with elf’s position In federated scenario, you could register, but without pre-established trust, it would fail. If you get the registration prompt, user probably doesn’t understand, just clicks yes. Not sure how you’d construct a suitable prompt if you had to.   
* Wendy:  
  * Does a prompt convey meaningful information  
* Sam:  
  * registerProtocolHandler prompt is one analogy.   
* Elf:  
  * Prompt is a bit disconnected in terms of the UX.   
* Wendy:  
  * Still needs discussion.  
* Nicolás:  
  * Will try to summarise the discussion in the issue.  
  * Will ask in the issues.  
* Elf:  
  * In Solid use verified email, we need to consider IdP phishing and other security considerations.  
* Nicolás:  
  * Somebody knowing your email and using that?  
* Elf:  
  * RP uses the fake email from a malicious IdP, and then sends a password reset to the fake email address.  
  * RP may assume user trusts the IdP because it has been registered.   
  * But the user may use a malicious IdP controlled email, the RP will trust it because it was registered (if user was tricked into using it)  
* Wendy:  
  * We are at time. Thanks  
  * Plan a hybrid meeting alongside the IETF meeting week of 21st of July? If anybody has office space to help us host a meeting, that would be great. No IETF space for it as a WG/CG meeting.  
  * 

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Chris Fredrickson (Google Chrome)  
* Erica Kovac (Google Chrome)  
* Christian Biesinger (Google Chrome)  
* Phil Smart (Shibboleth/Jisc)  
* [elf Pavlik](https://elf-pavlik.hackers4peace.net) (independent, Solid CG)  
* Simone Onofri (W3C)  
* Alex B Chalmers (independent)   
* Benjamin VanderSloot (Mozilla)  
* Andrew Regenscheid (NIST)  
* Yi Gu (Google Chrome)  
* Emily Lauber (Microsoft Identity)  
* Alan Buxey (MyUNiDAYS Ltd.)  
* Wendy Seltzer (co-chair)