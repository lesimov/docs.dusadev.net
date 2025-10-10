---
icon: bug
---

# Error parsing script ... <\1>

Error message **example**: `Error parsing script @dusa_evidence/game/serverside/server.lua in resource dusa_evidence: @dusa_evidence/game/serverside/server.lua:1: syntax error near '<\1>'`

### Possible reasons <a href="#possible-reasons" id="possible-reasons"></a>

* You are transferring the folder to the VPS file by file, please upload the .zip file and extract it **after** it is already on your VPS (so drag and drop the zip file and **not** the folder)
* You may have to clear the **server** caches
* The download was corrupted, try doing a new clean install
* You have a virus on your server that is modifying other script files (very likely if everything else hasn't fixed it)

### How to verify my server version? <a href="#how-to-verify-my-server-version" id="how-to-verify-my-server-version"></a>

To verify what server version your server is currently using, you have to use the following command in your FiveM server console: `version`

#### Example <a href="#example" id="example"></a>

<figure><img src="https://documentation.jaksam-scripts.com/~gitbook/image?url=https%3A%2F%2F3735039044-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FFH9TH8An8XLjMiOMvVGb%252Fuploads%252F0rq9iQgYNSxNehKgBMCL%252Fversion_example.jpg%3Falt%3Dmedia%26token%3Db94e039f-7f28-4230-8e38-f6d9cb28f74e&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=38550fc7&#x26;sv=1" alt=""><figcaption></figcaption></figure>

### How to update my server version? <a href="#how-to-update-my-server-version" id="how-to-update-my-server-version"></a>

To update your server version, you have to download the new [server artifacts](https://runtime.fivem.net/artifacts/fivem/build_server_windows/master/) and to extract and replace them in your server folder

This is the **official** [FiveM guide](https://docs.fivem.net/docs/server-manual/setting-up-a-server/) to update your server

### My server version is already updated, but I have the error <a href="#my-server-version-is-already-updated-but-i-have-the-error" id="my-server-version-is-already-updated-but-i-have-the-error"></a>

If you have the error even if your server version is not the issue, then you have to check [here](failed-to-verify-protected-resource.md)
