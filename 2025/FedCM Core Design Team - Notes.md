## Design Team members:

Sam Goto, Christian Biesinger, Nicolás Peña Moreno, Ben VanderSloot, Erica Kovac

## 3 March 2025

* (Heather) Where we left it: what would be in the core spec \= accounts pull, Active Mode, continuation API, login status API, IdP assertion endpoint, parameters API. This would be a non-fictional starting point.  
  * Remove passive mode, not fields as currently defined, metadata endpoint, IdP Registration (tho’ this last one has a requirement in the Solid demo)  
* (Heather) I am interested in figuring out what the core spec means for the [FPWD-identified issues](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues)  
* (Sam) We have some other steps to take first before we can dive into that list; we don’t have quite enough detail re: the core spec to make a determination on all the items on that issue list.   
* (Sam) First, would like to know more about Mozilla’s decision to support Ben’s work on the spec.  
* (Ben) He has already started working on it. That includes matching the specified fetch requests. Has started enough implementation to bump into issues. The core is what we started discussing last time; that’s what he’s trying to implement. We envision a world where there are no storage access heuristics and this unblocks us from that. Maybe we won’t need storage access at all in the long-term future.   
* (Christian) For the FPWD issues, some have a comment from Ben that Google needs to discuss internally and Google hasn’t done that yet.   
* (Ben) \[demo\] Using a test IdP that Google set up. Origin headers are compatible\! Wooo\! This does do client metadata (he will likely rip that out). Disconnect also works. Did get an ORB exception.  
* (Sam) can we agree on a web platform test that defines what core is? From a UX perspective, can we assume this might look more like a modal dialogue in the future?  
* (Ben) Working on it. The UI/UX is up in the air. The web platform tests are super-tied to the UI of Chrome (but Google is happy to discuss changing that, though Mozilla doesn’t know their UI yet so not really sure how to make a web platform test compatible.)  
* (Sam) Are you thinking account chooser first?   
* (Ben) Definitely will have an account chooser and will skip IdP chooser when you’re in a connected account set.   
* (Sam) Will the IdP chooser be a once-per IdP and removed outside the RP? Probably a platform choice. It would be helpful to work with the Google Sign-in team to work with the Firefox implementation, so we’re thinking of what questions they’ll ask.   
* (Ben) Working with the Google Sign-in will definitely be a goal.   
* (Sam) Maybe we can create feature detection so that when the browser doesn’t see the disclosure, they can use the continuation API. Not sure if Google Sign-in degrades gracefully.  
* (Ben) Re: the login URL \- right now, it is protected from URL decoration because it is one per IdP and it is in the well-known file. Can we get it out of the well-known file? This is a benefit that would let us cover more use cases. The one that need a login page to be contextualized to the referrer. Navigational tracking on this is fine since it only happens after an interaction with the browser UI. It doesn’t happen after the “game over” moment, but it does happen after the pop-up of “this IDP wants to do a thing)  
* (Christian) why we have this in well-known:  in active mode, when you click in login with google button, if you’re not logged in, it directly opens a pop up. This is a way around future bounce tracking mitigations.   
* (Ben) Forgot about the active mode difference.  
* (Sam) If core meets certain criteria for enough developers (but not all) is that a reasonable starting point that is constraining from an ergonomics perspective and facilitates the privacy analysis.  
* (Ben) this will be in core; it’s a question as to whether it has a constraint on it. We can come back to it later, but it is useful to consider options.   
* (Sam) maybe we have to stage core? The first step might presuppose that it’s ok to be constrained if it has enough deployment.  
* (Erica) it will be easier to unconstrain it later than constrain it after-the-fact. We can discuss later.  
* (Sam) One wrinkle \- someone found an attack vector, even with the well-known file, so we are unhappy with well-known  
* (Ben) is filing issues as new things are discovered during implementation  
* (Sam) maybe web platform tests are too expensive? We could collectively write something that tests all the things but is a manual test.   
* (Ben) simplest transformation would be to take the current web platform tests and make them manual tests with the instruction to click through and accept visible on the page. Web platform tests do have [manual components](https://web-platform-tests.org/writing-tests/manual.html).  
* (Christian) Could make our tests show instructions so it’s both manual and automatic.  
* (Ben) part of the challenge is the IDP chooser doesn’t have any representation here.   
* (Sam) from a backwards compatibility problem, it’s not too bad. It’s up to Ben wrt scope and amount of work. If we want to pull the web driver discussion in, we can, but if manual testing is better for now, that’s fine.  
* (Erica) possibly a higher-level webdriver API that just takes a tuple of (idp-origin, account-id) that's used for any of the cross-browser tests. (Not concerned with the presentation)  
* (Christian) that wasn’t sufficient for web app testing  
* (Erica) it won’t be sufficient to test exact behavior of the UI, but it would give us some tests that would work between the two browsers  
* (Sam) Maybe core and non-core parts of the web driver tests?   
* (Ben) it makes sense to have the web bindings on it; we should have automatic tests. Those are in scope for core. Having a way to disable the display and cancel the dialogue will get us in good shape with a ton of coverage  
* (Sam) there are two different audiences for tests. IdPs that want to prevent regressions and tests we want to use as browser vendors to make sure they don’t diverge too strongly from each other. The current tests are focused mostly on the IdP audience and are based on Selenium tests.   
* (Christian) note that other people are submitting PRs to improve the Selenium tests.   
* (Sam) wouldn’t filtering be something we MUST have in the spec? Like login hint or domain hint?  
* (Ben) yes, filtering is in the spec and Ben needs to implement. But if the IdP responds with 100 matching accounts, must you show all of them?  
* (Sam) the spec doesn’t say anything about that now; it’s up to the browser.  
* (Christian) the spec may require the browser to do that. We don’t have to do that initially, though. Can start with what Erica suggested for the tests.   
* (Ben) Can still test filtering; a reasonable behavior if the account is not in the list would be interesting.  
* (Christian) Can use autosignin to test that too.   
* (Sam) Good convergence on using web platform tests for interoperability between browsers. We seem to have good agreement as to what specifically the web platform tests are. We should have a separate stream of conversation for this. Note that web platform tests are also a CR blocker as per W3C process. We could use the web platform tests to define core; whoever is passing these tests is compliant with core.   
* (Ben) That would be idea.   
* (Sam) We could do the reverse, too, and create an extensions directory and move stuff we don’t expect to have defined in core.   
* Back to the [FPWD list](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues) 
  * 428 \- part of core  
  * 537 \- (because cookies are same site and not same origin, and so you want to be able to set login status to same site) part of core  
  * 442 \- part of core  
  * 555 \- part of core  
  * 556 \- part of core  
  * 559 \- NOT part of core (do you want to always have the fields array even in core? this leads to a discussion re: feature detection; core will need an extension to allow this in the future. Ideally extension behaviors are designed such that if you send nothing, it will still work. This one might be sticky. It will be something core can’t disagree with.)  
  * 511 \- part of core  
  * 553 \- part of core  
  * 552 \- part of core  
  * **488 \- come back to this one**  
  * 319 \- part of core  
  * 467 \- part of core  
  * 517 \- NOT part of core (tentatively)  
  * 352 \- NOT part of core (no one has it now, but we will need it someday)  
  * 407 \- duplication of the continuation API and the params API (so, in core)  
  * 240 \- NOT in core  
  * 441 \- NOT in core (which makes us sad)  
  * 317 \- part of core  
  * 677 \- NOT in core  
  * For the remainder of this list, design team is encouraged to review what’s left so we can come back and discuss whether it is core or an extension  
* (Sam) are there different level of extensions? Some are ones that may just be ones that are a very long ways away from mutual adoption, but others are philosophically misaligned.   
* (Sam) Next step for design team \= start editing the spec to pull out non-core things.   
* (heather) look at us doing cool stuff

**Action item: Christian to take a pass at the web driver tests to figure out what’s part of core, and reshape the API commands to make the applicable to Firefox.**   
**Action item: Heather to write up what the criteria are for core vs NOT core and put it in the administrative repo and adding a column to the Status of FPWD list**  
**Action item: Google (probably Nicolás) to work on revising the spec text; with Ben to review changes (break the spec into two parts (core and extensions). Extensions will be a Google editor. Core spec will have Ben as co-editor).** 

## 10 February 2025

* (Ben) Since FedCM is seeing more organic adoption, we're in a challenging moment to tighten this up. What are things that cannot be extracted from the spec? That are dependencies for consumers  
* (Sam) What's the right thing to do? We'll work backward from that. If that includes breaking changes, we'll make it work. There aren't many IdPs using FedCM; there are more RPs.  
* (Ben) So what's the right thing? We need an identity credential that will hold a token it fetches dynamically. What else?  
* (Sam) Paraphrasing inner-Ben: lightweight FedCM, active mode, multipleIdP extensions, not passive mode, not fields  
* (Ben) Would anyone use that? Things Ben doesn't like are being driven by user demand. If there is no passive mode, are there still consumers for FedCM?  
* (Sam) Yes. At least a deployment of Sign In with Google uses a subset. Not the lightweight push, but a subset that would benefit from the things I listed. There isn't anyone using the accounts push mechanism, but we're finding we'd be willing to take a leap of faith that it would be implemented. (No one has come to Google to say they require it, but willing to think they might if it's available.) There are entities using accounts pull and that might work with an IdP chooser in front of it (which might help with the timing attack problem)  
* (Ben) Of course another part of the problem is the sheer amount of resource available at different browser vendors to implement anything.  
* (Sam) Different groups in Google have different requirements/focus. Sam's group is willing to take a gamble on Lightweight FedCM.  
* (Ben) if the deployments are reliant on extensions, then that won't work.  
* (Sam) That's a choice Firefox is making as to what features you're implementing. But Google have tried to have stuff pushed to the browser before; it became complicated enough in the past they pulled it. So, Google signin might use lightweight push, but it's out of our hands and unlikely because of the freshness problems. They have a technical requirement to keep the accounts fresh, and that's probably a common requirement of IdPs.  
* (Erica) Agree with Sam re: accounts push. there are definitely IdPs that won't want to do that, so likely that for FedCM to work it's going to have to support accounts pull. Can we agree to that as part of the core spec?  
* (Ben) yes  
* (Erica) Next question: Fields is a point of contention. If, hypothetically, Firefox supports all of FedCM except Fields and only supports Active Mode, users won't get any benefit from that.  
* (Sam) The sign-in with google traffic uses Active mode, fields=empty array, continuation API, accounts pull, domain/login hints.  
* (Ben) can we implement without a disclosure UI?  
* (Sam) yes, that would still support instances  
* (Ben) continuation API is a tough one; it allows navigation-based tracking.  
* (Sam) the "game over" moment is the account chooser. After the account chooser, happy to send 1pc and link decoration parameters because it's past the account chooser.  
* (Ben) I was thinking about LoginURL.  
* (Sam) When the user logs out, we pop up a window pointing to the LoginURL but we don't allow link decoration there. there are no more parameters being passed.  
* (Christian) Continuation can contain anything, but it's after the user actively clicks the account.  
* (Ben) the issue is that it opens up a pop-up, which is less good on mobile.  
* (Christian) on Chrome, we use a custom tab.  
* (Ben) We don't have that. (unclear if Firefox implements the custom tab API)  
* (Sam) Maybe the core spec is: **accounts pull, Active Mode, continuation API, login status API, IdP assertion endpoint, parameters API**. This would be a non-fictional starting point.  
  * **Remove passive mode, not fields as currently defined**  
