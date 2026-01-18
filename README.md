# Community Cordova In-App Purchase Plugin

A comprehensive Cordova plugin for In-App Purchases on iOS (AppStore), Android (PlayStore), and Windows.

## Support This Plugin

I dedicate a considerable amount of my free time to developing and maintaining many Cordova plugins for the community ([See the list with all my maintained plugins][community_plugins]).

To help ensure this plugin is kept updated, new features are added and bugfixes are implemented quickly, please donate a couple of dollars (or a little more if you can stretch) as this will help me to afford to dedicate time to its maintenance.

Please consider donating if you're using this plugin in an app that makes you money, or if you're asking for new features or priority bug fixes. Thank you!

[![Sponsor Me](https://img.shields.io/static/v1?label=Sponsor%20Me&style=for-the-badge&message=%E2%9D%A4&logo=GitHub&color=%23fe8e86)](https://github.com/sponsors/eyalin)

[community_plugins]: https://github.com/EYALIN?tab=repositories&q=community-cordova-plugin

## Credits & Acknowledgments

This plugin was originally forked from [cordova-plugin-purchase](https://github.com/j3k0/cordova-plugin-purchase) by [Jean-Christophe Hoelt](https://github.com/j3k0).

A huge thank you to Jean-Christophe Hoelt for creating and maintaining the original cordova-plugin-purchase plugin. The original work laid the foundation for this plugin, and we are grateful for his contributions to the Cordova community.

Due to the original plugin no longer being actively maintained, this standalone repository was created to continue development, provide updates, and ensure compatibility with the latest platform versions.

Special thanks to all the original contributors:
- Jean-Christophe Hoelt (Author)
- Josef Froehle
- Guillaume Charhon
- Matt Kane
- Mohammad Naghavi
- Dave Alden

## Features

- **Consumables**: One-time purchases that can be bought multiple times
- **Non-Consumables**: One-time purchases that are permanent
- **Subscriptions**: Recurring purchases with auto-renewal
- **Multi-Quantity Consumables**: Purchase multiple items at once (Android)
- **Restore Purchases**: Restore previously purchased items
- **Receipt Validation**: Server-side validation support

### Platform Support

|  | AppStore (iOS / macOS) | Google Play | Windows |
|--|--|--|--|
| Consumables | Yes | Yes | Yes |
| Non-Consumables | Yes | Yes | Yes |
| Subscriptions | Yes | Yes | - |
| Restore Purchases | Yes | Yes | Yes |

## Installation

```bash
cordova plugin add community-cordova-plugin-purchase
```

Or from GitHub:

```bash
cordova plugin add https://github.com/EYALIN/community-cordova-plugin-purchase.git
```

## TypeScript Usage

```typescript
import 'community-cordova-plugin-purchase';

declare var CdvPurchase: any;

// Wait for device ready
document.addEventListener('deviceready', () => {
    const store = CdvPurchase.store;

    // Register products
    store.register([{
        id: 'my_subscription',
        platform: CdvPurchase.Platform.APPLE_APPSTORE,
        type: CdvPurchase.ProductType.PAID_SUBSCRIPTION,
    }]);

    // Setup event handlers
    store.when()
        .productUpdated(() => {
            console.log('Products loaded:', store.products);
        })
        .approved(transaction => {
            console.log('Purchase approved:', transaction);
            transaction.verify();
        })
        .verified(receipt => {
            console.log('Purchase verified:', receipt);
            receipt.finish();
        });

    // Initialize the store
    store.initialize([{
        platform: CdvPurchase.Platform.APPLE_APPSTORE,
        options: { needAppReceipt: true }
    }]);
});

// Make a purchase
function purchase(productId: string) {
    const product = CdvPurchase.store.get(productId);
    if (product) {
        product.getOffer()?.order();
    }
}

// Check ownership
function isOwned(productId: string): boolean {
    return CdvPurchase.store.owned(productId);
}
```

## JavaScript Usage

```javascript
document.addEventListener('deviceready', function() {
    var store = CdvPurchase.store;

    // Register products
    store.register([{
        id: 'my_product',
        platform: CdvPurchase.Platform.GOOGLE_PLAY,
        type: CdvPurchase.ProductType.CONSUMABLE,
    }]);

    // Handle events
    store.when()
        .approved(function(transaction) {
            transaction.verify();
        })
        .verified(function(receipt) {
            receipt.finish();
        });

    // Initialize
    store.initialize([CdvPurchase.Platform.GOOGLE_PLAY]);
});
```

## API

### Store Methods

- `store.register(products)` - Register products to be managed
- `store.initialize(platforms)` - Initialize the store for specified platforms
- `store.get(productId)` - Get a product by ID
- `store.owned(productId)` - Check if a product is owned
- `store.when()` - Setup event handlers
- `store.restorePurchases()` - Restore previous purchases

### Product Types

- `CdvPurchase.ProductType.CONSUMABLE`
- `CdvPurchase.ProductType.NON_CONSUMABLE`
- `CdvPurchase.ProductType.PAID_SUBSCRIPTION`
- `CdvPurchase.ProductType.FREE_SUBSCRIPTION`

### Platforms

- `CdvPurchase.Platform.APPLE_APPSTORE`
- `CdvPurchase.Platform.GOOGLE_PLAY`
- `CdvPurchase.Platform.WINDOWS_STORE`
- `CdvPurchase.Platform.BRAINTREE`

## Platform Support

- Android (API 16+)
- iOS (9.0+)
- macOS
- Windows
- Browser (for testing)

## Receipt Validation

For production apps, receipt validation is strongly recommended:

```typescript
store.validator = "https://your-validator-server.com/validate";
```

## Migration from cordova-plugin-purchase

If you're migrating from the original plugin:

1. Remove the old plugin: `cordova plugin rm cordova-plugin-purchase`
2. Install this plugin: `cordova plugin add community-cordova-plugin-purchase`
3. The API is compatible - no code changes required

## License

MIT

## Author

EYALIN (Community Fork Maintainer)

Original Author: Jean-Christophe Hoelt

## Contributing

- Star this repository
- Open issue for feature requests
- [Sponsor this project](https://github.com/sponsors/eyalin)

## Support

For issues and feature requests, please use the [GitHub Issues](https://github.com/EYALIN/community-cordova-plugin-purchase/issues) page.
