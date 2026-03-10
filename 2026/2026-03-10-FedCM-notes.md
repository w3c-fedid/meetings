# FedID WG/CG Telecon, 2026-03-10

* Moderators:  Heather

* Scribe: Theo, Emelia

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
  * FedCM Core  
* Any Other Business (AOB)

# Notes

## Administrivia

* 

## 

## Ecosystem Updates (5 minutes)

* Emelia: Bluesky gave me a grant to work on Fedcm for a year. For all decentralized ecosystems, so also Solid, IndieAuth, and ATproto. The goal is to push the decentralized FedCM. In particular the grant contract language requires collaboration across different protocols and communities interested in federated and decentralized identity, naming in particular Solid, IndieAuth, and AT Protocol, but also including others.  
  * [https://atproto.com/blog/working-to-decentralize-fedcm](https://atproto.com/blog/working-to-decentralize-fedcm)   
* Theo: I’m working on a test suite to make FedCM work with Solid and will try to make it generally useful for other ecosystems. One of the trickiest parts is the token endpoints, work in progress. I’ll share a link, [https://github.com/Liquid-Surf/fedcm-test-suite](https://github.com/Liquid-Surf/fedcm-test-suite) 

## Discussion (45 minutes)

[FedCM Core](https://github.com/w3c-fedid/FedCM/issues/703)

* Heather: Explaining that W3C TAG had a meeting last monday (?) and the relation to FedCM and third-party cookies (?). Heather gave them some background and gave them the sheer breadth that FedCM covers. One participant mentioned that FedCM was so large his company was intimidated to implement it.  
* Heather: FedCM Core is designed to be a common set of functionality for what FedCM is. One issue with creating a “Core” is that, with only Google implementing it, it results in all of FedCM being “Core” from Google’s perspective.  
* (Npm?): What do you mean by reviving ?  
* Heather: We go through the issues and we talk about stage 1 that we’re considering, but we haven’t gotten to making core a CR.  
* Npm: Core needs other browser agent opinions, but they are not here today. I'm wondering how much time we should spend on this, since they are not active at this moment.  
* Heather: Opens the floor to others for response.  
* Emily: Is the feedback that you heard in the TAG meeting that FedCM was so large that having FedCM Core go to CR sooner would support implementers?  
* Heather: Yes, correct  
* Emelia: What do we define as Core? For me, Core would need to work for decentralized web, since that’s critical to me. Microsoft, Google, etc., might be different and only need a core to work with one IdP. It might be hard to define a “Core” that is suitable for everyone.   
* Heather: We address some of that, including multi IdP etc.. There is an old wiki page that captures that.   
  	[hlf@sphericalcowconsulting.com](mailto:hlf@sphericalcowconsulting.com) — Could you add a link to that page?   
* George : I agree with Emelia, what is the critical user experience we want to have, and start from that, not the technology.   
* Tim: \+1 , one exercice would be to create differents users profile, a decentralized profile, etc., and see what is in common to all of them to define Core  
* G: When you do that, the core we deliver might not work for anyone. We want to improve the user experience over redirect flow, but some may be better being told “stick with your redirect flows”. But I agree with defining profiles.  
* Tim: Define a minimal set of features and then define the profiles. The hardest part is to define the minimally viable user experience.  
* Sam Goto: \+1 to everything said. In particular George, should start from the user exp. Initially we have defined Core from the browser perspective, but that might lead to a user exp that is not viable. But if we start from the user, then the RP, and lastly the browser — that seems to be the viable path instead of the other way around. I believe “idp-registration” was part of Core, as Firefox implemented it. That might lead to more work on the browser side, but it is the right path.   
*  Emelia: Do we have a living explainer of all the proposals and what is part of Core or not ? a big table of everything to have a quick overview ? Would it make sense to have such a page ?  
* Sam: We have the baseline spec. We have an "extension" part, for example, that was too much work for Firefox to implement  
* Emelia: I was not able to find such a page. I was referencing the list from the last meeting agenda, and wasn’t sure if there was something better to refer to.  
*  Heather: (will find the link ) : [https://github.com/w3c-fedid/FedCM/wiki](https://github.com/w3c-fedid/FedCM/wiki)  
* Emily: (?)  
* Heather: Where would we put such a document?  
* Emilia: is there a “main repo” ? Could it be on the main FedID GitHub page ? Mastodon has a readme for the whole organisation  
* Heather: What other browser vendors think about it is still an open question. We would like to have them come back and have their opinions reflected.  
  * Possibly [https://github.com/w3c-fedid/FedCM/wiki](https://github.com/w3c-fedid/FedCM/wiki) 

## AOB

### [Enterprise Scenarios: admin consent for users](https://github.com/w3c-fedid/FedCM/issues/715#top) \#715 (Deferred)

* Heather: I thought Emelia had a good comment about whether the Step-Up flow would help for this particular use case  
* Emelia: Can we defer as I’d like to prioritise the FedCM for Decentralized Ecosystems since we have both Solid and ActivityPub representatives on the call?

### FedCM for Decentralized Ecosystems

* Emelia: I’m still getting up to speed with this Grant. I’ll be at the Solid CG meeting tomorrow, as well as the next Social Web WG/CG meeting or the ActivityPub API meeting (sorting this out with Darius as to what makes sense).  
* Emelia: I also had a conversation started with Aram Zucker-Scharff (W3C member from the  Washington Post) who has shown interest in FedCM and in particular the IdP-registration part. (I have a call with him on Monday 16th)  
* Emelia: I’m also trying to organise a call with Aaron Parecki from IndieAuth (also with regards to OAuth CIMDs).  
* Evan Prodromou: (towards Sam), What are you expecting from this discussion?  
* Sam Goto: Curious to hear about how AP is doing, number of users, servers, what are the challenges FedCM can solve? High level overview.  
* EP: AP is a distributed social protocol, letting the user create accounts on different servers. The last numbers: 43000 servers (approximately 12.7 million accounts). A typical flow for the user is to mainly have interaction with their own server, which will use the AP protocol to communicate with other servers. But it's also possible for a user to browse other servers and interact with posts. Right now, this can be difficult to impossible: Mastodon uses a redirection-based system to pull you back to your own server to do the interaction from there, but not on all servers. And Mastodon needs users to type their own server URL, which is cumbersome. It would be great to have FedCM do that automatically, to ease the flow.   
  * “Remote Interaction” is what this is called, and it redirects you from a remote server to your home server.  
* SG: What happens after a user enters their username in another server? Is it OAuth or Mastodon-specific?  
* Evan: It is not an OAuth process; it is actually just a custom redirect.  
* Emelia: Mastodon has implemented a new spec to standardise this flow, where there is a redirect to your server and then possible back again. This new spec proposal is called Activity Intents which is not OAuth, but models on it, working with redirection. This supersedes their previous OStatus based flow. It has been merged to Mastodon.  
  * [https://codeberg.org/fediverse/fep/src/branch/main/fep/3b86/fep-3b86.md](https://codeberg.org/fediverse/fep/src/branch/main/fep/3b86/fep-3b86.md) Activity Intents shipped in Mastodon today  
  * Mastodon are also now a W3C member organisation.  
* Emelia: The main issue with doing OAuth with Mastodon: if a random server shows a post, if you click the like button, that triggers an OAuth flow, and that random server has a token with a full “write status” scope. This encourages users to trust any website and give a large scope to random servers, which is a security issue. Also Mastodon tokens live forever, which is also dangerous. The Mastodon API is not standardized. If I build an app for events, mastodon doesn't understand what a “create event” is, Mastodon is not a generic AP implementation.  
* Emelia: OAuth doesn’t really work for the Mastodon use case for the moment, due to security concerns. I wrote a [roadmap](https://github.com/mastodon/mastodon/issues/34316) for the OAuth aspect of Mastodon, but none of it has been fully implemented yet, and the only aspect Mastodon has actively shown interest in was adopting CIMD documents over their form of dynamic client registration. When reviewing the activity intent (FEP-3b86) proposal, the issues around OAuth security were forefront and that’s what led to my recommendation not to use OAuth here, but to just do a redirect flow that is protocol-native, so “create this event” or “like this post”. There is a future where AP API is standardized and implemented, however, but that’s a long way off as work on AP API only started in September 2025\.  
* Emelia: WordPress has an AP plugin, which started as using Server to Server activitypub, but they have recently been implementing the OAuth aspect for the AP API, but it is still WIP and will take time for adoption. From the FedCM side, the thing we can do is to make the FedCM API have selective disclosure not of a credential, but an identity: you would receive a unique identifier, and a username or other fields. This would mean we could use FedCM to kick off the activity intents flow more easily without needing the user to type in their home server URL or username.  
* Sam: FedCM is protocol-agnostic, doesn’t need to implement OAuth, can return whatever you want. The credential returned is just a string. There is a way to help AP even before they decide the specifics of their implementation. We have selective disclosure and it’s called “field”, for example. Username. There is a way to deploy this to AP with its current state.  
* Tim (from chat): just because the API is protocol agnostic, doesn't mean you shouldn't define a protocol. without a protocol, it's not interoperable. I would assume flexibility for the browser and definitions required for RP & IDP  
* Emelia: For ActivityPub, ATproto, and Solid,  you need the unique identifier along with the username. (AP doesn’t have a concept of a “username” that is globally unique; that is achieved through an extension that combines ActivityPub and WebFinger). For ATproto, we have an identifier as a DID, and also a handle. For Solid, we have a WebID document which has a URI (identifier) and then that document can contain other data (name, username, etc.).  
* Evan: There is plenty of opportunity to use OAuth flow with AP. Might not be advisable in certain flows to use it. Long term, it would be very useful to go with OAuth.  
* Emelia: OAuth here has the issue of trusting an arbitrary server with significant access to your account, and there is a concern for token theft, which the DPoP spec prevents. DPoP is pretty essential for decentralized OAuth. ATproto OAuth requires DPoP, as well as Solid-OIDC. AP should probably require DPoP too.  
  * There is also an idea to work on an OAuth profile document based on AT Protocol’s OAuth specification profile, and take that to the OAuth WG at the IETF.  
* Sam: Evan: What is the concrete next step we can take ?  
* Heather: times up ,   
* Evan will follow up next meeting on that question

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Theo [@thhck](https://github.com/thhck)  
* Nicolás Peña Moreno (Google Chrome)  
* Christian Biesinger (Google Chrome)  
* Emily Lauber (Microsoft Identity)   
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* George Fletcher  
* Bjorn Hjelm (Yubico)  
* Wendy Seltzer  
* Tim Cappalli  
* Sam Goto  
* Evan Prodromou  
* Emelia Smith

