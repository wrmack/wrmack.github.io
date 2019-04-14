---
layout: page
title: Solid verifiability
subtitle: How Solid improves verifiability
use-site-title: true
show-avatar: false
---

## Trust scenarios
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

Because voters' votes are still on their pods, they can be re-counted by a different entity.

