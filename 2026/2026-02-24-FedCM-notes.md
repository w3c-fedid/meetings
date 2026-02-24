# FedID WG/CG Telecon, 2026-02-24

* Moderators:  Heather

* Scribe: Phil Smart

* Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

* Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * Reminder: DST clock skew coming up from 8 March through 5 April  
* Ecosystem Updates (5 minutes)  
* Discussion (45 minutes)  
  * [FedCM](https://w3c-fedid.github.io/FedCM/) and the [WG/CG process](https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md)  
  * [IdP Registration](https://github.com/w3c-fedid/idp-registration)  
* Any Other Business (AOB)

# Notes

### Administrivia

* W3C Code of Conduct.  
* DST changes starting March 8th…  
  * Calendars might help

## Ecosystem Updates (5 minutes)

* Joel, Shopify  
  * Over the last couple of weeks, prototyped the delegation API and metrics API.   
    * Not formalised prototype feedback yet, but work is ongoing.  
    * Excited about the Metrics endpoint  
* Sam:  
  * Can you file issues for anything you’ve found that does not work.   
    * Delegation has a repo, but Metrics API does not.  
  * Where do we go from here?  
* Joel  
  * I can give feedback on the Metrics API, a few gotchas in the documentation.  
  * On the browser vendors to move this forward  
    * More browser vendors to participate, to find a larger audience  
  * Sam?  
* Sam:  
  * Sounds right. Chrome would be happy for an Origin Trial. You’ve been using a Dev Trial (flipping flags). Origin Trial allows users to test it.  
* Joel:  
  * From the user's perspective, what is the difference if delegation and mediation  
* Sam:  
  * There is none, but we could change the UX as a different privacy bar  
  * Get more confidence when we put this in front of users; privacy and UX bars we can gauge during an Origin Trial.   
* Joel:  
  * If Origin Trial is the way to move this forward, sure. I need to spend some time making sure it is ready. If this is the most effective way to bring delegation-oriented to more users then I am all for it.  
* Sam:  
  * Can you work toward production, security, and privacy review with Shopify to see if ready, and we can do that on the Chrome side? Once complete, we can decide if we need Origin Trial or straight to production.  
* Joel:  
  * Benefits on Origin Trial for Metrics API?  
* Sam:  
  * …  
  * Origin Trials help see developer demand, we do not want to ship things that are not used.  
  * Let’s look to move on delegation-oriented and metrics API, but productionising them may be the next step.  
* Heather:  
  * Write this down in the various issues e.g. there is a Metrics API issue  
* Achim:  
  * The delegation model is like the holder model. The IdP will not know what the user is logging into.   
* Sam:  
  * There are things used in delegation not used in mediation and vice-versa, e.g., approved clients, maybe client id metadata.  
* Achim:  
  * There are changes to the function and the UX. How do we inform the user of what they are logging into, etc? *(P.S. Other things that need thinking about.)*  
* Sam:  
  * First-time presentation vs. a recurring one is different.  
* Achim:  
  * … *(P.S. did not catch)*  
* Sam:  
  * This is a complex topic and should have its own discussion.  
* Theo:  
  * Was at FOSDEM: Talked about FedCM. Creating a video and webpage to explain it. Including the IdP Registration API. video: [https://www.liquid.surf/fedcm](https://www.liquid.surf/fedcm).  
* Sam:  
  * There are materials we have collected over the years; we should collect them, and it would be cool to add this. 

## Discussion (45 minutes)

* Heather:  
  * Step back and talk about the features of FedCM.  
  * Talk about how new features get added.  
  * What is still being worked on, and what is currently there? (See the list below)  
  * Are these all still useful things? Please take a look when you can.  
  * Nicolás can you check I’ve not missed anything?  
  * Want to talk about IdP Registration (see below)

### [FedCM](https://w3c-fedid.github.io/FedCM/) and the [WG/CG process](https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md)

* Developer docs: [https://developer.chrome.com/docs/identity/fedcm/overview](https://developer.chrome.com/docs/identity/fedcm/overview)   
* Associated APIs  
* [IdP Registration](https://github.com/w3c-fedid/idp-registration) (Stage 1\)  
* [Multi-IdP API](https://github.com/w3c-fedid/multi-idp) (stage 2\)  
* [Metrics API](https://github.com/w3c-fedid/FedCM/issues/352#issue-1386737182) (maybe ready for Stage 2\)  
* [Delegation-oriented FedCM](https://github.com/w3c-fedid/delegation) (Stage 1\)  
* [IdP-Initiated](https://github.com/fedidcg/idp-initiated) (Stage 1\)  
* [login-element](https://github.com/fedidcg/login-element) (Stage 1\)  
* [Native-app-IdPs](https://github.com/fedidcg/native-app-idps) (Stage 1\)  
* [Lightweight FedCM](https://github.com/fedidcg/LightweightFedCM) (Stage 1\)  
* [Login Status](https://github.com/w3c-fedid/login-status) (Stage 1?)  
* Add Account API (now merged as part of FedCM)  
* Error API (now merged as part of FedCM)  
* Active Mode API (now merged as part of FedCM)  
* Multiple configURLs (now merged as part of FedCM)  
* Account Labels API (now merged as part of FedCM)  
* Continuation API (now merged as part of FedCM)  
* Params API (now merged as part of FedCM)  
* Fields API (now merged as part of FedCM)  
* If you’d like to join the W3C Community slack and the \#fedid-cg or \#fedid-wg, go to [https://www.w3.org/slack-w3ccommunity-invite](https://www.w3.org/slack-w3ccommunity-invite) 

### [IdP Registration](https://github.com/w3c-fedid/idp-registration)

* Sam:   
  * Update on this. IdP Registration allows an RP to ask for ‘any’ IdP, not just specific ones. There is an implementation behind a flag in Chrome (various flavours).  
  * The UX model for permissions needs finalising. Thinking about not needing any permissions at all, and dealing with abuse in the settings page. As people try it, we will see how this works.  
* Heather:  
  * Questions or discussions for people trying to implement it  
* Sam:  
  * Other aspects of this we’ve heard from Solid CG, BlueSky? (and others, including IndieWeb). Individuals want their own identity, identity wallets, etc. Bring your own identity to websites.   
* Tim:  
  * Comment on silent IdP registration. Some blowback from conditional passkey creation, creating without a prompt. So fyi that could be an issue here.   
* Sam:  
  * I share your concern. Worry about not having permission.   
  * Registering your IdP is so decoupled from using it, it is hard to communicate this to users.  
  * Could become an abuse vector, so a permission might make this harder.  
* Tim:  
  * Halfway, notification that it actually happened.  
  * Chrome shows passkeys have been created, etc.  
* Sam:  
  * Does not feel like an irreversible decision; if we want to later have more explicit consent, we could add that.  
* Tim:  
  * No fundamental concerns, just wondering about the reaction…from users who are also developers are vocal.  
* Bumblefudge:  
  * Wondering about Tim’s point. Reference to IdP settings in the demo video, how do we align the settings about where you go to revoke things?   
  * Is this something people talk about in advance, or retrospectively (alignment on settings).  
*  Nicolás:  
  * Don't usually talk about this. Browsers have a lot of autonomy about how they interact with users. Would not mandate what this looks like.  
* Bumblefudge:  
  * Not design language; a use case, not a visual design  
* Nicolás:  
  * How do settings refer to the use case  
* Sam:  
  * They are linked to use cases; a user should be able to remove an IdP that was manually registered. There should be a place a user can go to do that.  
* Nicolás:  
  * We could have that in the spec, but we do not want to mandate UI for user-agents.   
  * We could say, there has to be a way for the user to disable this, … etc.  
* Sam:  
  * These calls are for us to learn from people trying to deploy this. For Chrome to learn from that feedback.   
  * Some of these use cases are for advanced use cases, not just the typical user cases. We can learn that from these calls.  
* Bumblefudge:  
  * I was not asking because I have a strong opinion. Some kind of non-normative description could be good  
    * From chat: ‘Maybe it's just a non-normative paragraph in Privacy Considerations or something’  
* Sam:  
  * Encourage us as a group to figure out what we want it to do.  
  * Not clear to me that not having any permission at all is the right way to go.  
    * Not having permissions might be a good way to go as well.   
  * Abusing the API will degrade the value of the API. Any website could register, and you might lose real IdPs in a long list of irrelevant IdPs.  
* Tim:  
  * Fear is that we solved the NASCAR problem, but now made it 100 times worse.   
* Sam:  
  * Not everybody has their own blog or wants to bring their own identity. Hard to design things for a common web user.   
  * What question do you ask the user when the IdP gets registered  
  * This is for an advanced user of the web  
* Theo:  
  * From FOSDEM. European Commission into decentralised technology. Might see more of this in Europe.  
  * Is abuse the main blocker for IdP registration?  
* Sam:  
  * We've not had anybody use it yet. That is the biggest blocker.  
  * IdPs using it, Not found RPs that want to use it  
* Aaron:  
  * AppProto community can help here.  
* Sam:  
  * Aaron do you know where they are with registration?  
* Aaron:  
  * AppProto has a solid OAuth foundation.   
* Bumblefudge:  
  * A bit slow-moving.  
  * Devs sometimes need to catchup  
  * Tried to get those folks to attend this call, but a bit short notice  
* Sam:  
  * Questions: Happy to join a call about AppProto.  
  * Question: How does OAuth work in BlueSky?  
* Aaron:  
  * BlueSky app is the RP. What the user interacts with.  
  * Clients needs access to your data in the PDS  
  * PDS is IdP and issues tokens for access to data  
  * There is currently a user prompt, but we can skip that with FedCM  
* Sam:  
  * I tried this last week. Enter AppProto PDS, then your username and password?  
* Aaron:  
  * Account for PDS (Personal Data Server), BlueSky hosted front-end.  
  * Client does discovery via PDS, then password to your own PDS, then client gets the token  
* Sam:  
  * I have my own PDS, and managed to log in to BlueSky with my own PDS. But could not see OAuth  
* Aaron:  
  * Correct, (correction) clients still needs password directly. Still does not support OAuth flow.  
  * There are some routes to using OAuth. OpenVibe?  
    * (Bumblefudge) See: https://leaflet.pub/  
* Sam:  
  * Would be good to have OAuth support in BlueSky app.  
  * FedCM could play a role in IdP discovery. Saves time of user having to enter your userHandle in input box.   
* Bumblefudge:  
  * For a while, you had to give your password and PDS domain. That was a bad UX.  
* Sam:  
  * Can we continue this, please?  
  * Heather, can you help determine if they come here or we go there (P.S. to one of their WGs)?

## AOB

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Joel Antoci (Shopify)  
* Nicolás Peña Moreno (Google Chrome)  
* Bjorn Helm (Yubico)  
* Yi Gu (Google Chrome)  
* Achim Schlosser (Bertelsmann)  
* Theo @thhck  
* Tim Cappalli (Okta)  
* Isaiah Inuwa (Bitwarden)  
* Phil Smart (Shibboleth/Jisc)  
* Aaron Parecki (Okta)  
* George Fletcher (independent)  
* Christian Bormann  
* Bumblefudge

