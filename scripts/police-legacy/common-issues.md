---
icon: square-exclamation
---

# Common Issues



<details>

<summary>I am ESX user and duty system is not working</summary>

<img src="../../.gitbook/assets/resim (9).png" alt="" data-size="original">

Your error report likely

This indicates that the ESX version you are using (and generally most ESX versions) does not support a duty system embedded in the core. In this case, we recommend setting the `RequireDuty` option to `false` in the config.lua

</details>

