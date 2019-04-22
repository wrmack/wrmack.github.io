---
layout: page
title: Solid verifiability
subtitle: How Solid improves verifiability
use-site-title: true
show-avatar: false
---

## Breach of trust scenarios
### Pod provider not trustworthy

##### Solid pod provider or third party maliciously changes Alice's vote on her pod before it is counted

Alice can check her pod at any time to verify her vote.  If she notices her vote has been changed, she can sign up with a different pod provider.

**Fails** if Alice does not check her vote on her pod, or the vote is changed following the final time Alice checks it. A **solution** might be that the voting app shows Alice her vote on her pod as soon as she lodges it and notifies Alice if it is changed anytime after that.

**Fails** if Alice's vote is changed only when the election provider reads it but appears unchanged to Alice.

### Alice's device not trustworthy

##### Alice's device changes her vote when she writes it to her pod

Alice can check her pod from a different device and correct it using the different device.

**Fails** if Alice does not check her vote from a different device.

**Fails** if all of Alice's devices are malicious. Alice should also check using, say, a device at her work.

### Election manager not trustworthy

##### Election manager has been hacked - the counting of votes has been manipulated by an attacker

Because voters' votes are still in the voters' pods, they can be re-counted by a different entity.

## Other aspects of the trust model

### Voting app

##### Can the voting app be trusted?

The code is open source and can be scrutinised.  This is key to establishing trust in the app. 

What is stored in Alice's pod is her data - her vote.  She can check this at any time and from any device (if the pod is in the cloud and she is online).  She can 'see' her vote the same way the election manager will 'see' it when the election manager counts her vote.  However, if the voting app is malicious and surreptiously stores on Alice's pod not only her vote data but also code which will execute to change her vote at the time it is read by the election manager, then we cannot rely on the aspect of only data being stored on the pod.  



