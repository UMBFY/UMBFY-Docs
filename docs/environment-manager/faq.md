# Environment Manager FAQ

**Does it sync content and media?**
No. Environment Manager moves **schema** only — Document Types, Element Types, Data Types, Templates, Dictionary
items and Languages. Content, media, application deployment and database restore are all out of scope.

**Do I need it installed on every environment?**
On both ends of any promotion, yes, at the same version. An environment without the package cannot be compared or
promoted to.

**Can I try it without paying?**
Yes. The Free edition gives you dashboard, connection diagnostics, snapshots, compare and basic drift, with no Hub
and no licence required. Plan, execute, bootstrap, verify and recover are Professional and above.

**Do I need Hub?**
Not for Free capabilities. Paid capabilities need a valid signed licence, or a usable Hub-reported licence.

**My load-balanced site has four servers. Is that four licensed sites?**
No — one. Licences count **logical environments** by `LocalIdentity`, and all nodes of one site share one identity.

**Is the API key my licence?**
No, and this trips people up regularly. The signed licence decides which features you may use. The environment API
key authenticates calls between your own Umbraco sites. Activating a licence does not grant remote access; rotating
a key does not change entitlements.

**Can I promote straight to Production?**
Only through the full flow — compare, plan, approve, execute, verify — and Production carries stronger
acknowledgements than other environment types. There is no shortcut, by design.

**Why won't my approved plan execute?**
Either it is not approved, or the schema moved after the plan was built so its bound fingerprint no longer matches.
Re-compare and re-plan.

**What happens if Hub or the network is down?**
An activated signed licence keeps working offline until it expires. An outage never revokes a valid licence — and
never grants paid access either.

**Does it work over plain HTTP?**
Only for localhost, and only when `AllowHttpForLocalhost` is enabled there. Everything else requires HTTPS.

**Is it production-ready?**
It is a **release candidate** (`1.0.0-rc.1`), not published to nuget.org, and claims neither Marketplace approval
nor live cloud certification. It mutates real schema. Exercise it Local to Development first.

**Is recovery a backup?**
No. Recovery handles supported managed schema. Keep a database backup strategy.

**Which Umbraco versions are supported?**
17.x and 18.x (`[17.0.0,19.0.0)`). See
[Supported Umbraco versions](../getting-started/supported-umbraco-versions.md).

**Where do I report a bug?**
The [UMBFY Packages issue tracker](https://github.com/UMBFY/UMBFY-Packages/issues). Never include API keys, licence
keys or connection strings.
