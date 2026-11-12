# Hub FAQ

**Do I have to install Hub separately?**
Usually not. Every UMBFY package depends on Hub, so installing any one of them installs Hub. Install it directly
only if you want the UMBFY section before any feature package is in place.

**Why can't I see the UMBFY section?**
It has not been granted to your user group. **Users → Groups →** your group **→ Sections →** tick **UMBFY**. This
applies even to the user who installed the package.

**Do I need a UMBFY account?**
No. Every free capability works without one. An account enables licence sync, update checks and support history.
Until you connect one, nothing is sent anywhere.

**Why does everything say "Not checked"?**
No account is connected, so Hub has not checked anything. It is an honest report rather than an error.

**Does Hub send my content or credentials anywhere?**
No. Content, credentials and connection strings are never sent. Usage statistics are a separate opt-in that is off
until an administrator turns it on, and the exact payload is shown first.

**Will installing a UMBFY package rebrand my client's site?**
No. Backoffice branding is off by default. If you enable it, it fills only the Umbraco image settings still at their
default value, so an explicit client logo always wins.

**Does Hub need Node.js or a client build?**
No. Compiled Backoffice assets ship in the package under `/App_Plugins/UMBFY.Hub/`.

**Which Umbraco versions are supported?**
17.x and 18.x (`[17.0.0,19.0.0)`). See [Supported Umbraco versions](../getting-started/supported-umbraco-versions.md).

**If Hub cannot reach UMBFY, do my paid features stop working?**
No. Licences are verified offline. An outage never revokes a valid licence — and equally, an outage never grants
paid access.

**How do I uninstall cleanly?**
Remove the feature packages first and `UMBFY.Umbraco.Hub` last, because they depend on it.

**Where do I report a bug?**
From **UMBFY → Support** in the Backoffice, or on the public
[UMBFY Packages issue tracker](https://github.com/UMBFY/UMBFY-Packages/issues). Never include secrets.
