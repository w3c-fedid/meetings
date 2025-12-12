# FedID WG Telecon — DC API Series B, 2025-12-10

* Moderators: Heather Flanagan

* Scribe: Rick Byers

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia (5 minutes)  
  * Scribe volunteer?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/participants/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/20240318/)  
* Ecosystem Updates (10 minutes)  
* Using CoPilot, Gemini, and other tools  
* [Security Considerations](https://docs.google.com/document/d/1BpBBiv7GgkGi1_Y7NvyD3Mkalj0g857Qw-aan3NqYwU/edit?tab=t.lgu8jgz2n99n)  
* Discuss [TAG Review](https://github.com/w3ctag/design-reviews/issues/1119#issuecomment-3616144896)  
* DC API Issues & PRs   
* Any Other Business (AOB) (15 minutes)

# Notes 

## Administrivia

* 

## Ecosystem Updates

* Marcos: Moahmed and I have been refactoring the test suite. Found a bunch of bugs on the WebKit side. Going well. Have a more robust test suite now. Works towards integrating the changes we're making with the registry and other things we've landed in the spec recently.  
* Marcos: WebKit implementation had the old OpenID string in it, which the test suite had. WebKit will remove the fake OpenID implementation (dead code) and if and when we do it again we can do it properly. If people see me removing OpenID, it isn't a sign of non-commitment, just removing old code. Was just empty stuff being passed around for no reason, so now opens the possibility of doing this properly.  
  * Rick: Was this related to the change to make Webkit succeed if presented with both OpenID and Annex C?  
  * Marcos: That should already work.  
  * Tim: No it doesn't and it's really bad for RPs.  
  * Mohamed: Final test will check this.  
  * Marcos: Then I'll have to fix WebKit to match the spec. Once I fix that, WebKit will align with the spec in this regard.

## Using CoPilot, Gemini, and other tools

* Heather: I'm not a developer but I've noticed how chatty the AI tooling is. Need to sort out how we're going to use it. Marcos, you've appreciated using them. Is there a way to make them less chatty?  
* Marcos: I've been trying to use CoPilot to check procedural things. like. did you use ReSpec properly, things I would normally check for in doing a review. Once it's set up, yes, it was pretty chatty. But once it's in place, it's not that chatty, and the things it is chatty about tend to be 95% right. Machines are better than humans at catching these things. Tried to set up "this is how you check a W3C spec".  Went over with Mohamed whether we should use CoPilot, Mohamed suggested maybe we should use Gemini. Don't really have an opinion. Primarily not for local, more for server.  Once we set it up, it would check everybody's pull requests. But can also save a bit of time on the client side.  
* Rick: I got the impression that only people paying for LLM subscription can invoke the agent. Can any uploader invoke the bot without a subscription?   
* Marcos: Github gave me unlimited access without any payment. I don’t know if that applies to others. Free tier should be sufficient  
* Rick: I need to understand how we can use it and then Google folks will have to get approvals to use a non-Google AI  
* Mohamed: I think where it was getting annoying for people was when we started to ask CoPilot for help and all others got messages which are annoying as notifications. I think this is what we need to agree on.  
* Marcos: Guess we could do that on a private branch in our own repos. I'm happy to do that.  
* Matt: Do we have to worry about copyright or anything?   
* Marcos: No, we're not asking it to write anything. We're just asking it to check stuff.   
* Matt: But if the checking of it leads to suggesting text, and that makes it into the spec, will that be a problem?  
* Marcos: Not at a level that should matter.  
* Heather: I've asked Simone, and the W3C team says that as long as output is used for review, not authoring, then it's OK, if the WG agrees.  
* Matt: Will it be a requirement that PR authors respond to AI generated feedback?  
* Marcos: There's no reason not to run it, kind of like running a spell checker.   
* Matt: I respectfully suggest that it's different from a spellchecker due to its non-determinism. I may not want these systems to pretend to have the intelligence we have. I would hate to have to engage with a chatbot just because this WG decided it's required.   
* Marcos: It can save a tremendous amount of time, means I don't need to follow up on things.  
* Matt: Is what has been submitted that difficult to understand that a human can't do it?  
* Marcos: If you look at the PR it's just checking procedural things like using ReSpec properly, etc. Things we would normally check.   
* Heather: Can you point to a PR that you believe it's done well?  
* Marcos:Yes.  A lot of the time it doesn't say anything because everything is fine. See \#407  
  * \<Enumerates what it checks for in the PR\> [https://github.com/w3c-fedid/digital-credentials/pull/407](https://github.com/w3c-fedid/digital-credentials/pull/407)  
* Wendy: I see Nick saying for example reviewing privacy and security considerations is more than a spellchecker / deterministic review. Who is expected to review the output that the LLM gives?  
* Marcos: Primarily me.  
* Heather: Why you when there are 3 spec editors?  
* Marcos: I like it. Editors could do it, others could too.  
* Wendy: So the author of a PR isn't necessarily responsible for reviewing all of that? Other human reviewers aren't necessarily responsible for that. Is it adding extra burden for other people in the workflow?  
* Marcos: It shouldn't, but it will catch things that people need to fix.   
* Matt: One thing that would be sad is if a PR gets out of its author's control because reviewers decide that the LLM is saying what it should be. I just don't want to see there be a deference to LLM output about what makes a good PR over what the author / other reviewers think. Why do we think LLMs will be smarter than industry experts? If the ultimate decision is to use LLMs, I would hope it would be an option for the author to opt into. If another human says "yes, this is valid feedback, I think you should make this change", then that is what would trigger the work. That feels like an appropriate workflow. As opposed to "you need to do that because the LLM says you need to". I just want to keep the humans in the loop. I'm worried it'll turn into a nonsense waste of time.   
* Heather: One thing that made me uncomfortable is: my expectation is that when an individual submits a PR, people will comment on it, but the responsibility for making changes should be the PR author. Marcos, you said you'd use it to make changes to a PR, and I don't think that's right at all; should be on the author.  
* Marcos: Yes, I think I misspoke. I didn't mean it would have control. Of course it's on the author. It gives you suggestions, but there's no magic. I think Matt's taking it to the extreme where all the checks we're doing are very simple and we can refine them. We can change the rules for the AI; there's no taking the humans out of the equation or devaluing them. Wouldn't it be nice if there was a tool that could do the annoying grunt work, freeing us to do more interesting stuff like writing the actual spec text.  
* Heather: Is it possible to suggest that we'll try it out for a couple months and if you're going to be engaging in a lot of back and forth, then please do it in a private branch and iterate there before submitting it.  
* Marcos: Yes  
* Heather: Anyone object?  
* Tim: I have no problem with you triggering this later, but I don't want it going automatically on my PRs. It's super annoying. One had 39 comments before a single human looked at it, we're going to lose the human conversations in these.  
* Marcos: That's so rare, we do want to check all these things before landing.  
* Tim: I think my proposal can work that way. If you want to run it, that's OK. If my inbox gets flooded with 100 messages from one PR, then my timely response to reviews will go down.  
* Heather: I'm hearing some rough consensus. Using LLMs to check is a good idea. If you're going to do a lot of back and forth, do that in a private branch. And only invoke when you want it, not at the start.  
* Marcos: I can live with that.  
* Tim: And if it turns out not to be crazy we can turn it on automatically. But you turned it on without asking anyone and it drove us nuts so left a bad taste in our mouths.   
* Marcos: I can merge in the thing and then it will not do automatic reviews anymore.   
* Tim: In the action there's a manual trigger.   
* Marcos: Ok, I've removed that so it won't do it automatically.   
* Heather: Mohamed, are you ok with this?  
* Mohamed: Thumbs up

## [Security Considerations](https://docs.google.com/document/d/1BpBBiv7GgkGi1_Y7NvyD3Mkalj0g857Qw-aan3NqYwU/edit?tab=t.lgu8jgz2n99n)

* Heather: I think we're waiting on this one. Marcos, not sure if you saw the latest on this document that we're waiting on? [https://docs.google.com/document/d/1BpBBiv7GgkGi1\_Y7NvyD3Mkalj0g857Qw-aan3NqYwU/edit?tab=t.0](https://docs.google.com/document/d/1BpBBiv7GgkGi1_Y7NvyD3Mkalj0g857Qw-aan3NqYwU/edit?tab=t.0)  
* Heather: When we met about this a couple weeks ago, the table that is an index of the threat model, people didn't feel we went too far in making it as succinct as possible to the point it wasn't useful anymore. I took the threat model table and spec and threat model guidance, and sent it to ChatGPT, and said make one. So I wanted your take on whether it's better or worse, worth keeping?  
* Marcos: I'm going to meet with Simone tomorrow and start going through it. I have an opinion on how these should be done from other specs, so I'm happy to continue working with Simone and Mohamed. I can also look at the LLM output.  
* Heather: As you said, we don't want an LLM writing the spec text, but I was trying to break through the "this is too long," "this is too short," etc.  
* Mohamed: Update I've been working with Simone and I think we've resolved the outstanding agreements. In 9 hours we will meet with the researchers and agree on which of the formats we want to settle on. Will have an update next call.   
* Heather: Ok sounds like a good update. Any other questions / comments?

## Discuss [TAG Review](https://github.com/w3ctag/design-reviews/issues/1119#issuecomment-3616144896)

* Heather: Got back a TAG review: [https://github.com/w3ctag/design-reviews/issues/1119\#issuecomment-3616144896](https://github.com/w3ctag/design-reviews/issues/1119#issuecomment-3616144896). Anything there we need to discuss?  
* Marcos: From my perspective, not really. We can discuss the larger societal issues but from my perspective there wasn't anything actionable. I encourage others to take a look and file bugs if anyone thinks there's anything actionable.  
* Matt: As author of accessibility considerations, my ears peaked up when they commented on it. But I wasn't sure what needs to be brought back. E.g., they said there should be "must" but the text reflects that a spec can't really mandate what the client does. Do we need to try to bring that back?  
* Marcos: We could ask for a proper accessibility review? It may be an indicator that it's a little thin and could be padded out. I'm not particularly concerned. TAG was confused about where WCAG applies and where it doesn't. But this is a system UI. We can make OS and Framework developers aware, which is what I do on the Apple side when I discover accessibility problems.   
* Wendy: Noting that the high-level output is that the TAG review is generally positive. Given the depth of discussion about the architecture, risks, and benefits, it's good to have their input and I think we've done a pretty good job of balancing and understanding those considerations. Good work to everyone who has put in thought on this design.   
* Mohamed: First: Credential selector in Credman is different from the one in Wallet/Android, it means two different things. I'd like to make sure TAG clarifies which one they mean (e.g., for the issue you filed Marcos). Second, they mention behavior in private browsing mode. I'm not sure what our response should be.  
* Marcos: For the second, I think it's way off; I think they misunderstood something. I don't know what they're talking about.   
* Mohamed: The point is that even in private browsing, you may expose something to the wallet. Option we have is to block the API completely.  
* Marcos: That doesn't make any sense. E.g., age verification in adult content.  Primary verification case.   
* Wendy: The comment was that they would like the document to say something about what user agents are expected to do in private browsing. What do we collectively expect should happen? We should describe that, and if it's consistent with the design principle that the API shouldn't reveal whether private browsing is engaged, then that's consistent with the TAG principles, and if not, we should have an explanation. That's how I read it.    
* Marcos: Maybe they misunderstood the API. Like, not having WebAuthn in private browsing would be absurd.  
* Nick: In terms of making the best use of feedback, we could assume the TAG aren't idiots and have some useful considerations. I think they anticipate use in private browsing mode would be common and that that could reveal more information to other parties like the wallet.  This is a case where you're going to be interacting with another piece of software, and maybe we should have some guidance about it.  
* Heather: Should we create an issue to hash this out? Sounds like three different perspectives?  
* Moahmed: I will create an issue. 

## 

## DC API PRs and Issues

* None tagged for discussion

## AOB

* Heather: Any other process we want to cover to make sure we're on the same page?  
* Rick: As a non-editor, I would like to see what process we are following for approving PRs. What exactly do we want to see before we land a PR?  
* Marcos: We don't have it formally written anywhere. Process we're following is do we have implementor commitment, hopefully we have one implementation before we land it in the spec. Ideally we have two implementations simultaneously. The checklist that comes in with every PR is the guidance we use. We could formalize it a bit more but we haven't needed to. I like the WHATWG model — two implementation commitments and no opposition. But some people argue that that gives too much power to one to veto. Also tests, implementor commitments, three editor approvals.   
* Rick: That’s not what I’ve seen in other W3C groups. Does that mean the group can only make changes when none of the editors is on vacation?   
* Marcos: No, it's not a hard thing, we can override it. But it's good to get reviews by all the editors.   
* Heather: We had a process discussion early on. FedCM work item has a much more elaborate set of process guidelines [https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md](https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md). But FedCM is a very big complicated set of APIs, so it needed a bigger, more complicated set of processes. When we brought in the DC API we made the decision that it's too heavyweight. The one thing I want to make sure we avoid is that no one person will ever do all approvals. There always have to be at least 2 editors. I don't want to use it as a voting system or anything, that sort of conflict has to come to the working group for discussion.   
* Matt: Some PR comments seem to be dependent on us picking a version of English we want to target. Let's just decide and move forward.   
* Ted: This question never dies. The W3C style guide says we use US English. But in current practice, if you're consistent within a given document, then it's OK to use either. Probably some believe the style guide is a typo and should be UK. We can probably agree amongst ourselves what makes sense for any given  document.   
* Marcos: US English, not up for debate  
* Wendy: [https://www.w3.org/guide/manual-of-style/\#Spelling](https://www.w3.org/guide/manual-of-style/#Spelling)  
* Heather: The style guide I wrote for IETF was US English unless the entire document was written for a different dialect..   
* Tim: The thing that triggered this was spelling of a word in a document we don't control. We're not going to change the name in the other document.  
* Heather: Yes, if citing a document name or quoting text in full, agreed, match the source..   
* Heather: Expecting to have series A on Monday but I won't be there myself. FedCM on Tuesday. Then a break through the end of the year, and start again in January. Watch the W3C calendar\!

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting, co-chair)  
* Nick Doty (CDT; mostly listening tonight)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Rick Byers (Google Chrome)  
* Mohamed Amir Yosef (Google Chrome)  
* Matthew Miller (Cisco)  
* Isaiah Inuwa (Bitwarden)  
* Marcos Caceres (Apple)  
* Wendy Seltzer (co-chair)  
  