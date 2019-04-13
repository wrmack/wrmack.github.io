---
layout: page
title: Solid voting
subtitle: Exploring the potential for using Solid for online voting
use-site-title: true
show-avatar: false
---
* auto-gen TOC:
{:toc}

## Trust
Voters must trust the election system.  Democracy will fall into disrepute if voters can no longer trust the system they use for electing their representatives.  Trust can be achieved if the voter can verify their vote was counted. 
## Verifiability
End-to-end verifiability is considered to be an essential property of an election system.  It should be possible to verify that a vote was:
* cast as intended
* counted as cast.

And to verify tht all valid votes were counted.

Most current election systems do not meet this expectation. 

In the past, candidates have appointed scrutineers to monitor the counting of paper votes.  This provided a degree of verifiability.

If votes are recorded electronically, scrutineers can satisfy themselves that the counting operations are robust (such as checking optical scans manually).

However, scrutineers cannot provide the verifiability that a fully trusted election system should have. 

Some systems provide:
* some form of receipt of a vote being received
* a token which a voter can use to check their vote on a bullletin board
* a phone-in service whereby a voter can check their vote was counted as they intended.

The feedback to the voter is provided by the election service itself, which may, or may not, be fully trusted.

If a recounting of votes is called for, the votes held by the election service are recounted.  If votes are on paper then there may well be a different result.  Manual counting of paper votes is more prone to error than counting of electronic votes.  Assumptions here are that the election service has all the votes that were cast and that no votes were changed.

## The Solid concept
The Solid concept includes the notion that the user does not part with their information.  If Alice wants to comment on Bob's data (such as a post of some sort) Alice does not send her comment to Bob but places her comment on her own pod and sends Bob a notification.  Bob can then read Alice's comment on her pod.

## Online voting using Solid
If Alice casts a vote on the Solid platform, it is placed in her pod and the election service is notified.  Alice does not part with her vote.  The election service reads her vote.

The essential property of this system is that Alice retains her original vote.  If there is a dispute about the election result all votes can be read and counted again by an entirely separate third party in order to verify the result.  The original votes are recounted - not just those held by election service.

## A bit more detail
Alice is an authenticated voter (we will leave aside the matter of authentication).  Bob has been given responsibility for running the election.  Carol and Charlie are a couple of the candidates.  Judy is a judge.  Ted is an independent election auditor.

Alice has a pod hosted by Inrupt. Alice puts her vote onto her pod, digitally signs it with her private key and sends a notification to Bob as well as to Ted, who have read access rights to her vote and who have her public key. She can use a different device to access her pod to check her vote is saved correctly and was not changed.

Bob reads her vote.  At the same time an acl file is associated with the vote which prohibits the world, including Alice, from changing or deleting the vote until two weeks following the election.

On election day the vote count is revealed and winners are announced.  Charlie gets elected but Carol misses out.  The vote is close.  Candidates have three days to lodge a request for a recount with the court.

Carol applies to the court to have a recount of votes.   Judy supervises the recount.  Judy attends Ted's premises and orders Ted (not Bob) to conduct the recount of votes that were originally counted by Bob while she observes.  She notes that Ted, on his computer, has a database of all notifications he has received from voters that they have lodged votes.  She verifies that this is the same set of notifications that were received by Bob. She then observes Ted run a script which reads all votes and then counts them.  She confirms that the same number of votes are counted as were counted by Bob, that no votes with the same origin were counted more than once and that the result is the same.  Judy confirms Bob's declaration of the results.

An enhancement to this scenario has additional election officials reading votes at the same time as Bob, using different clients.  The vote count of all such counters is compared and a result only announced if all agree.  An attacker who wanted to interfer with the vote count would need to hack all separate counting devices.

Assumptions made in the above include:
* pod providers can be fully trusted
* all voters' pods will be online when Bob and Ted read votes

Issues not addressed include:
* whether Alice should have a chance to change her vote because she was coerced
* how Alice is authenticated
* how Bob can record that Alice has voted without knowing who she voted for
* how Bob can record who Alice has voted for without knowing it was Alice
* security

## Comparison to physical voting methods

In all current election systems, a voter submits their vote.  The voter might, depending on the election system being used:
* fill in a paper ballot and deposit it in a ballot box
* fill out voting documents and post them in the mail
* fill out a voting form online and press the submit button.

In an election a voter casts their vote by parting with it.  This creates uncertainty for the voter about whether the vote progresses through to be counted.

Consider voting at meetings where this is by show of hands.  Voters do not part with their vote - they display their vote.  Someone counts the hands that are raised and may be assisted by others in order to corroborate the vote count.  Up until now this way of voting has only been available when those voting are in the same room and visible to counters.

Solid voting is a bit like voting by show of hands.  A voter does not part with their vote.  It is on their pod for one or more counters to count.  But voters do not need to be in the same room and each voter can 'display' their vote in secret.

## How this changes the trust model
There are different trust models for different voting systems.

### Booth voting
A voter must trust:

1.    The booth will be available and accessible (availability is compromised if there is a two hour queue to get in, or if the booth does not have access to the electoral roll for the area the voter lives in, and could be inaccessible to a voter who is overseas)
2.    The vote will be counted as cast (this is compromised if a counter mis-reads it in error or maliciously changes it)
3.    The counting of all votes is accurate (errors in counting can be mitigated through various mechanisms, including checking systems during the counting process, auditing and recounts)

### Postal voting (or vote by mail)
A voter must trust:
1.    Their voting documents will be delivered to their home, and will be on time to post back a vote (there are recorded instances of papers not being delivered; overseas voters who recieve voting documents by mail may not have time to post back completed documents; there are reports of voting documents being stolen from private letter boxes)
2.    Their completed voting document will be delivered by the postal service to the election office in time for counting (postal services are getting less frequent with the possibility a voting document might not be delivered by the deadline)
3.   Their voting document will not be altered by the postal service (it is possible for a postal worker to unseal a voting document, alter it and reseal it)
4.    The counting of all votes is accurate (errors in counting can be mitigated through various mechanisms, including checking systems during the counting process, auditing and recounts)

### Online voting
A voter must trust:
1.    Their personal computer or device submits the vote as entered and does not change it.
2.    The vote is received by the election office server without being changed in transit.
3.    The election office server is available and receives the vote into its system (a DDOS attack could take the server down) 
4.    The election office server is not compromised in any way and counts the vote as intended by the voter.
5.    The bulletin board, if a vote is verified through a bulletin board.
6.    A recount is meaningful (what is the meaning of pressing the 'count' button on the same data as the first time?)

### Solid voting

[Verifiability](Solid-verifiability/)
