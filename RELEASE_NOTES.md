# Release Notes - Community Cordova Plugin Purchase

## 1.0.0 (2025-01-18)

### Community Fork

This is the first release of the community-maintained fork of `cordova-plugin-purchase`.

#### Why This Fork?

The original [cordova-plugin-purchase](https://github.com/j3k0/cordova-plugin-purchase) by Jean-Christophe Hoelt is no longer actively maintained. This community fork was created to:

- Continue maintenance and bug fixes
- Ensure compatibility with latest Cordova and platform versions
- Provide ongoing support for the community

#### Credits

This plugin is based on `cordova-plugin-purchase` v13.12.1 by Jean-Christophe Hoelt. All credit for the original implementation goes to him and the original contributors.

#### What's Included

- Full compatibility with the original cordova-plugin-purchase v13.12.1 API
- Support for iOS (AppStore), Android (PlayStore), Windows, and macOS
- Consumables, Non-Consumables, and Subscriptions
- Receipt validation support
- Google Play Billing Library 7.1.1

#### Migration

If you're migrating from `cordova-plugin-purchase`:

```bash
cordova plugin rm cordova-plugin-purchase
cordova plugin add community-cordova-plugin-purchase
```

No code changes are required - the API is fully compatible.

---

## Previous Releases (from original cordova-plugin-purchase)

For historical release notes from the original plugin, see:
https://github.com/j3k0/cordova-plugin-purchase/blob/master/RELEASE_NOTES.md
