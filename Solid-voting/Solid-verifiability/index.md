---
layout: page
title: Solid verifiability
subtitle: How Solid improves verifiability
use-site-title: true
show-avatar: false
---

## Trust scenarios
### Pod provider not trustworthy

**_Solid pod provider or third party maliciously changes Alice's vote on her pod before it is counted_**

Alice can check her pod at any time to verify her vote.  If she notices her vote has been changed, she can sign up with a different pod provider.

**Fails** if Alice does not check her vote on her pod, or the vote is changed following the final time Alice checks it.

**Fails** if Alice's vote is changed only when the election provider reads it but appears unchanged to Alice.

### Alice's device not trustworthy

**_Alice's device changes her vote when she writes it to her pod_**

Alice can check her pod from a different device and correct it using the different device.

**Fails** if Alice does not check her vote from a different device.

**Fails** if all of Alice's devices are malicious. Alice should also check using, say, a device at her work.