* (Ben) Hints field, too, though not a fan of how it has been implemented  
* (Sam) would you put an IdP chooser before accounts pull?  
* (Ben) Probably  
* (Sam) The signin with google team might question that as to whether it's the best user experience.  
* (Erica) Client metadata, passive mode, fields gets dropped  
* (Christian) IdP registration API is not in the spec at this time. What about .well-known.  
* (Ben) if you're fetching accounts, you need it.  
* (Nicolas) you fetch after the user clicks. So it depends on your threat model.  
* (Christian) If you fetch accounts only after you've opted into the IdP, it's maybe not that important?  
* (Ben) it has to exist for the accounts pull. Get-user-info returning all the accounts presented to the user is weird.  
* (Sam) that's an API that could be polyfiled by the StorageAccess autogrant.  
* (Ben) Yes, there's no privacy loss just not clear as to why it's needed.  
* (Nicolas) we could remove it.  
* (Ben) One more thing that's potentially sticky: is FedCM a login API or a social login API?  
* (Sam) The definition of social login is fuzzy. What's your definition?  
* (Ben) Is SSO still in scope?)  
* (Sam) parts of google sign in is for enterprise. Enterprises are harder.  
* (Erica) The problem with the enteprise use case is they don't expect to have to connect an account for every domain. It's not ideal.  
* (Sam) We are also seeing this in e-commerce (e.g., Shopify)  
* (Ben) It’s a weird mix. Login may be too big?  
* (Sam) Enterprise and edu has a much more complicated requirements than consumers have.   
* (Ben) where we started a few years ago was different from where we are now. Then it was solving for 3pc; it’s become more complicated.  
* (Sam) Next steps? A pass to remove just the things we’re not happy with, with maybe a moderation of the Fields API? We skill the exposure API when you get an empty array. Fields when undefined defaults to name, email, something. Perhaps: If you pass something other than fields empty array then we’ll throw an exception.  
* (Ben) The next step sounds like a larger work item that might have less adoption. What was originally in mind, dive in and implement something close to this, but did not realize how much UI changes and engineering efforts would be required. It would be a smaller fraction of google account stuff than I thought would be useful. So, in order to get the return we want in terms of immediate adoption, Ben has more work than with less return than before. Too many orgs are using the extensions that would only work in Chrome. If we made Lightweight FedCM \= Core, adoption would be even less.   
* (Sam) What’s harder? Adoption or writing code? For Chrome, it’s adoption.  
* (Ben) Not comfortable putting all the Auth eggs in one basket. And this is all engineering on one person in Mozilla.   
* (Sam) Is firefox opposing the design choices, or is it more a question of bandwidth to implement?  
* (Ben) That’s in part what I need to get answers on. Will work on getting answers over the next 2 weeks.  
* (Sam) Can we put together a PR that will remove the things that we know don’t align with Firefox and adding Ben as an editor, would that be a good step?  
* (Ben) Rough out the shape and let Ben have the conversations.  
* (Sam) Is anything in our [PR list](https://github.com/w3c-fedid/FedCM/pulls) something that shouldn’t be in core? (not that we can see). For items not  yet spec PRs, OK to have lightweight, IdP registration, delegation is too early but probably is non-conflicting?  
* (Ben) Yes, but have resource constraints for implementation.  
* (Sam) Let’s make sure to split the question \- what is the correct design and would represent Mozilla’s goals, and what is implementable given available resources.  
* (Ben) it’s not that simple, but understand the point. 

Action Items

* Ben to talk internally with Mozilla (HF to check back in 2 weeks)  
* Nicolas to revise the spec to pull out the extension into another file; we can then monkey patch the core