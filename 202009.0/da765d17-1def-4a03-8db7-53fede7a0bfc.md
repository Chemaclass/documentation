## Install Feature Core

### Prerequisites
To start feature integration, overview and install the necessary features:

| Name | Version |
| --- | --- |
| Product Bundles | 202009.0 |
| Order Management | 202009.0 |
| Spryker Core | 202009.0 |

### 1) Set up Behavior


| Plugin | Specification | Prerequisites | Namespace |
| --- | --- | --- | --- |
| `ProductBundleOrderItemExpanderPlugin` | Expands order items with product bundles. | None | `Spryker\Zed\ProductBundle\Communication\Plugin\Sales` |
| `ProductBundleOptionItemExpanderPlugin` | Expands order items with product options. Copies unique product options from related bundle items to bundle. | None | `Spryker\Zed\ProductBundle\Communication\Plugin\Sales` |

**src/Pyz/Zed/Sales/SalesDependencyProvider.php**
```php
<?php

namespace Pyz\Zed\Sales;

use Spryker\Zed\ProductBundle\Communication\Plugin\Sales\ProductBundleOptionItemExpanderPlugin;
use Spryker\Zed\ProductBundle\Communication\Plugin\Sales\ProductBundleOrderItemExpanderPlugin;
use Spryker\Zed\Sales\SalesDependencyProvider as SprykerSalesDependencyProvider;

class SalesDependencyProvider extends SprykerSalesDependencyProvider
{
    /**
     * @return \Spryker\Zed\SalesExtension\Dependency\Plugin\OrderItemExpanderPluginInterface[]
     */
    protected function getOrderItemExpanderPlugins(): array
    {
        return [
            new ProductBundleOrderItemExpanderPlugin(),
            new ProductBundleOptionItemExpanderPlugin(),
        ];
    }
}
```
:::(Warning) (Verification)
Make sure that every order item from `SalesFacade::getOrderItems()` results contains product concrete/abstract IDs data.
:::