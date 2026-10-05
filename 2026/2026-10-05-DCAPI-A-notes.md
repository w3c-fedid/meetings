# FedID WG Telecon — DC API Series A, 2026-10-05

* Moderators: Heather

* Scribe: 

Call-in details: see [https\://www\.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https\://www\.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?   
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * TPAC Schedule  
    * Tuesday, 27 October, 13:15–15:00 GMT: [Web Authentication WG, Web Payment Security Interest Group, Federated Identity Working Group, Verifiable Credentials Working Group Joint Meeting](https://www.w3.org/events/meetings/7f5ffe2d-c418-47f1-880a-36710212b347/)  
    * Thursday, 29 October, 09:00–12:30 GMT, [Federated Identity WG](https://www.w3.org/events/meetings/0c6307c0-0cd8-4308-9343-b61e2042d15f/)  
    * Thursday, 29 October, 13:45–16:45 GMT, [Federated Identity Working Group, Federated Identity CG Joint Meeting](https://www.w3.org/events/meetings/64b54806-62fd-44fc-a3b0-345706c0a184/)  
* Ecosystem Updates (10 minutes)  
* DC API Issues & PRs (45 minutes)  
  * [Issue Triage](https://github.com/w3c-fedid/digital-credentials/issues) \- what needs time at TPAC  
* Any Other Business (AOB)

# Notes

## Administrivia

* Heather: usual reminder, code of conduct ..etc  
* 

## Ecosystem Updates

* Lee: I’d like to talk about transient activation, relaxing requirements, when we have more people here, as in Paypal’s recent issue.  
* Christian: SPRIND is going to be renamed soon (switching to a new subsidiary), but will be the same people.  
* Heather: TPAC schedule is out for the FedID WG, and there will be a joint meeting between DC API,,,, and Payment. We may switch the DC API morning one with FedCM afternoon talk due to conflicts with some WG members.  
* Wendy: Please communicate any conflicts in case we can resolve, no promises though.  
* Matt: Are the times for the WG already on the TPAC agenda? (Heather: nodding yes)  
* (Ted: If you're subscribed to the WG calendar, you've been auto-subscribed to the WG's TPAC events. Not that they've prefixed all those events with \`TPAC …\`, so they're not trivial to find within your calendar….)  
* Heather: Any other updates? Hearing none….

## DC API Issues & PRs (45 minutes)

### [Issue Triage](https://github.com/w3c-fedid/digital-credentials/issues) \- what needs time at TPAC

* Heather: We have 55 open issues, and we should get them down to reach CR. Most of the issues are security and privacy related, and Heather has been chasing Simone and Tara. Let’s take a look at the open issue list and vote for which one we should discuss  
* Matt: Some issues are marked CR-blocker, some aren’t, should we use the same label?  
* Heather: I would love to, but I am not confident in our label hygiene. I have also created the “TPAC2026” label, let’s use both.  
* Matt: Can we take [issue 574](https://github.com/w3c-fedid/digital-credentials/issues/574)?  
* Heather: Is it a blocker? Or do we only need to talk about it?  
* Matt: Cannot be a blocker\!  
* Heather: Should the PayPal [issue (587)](https://github.com/w3c-fedid/digital-credentials/issues/587) be discussed?  
* Lee: Yes  
* Heather: I will add it.  
* Christian: … “scribe was too slow” [Issue 382](https://github.com/w3c-fedid/digital-credentials/issues/382) and [issue 574](https://github.com/w3c-fedid/digital-credentials/issues/574) are both reopening some of the layering discussion (should be in the protocol layer or the API layer) and hence need some face time.  
* Heather: [Issue 565](https://github.com/w3c-fedid/digital-credentials/issues/565) seems like it needs to be done, but no need for further discussion.  
* Heather: most of the remaining issues  
* Matt: Key rotation is top of mind for the ………. but those seem to be at the protocol layer not the API layer.  
* Lee: not the DC API level, Christian thumbs up\! We can put recommendations for the protocol to be PQC ready but not at the DC API level.  
* Christian: the two I mentioned earlier might change that depending on the picked solution.  
* Lee: We have 3 options a) pick one of the recommended algorithms and assume it won't change, b) have a list of supported algorithms, or c) do nothing and pass it over the protocol.  
* Matt: It makes sense, but I don’t think there is a need to discuss PQC in TPAC.  
* Heather: What about [Issue 504](https://github.com/w3c-fedid/digital-credentials/issues/504)   
* Matt: this will be solved by clientData, I would be surprised if 504 isn’t addressed by client data and hence we better leave it out of the agenda since client data is the better pattern.  
* Heather: any other issues should be included? Hearing none, I will also ask for more input on Slack.  
* Wendy: should we also take a quick pass on the open PR list in the context of TPAC prioritization?  
* Heather: I will go through the list in case one is related to the issues.  
* Wendy: Reminder that TPAC is a good time for people in different time zones in case this helps get closure for some of the issues here, chairs are happy to help\!  
*  Matt: cross-WG discussion in TPAC. Should we have a discussion with CredMan regarding conditional meditation? For a more holistic view on credential (Webauthn vs DC API)  
* Heather: we should bring it to the joint meeting, I will add a note to make sure CredMan is included in the joint meeting  
* Heather: Lee, you had a couple assigned to you, would you be able to do it before TPAC?  
* Lee: We discussed a different approach in GDC which seems more plausible now than 1 year ago, and I will have a write up for that\! Issuers will provide a list of PKI root certs, and the platform will change the wallets to and show only the legit ones in the wallet selector. Malicious wallet won’t be offered, works over hybrid, and we might have the necessary PKI for that.  
* Christian: can we combine it with VCI wallet attestation?  
* Lee: In reality, they will be the combiner, but in theory no need to.  
* Christian: Yes, they can work independently, but we should avoid duplicating things.  
* Lee: Make sense to use the same cert. We expect people will be asking if we can do this for passkeys to filter credential managers.  
* Heather: Let chairs know about any other issues, agenda is being drafted now\!  
* 

## Any Other Business (AOB)

* 


# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Wendy Seltzer (co-chair)  
* Christian Bormann (SPRIND)  
* Matthew Miller (Cisco)  
* Helen Qin (Google Android)  
* Lee Campbell (Google Android)  
* Mohamed Amir Yosef (Google Chrome)  
* Bjorn Hjelm (Yubico)

