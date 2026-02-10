# FedID WG/CG Telecon, 2026-02-10

* Moderators:  Wendy

* Scribe: Heather

* Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

* Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * Volunteer as an additional editor: Emily Lauber  
* Ecosystem Updates (15 minutes)  
* Issues & PRs (35 minutes)  
  * [Discovery of Token Validation Metadata and Protocol Binding \#810](https://github.com/w3c-fedid/FedCM/issues/810#issuecomment-3852665095)  
  * [Use of apex domain is hard for organizations with different services owning different subdomains \#809](https://github.com/w3c-fedid/FedCM/issues/809)  
* Any Other Business (AOB)

# Notes

### Administrivia

* Wendy: Usual reminders plus the offer from Emily Lauber to be an editor for the FedCM spec.  
* Emily: Yes, I am interested in joining as editor for the FedCM spec. There have been a number   
* Sam: This sounds great. The Chrome team is happy to have the participation.  
* Nicolás: Same. Thanks for joining us\! We saved a bunch of spec bugs for just this moment. Will create a PR to add Emily as an editor to the doc.  
* Wendy: If there are any GitHub permissions that need to be added, let the chairs know.

## Ecosystem Updates (15 minutes)

* Sam: There are a few things happening. A week or so ago, Substack became a FedCM IdP (noticed as randomly reading the web). We’re trying to reach out to them to understand how it’s going. Also, we’re making progress on some of the stage 1 proposals. Login element is getting more defined; we’ll come back with an update. IdP initiation is getting more implementation experience and seems to be becoming more viable. Tangentially, Chrome recently (a few weeks ago) announced a Gemini integration in Chrome for an AI experience. That might be of interest as it’s setting direction for Chrome for a while.   
* Wendy: What should people search for to find those demos?  
* Sam: Will share links to the announcements. There is a blog post and also a YouTube video. It roughly looks like an LLM navigating the web on your behalf. It is largely publicly available, though some features are only open to subscribers.   
* Wendy: Thank you. That sounds like it will raise some fun issues around authorization and delegation.

## Issues & PRs (35 minutes)

### [Discovery of Token Validation Metadata and Protocol Binding \#810](https://github.com/w3c-fedid/FedCM/issues/810#issuecomment-3852665095)

* Sam: Not sure we have the person who created the issue on the call? To summarize to the group, it sounds like what they’re trying to accomplish is to make more IdPs interoperate between one another, to make the server accept IdPs and not have to write custom code for each one. They’re trying to find ways for browsers to help with that goal. Browsers can help, but there are a lot of other protocols that might help as well. This might not be something we cover until we get to registration. I don't know what the answer is, but it’s a good goal.   
* Wendy: The submitter is new to me, but anyone from the public can raise GitHub issues, and we’re glad to see it happen. More discussion will likely happen in the issue rather than on calls. Aaron has also chimed in on the issue. Anything else we need to discuss?   
* Sam: Could use more guidance from Aaron on what direction to take this. Maybe some client-side validation? Would that be at all helpful, or do we need to wait for registration?  
* Aaron: I’m not sure I understand what’s being asked here.   
* Sam: I think they’re trying to make the output of the JS call be constrained or guaranteed to interop across IdPs. One way we could accomplish this is to have the browsers make these checks, so when the IdP is building integrations, they can test against the browser; it can act as a universal client. For ID tokens, the browser could check for certain fields, or the JWT signatures; it would have to be re-checked on the server side, but the browser can check and confirm certain things.   
* Aaron: So the current approach we’ve been taking assumes the client knows what flavor of protocol it's been using, either because it knows the IdP or because it's following the OAuth profile I wrote up, but it’s not possible to discover that dynamically. Is that correct?  
* Sam: It’s arguable as to whether it can be discovered dynamically. Couldn’t there be something in .well-known?   
* Aaron: Assuming the providers have all those files, which is not a guarantee.  
* Sam: Does that happen often?  
* Aaron: In practice, you end up with clients that are hardcoded to a particular implementation or family. Bluesky, for example, has a particular flavor of OAuth and has DPoP requirements that other OAuth servers don’t. You can’t drive that entirely dynamically.  
* Sam: One way the browser could help would be to fix those parameters on the client side. Example: Bluesky OAuth will be defined, and then the browser can test for that.   
* Aaron: That makes sense, but I’m not convinced that’s the correct layer to do that sort of thing. It feels like this isn’t a new problem created because of FedCM. This question exists outside of FedCM as well.   
* Sam: Yes, but it’s one of the few opportunities where the browser layer can have an opinion.   
* Aaron: I would be interested to see what that could look like, what kind of validation steps it could do. It seems challenging.  
* Emily: I would add that I’d be concerned that the browser would be adding an intermediate layer that would require browsers to keep up with IdPs and how they are changing. If Bluesky changed its requirements not to use DPoP, for example, the browser would have to keep track of that.   
* Aaron: I would want to see a plan to address this outside of FedCM before I tried to bring it into this API.  
* Sam: That sounds like reasonable guidance. Should we apply that guidance to registration, that there will be a layer to help outside the browser?  
* Aaron: I don’t think it’s quite the same thing. With IdP registration, the path to solve that problem outside of FedCM is asking the user to create the link between the two parties. There already is a solution outside of FedCM. We’re saying it’s not ideal, but it’s possible. FedCM can make a better solution because the browser can remember the link rather than depending on the user for it.  
* Sam: Maybe we can move this issue to registration to discuss it in that context?  
* Aaron: Is this only a problem for registration, or does the problem exist for fixed config URLs as well? What he’s saying is that it does exist even if you provide a config URL.  
* Sam: It is a problem, even if you name the IdP.  
* Aaron: So it’s not a problem with registration, but it will be seen more there.   
* Sam: I can see value in doing some browser-side validation for things like id-token, if JWKs are available in an interoperable fashion. That could create a base layer of interoperability.  
* Aaron: Yes, there are a handful of things like that that would be possible, but then there are a bunch of other things that the browser could not check, and I’m not sure how valuable it would be if it can’t go all the way.  
* Sam: If the browsers can’t keep up with the changes, then it must be even harder for the RP to keep up with the changes.  
* Nicolás: Can’t they use type for that?  
* Sam: We can pick a type with specific validation rules. Right now, type doesn’t have that, but we could introduce it. But this can’t happen at the code flow level.  
* George: The impression I’m getting is that the developer wanted to write a generic library that would work with a bunch of different IdPs. Determining what the behavior is could be done through the type as long as the type referenced a standardized profile (e.g., OIDC 1.0, or OAuth 2.1). It doesn’t mean IdPs don’t add a lot of extra stuff. Not sure you’ll ever get around that. In OIDC or SAML, the id-token can be encrypted for the RP, at which point the browser can’t do anything with it. There’s probably not a lot of value for the browser trying to evaluate the implementation of the described protocol. There is value in a browser signaling what it supports. Without a certification program, your interop mileage may vary. The discovery element for an RP to determine what the IdP support does make sense, and we may need to expand that capability a bit so the IdP can describe more about itself. If the RP is talking directly to the IdP, though, you lose some of the RP/IdP privacy aspects. The main point: if the id-token isn’t encrypted, maybe the browser can do something, but I would rather find a solution that doesn’t require that the browser add another layer of validation.  
* Wendy: Sounds like we have some useful expansion on the issue; we’ll link this discussion in the comments.

### [Use of apex domain is hard for organizations with different services owning different subdomains \#809](https://github.com/w3c-fedid/FedCM/issues/809)

* Heather: I thought this was interesting and wanted to draw the group's attention to it; that’s why I added the agenda+ tag.  
* Sam: Emily, do you know anything about this deployment set up? Not sure I fully understand the problem. I empathize with .well-known being hard to set up, but are DNS records enough of a solution?  
* Emily: I don’t know enough about the DNS txt records idea. Is the use case well known?  
* Christian: The bug describes a white-label authentication service. That’s not what Microsoft does. But I do empathize with this more broadly, but I’m not sure DNS is the right answer. There is still a need to manually update the DNS just as they’d have to update .well-known. This wasn’t an issue for Google, so I am curious as to why it’s an issue for Microsoft.   
* Emily: Google and Microsoft took different architectural approaches when it comes to our domain names. Microsoft’s different products historically have their own apex domains, unlike Google, so there is a more diversified protocol. Who owns what may exist in a very different part of the company based on the product itself.   
* Christian: What you’re saying is that [login.live.com](http://login.live.com) is owned by a different team than the apex [live.com](http://live.com)?  
* Emily: One of our authentication services lives at [live.com](http://live.com). There is another, depending on the authentication service.  
* Christian: The issue is proposing a special FedCM subdomain, which might work for the Microsoft use case.   
* George: Not for FedCM, but for WebFinger, you needed to have a similar mechanism on the apex domain, and it was a nightmare to try and keep that up and running. You can play games with your routing configs, but the people who own those configs forget why the rule is in there and take it out, or they migrate to new networking gear and forget to copy it over. It’s very difficult and it becomes brittle and unstable. In OpenID discovery, we enabled redirects so all you needed to do was to get the apex domain to do a redirect to the appropriate place.   
* Christian: We do allow redirects for this file; that’s the only place we allow redirects in FedCM.  
* George: When the identity team does not own the domain, it makes it hard to keep it in sync.  
* Heather: This problem has been discussed for years in FedCM, since before there was FedCM.  
* Aaron: Since every customer in Okta has their own subdomain, the apex could not manage all that customer information. This DNS alternative solves that issue.  
* Christian: How would DNS solve that? The way it would work is that the DNS record would also be the DNS record for the apex domain. For Okta, something on [rp.com](http://rp.com) would have an SDK from Okta to make a request to [rp.okta.com](http://rp.okta.com)?  
* Aaron: We can put anything at the customer URL, but [okta.com](http://okta.com) is not in the public suffix list.   
* Christian: The problem with that setup with regards to FedCM is that it’s indistinguishable to have a subdomain per RP, but if we don’t want the IdP to know the RP.  
* Aaron: If the customers have to map their domain to Okta, then it becomes a question of how we ensure we can manage that file for them. If it’s [login.example.com](http://login.example.com), we don’t want to tell them to put a file on that web server, we want to take over hosting that file, and that’s where the DNS issue would solve that problem, because they already had to create a record to delegate to Okta in the first place.  
* Christian: I suppose it would work, but if you ever change what the .well-known file contains, the customer would have to update their DNS record; still, it’s better than putting a redirect there.  
* Aaron: I would rather they add one thing to delegate to us to serve the content rather than have them put in the values.  
* Christian: Maybe the DNS record could contain the file path.  
* Sam: Wouldn’t a CNAME work?   
* Christian: Not sure how CNAMEs work with TXT records.  
* Sam: The property that’s worth having is to find a way that if the RP can set up DNS, that will delegate the declaration to their host, which would accomplish the goals.  
* George (chat) : Pointing a DNS record to the correct .well-known file seems like a much better solution.  
* Sam: We would also be able to make this delegation if the other website created a redirect from their .well-known to Okta’s .well-known?   
* Aaron: Yes. If we’re already telling them to update the DNS record (which Okta is), adding a second DNS record is easier than separately hosting a file on their web server.   
* Christian: Would DNS records be easier for Microsoft, or does it run into the same org chart issue?  
* Emily: My understanding is yes. And while I’ve talked to the submitter, I need more detail.  
* Wendy: This reminds me of conversations going well back in DNS about the boundaries of administrative control often don’t map to the boundaries of technical control. 

## AOB

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Wendy Seltzer (co-chair)  
* Simone Onofri (W3C)  
* Sam Goto (Google)  
* Yi Gu (Google Chrome)  
* Emily Lauber  
* Bjorn Hjelm (Yubico)  
* Nicolás Peña Moreno (Google Chrome)  
* Christian Biesinger (Google Chrome)  
* Aaron Parecki  
* George Fletcher (Practical Identity LLC)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Evan Prodromou  
* 

