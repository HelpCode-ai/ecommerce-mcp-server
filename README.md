# E-commerce MCP Server

**Connect 13 shops and marketplaces to Claude, ChatGPT and Copilot through one MCP server.** Powered by [AnythingMCP](https://github.com/HelpCode-ai/anythingmcp).

E-commerce MCP Server connects 13 e-commerce systems to Claude, ChatGPT, Copilot and Cursor through one MCP endpoint: 171 tools in total. Pick the systems you run, add their credentials, and each becomes a set of MCP tools. It runs on AnythingMCP Cloud or self-hosted with Docker, with encrypted credentials and an audit log.

**Last verified:** 2026-09-26 against the systems marked verified in the table (each one's own verification is linked from its row).  
**Adapter synced:** <!-- synced -->2026-10-08

Maintained by [helpcode.ai](https://helpcode.ai), the team that builds and maintains [AnythingMCP](https://github.com/HelpCode-ai/anythingmcp).

## Systems

| System | Region | Tools | Auth | Verified live | Cloud | Dedicated repo |
|---|---|---|---|---|---|---|
| Amazon Seller Central (SP-API) | Global | 15 | OAuth 2.0 | yes, 2026-07-17 | [install](https://cloud.anythingmcp.com/connectors/store?install=amazon-seller) | [amazon-seller-mcp-server](https://github.com/keysersoft/amazon-seller-mcp-server) |
| WooCommerce | Global | 49 | QUERY_AUTH | yes, 2026-09-26 | [install](https://cloud.anythingmcp.com/connectors/store?install=woocommerce) | [woocommerce-mcp-server](https://github.com/keysersoft/woocommerce-mcp-server) |
| Shopware 6 Store API | DE | 6 | API key | yes, 2026-09-26 | [install](https://cloud.anythingmcp.com/connectors/store?install=shopware-6) | [shopware-mcp-server](https://github.com/kochfreiburg/shopware-mcp-server) |
| Magento (Adobe Commerce) | Global | 13 | API token | yes, 2026-09-26 | [install](https://cloud.anythingmcp.com/connectors/store?install=magento) | [magento-mcp-server](https://github.com/keysersoft/magento-mcp-server) |
| BigCommerce | Global | 14 | API key | not yet | [install](https://cloud.anythingmcp.com/connectors/store?install=bigcommerce) | – |
| eBay Sell | Global | 10 | OAuth 2.0 | not yet | [install](https://cloud.anythingmcp.com/connectors/store?install=ebay-sell) | – |
| Etsy | Global | 22 | OAuth 2.0 | not yet | [install](https://cloud.anythingmcp.com/connectors/store?install=etsy) | – |
| Ecwid | Global | 10 | API token | not yet | [install](https://cloud.anythingmcp.com/connectors/store?install=ecwid) | – |
| Kaufland Marketplace | DE | 7 | Signed API key | yes, 2026-10-08 | [install](https://cloud.anythingmcp.com/connectors/store?install=kaufland) | [kaufland-mcp-server](https://github.com/kochfreiburg/kaufland-mcp-server) |
| OTTO Market | DE | 8 | OAuth 2.0 | not yet | [install](https://cloud.anythingmcp.com/connectors/store?install=otto-market) | [otto-market-mcp-server](https://github.com/kochfreiburg/otto-market-mcp-server) |
| Zalando Partner (ZDS) † | DE | 5 | OAuth 2.0 | no † | [install](https://cloud.anythingmcp.com/connectors/store?install=zalando-zds) | – |
| Billbee Order Management | DE | 8 | User + password | yes, 2026-09-26 | [install](https://cloud.anythingmcp.com/connectors/store?install=billbee) | [billbee-mcp-server](https://github.com/kochfreiburg/billbee-mcp-server) |
| Mercado Libre | BR | 4 | OAuth 2.0 | not yet | [install](https://cloud.anythingmcp.com/connectors/store?install=mercado-libre) | – |

"Verified live" means someone ran the connector against a real system; its own repository says how and when. "Not yet" means it follows the vendor's API documentation and has not been confirmed there; reports are welcome.

† Built from the vendor's published API documentation and not yet exercised against a live system. Reports and fixes are welcome.


## Self-hosted (Docker)

```bash
git clone https://github.com/HelpCode-ai/ecommerce-mcp-server.git && cd ecommerce-mcp-server
./scripts/install.sh   # installs every system whose credentials are set in .env
```

## Connect Claude, ChatGPT, Copilot or Cursor

- **Claude (claude.ai, Desktop, mobile):** *Customize → Connectors → Add custom connector*, paste your MCP server URL and sign in. Claude connects from Anthropic's cloud, so the URL must be public HTTPS: your AnythingMCP Cloud URL, or your own instance behind TLS.
- **Claude Code:**

  ```bash
  claude mcp add --transport http ecommerce-mcp-server http://localhost:4000/mcp --header "X-API-Key: <MCP_API_KEY>"
  ```
- **Cursor** (`.cursor/mcp.json`) and **VS Code / GitHub Copilot** (`.vscode/mcp.json`, key `servers` instead of `mcpServers`, plus `"type": "http"`):

  ```json
  { "mcpServers": { "ecommerce-mcp-server": { "url": "http://localhost:4000/mcp", "headers": { "X-API-Key": "<MCP_API_KEY>" } } } }
  ```
- **ChatGPT:** add the public HTTPS URL as a connector (app) in ChatGPT's settings. A `localhost` URL does not work there.

## Tools

<!-- tools:start (generated from adapter/*.json, do not edit) -->
#### Amazon Seller Central (SP-API) (15)

| Tool | What it does | Access |
|---|---|---|
| `amazon_marketplace_ids` | Reference table of Amazon marketplace IDs and the regional SP-API endpoint that serves each. | read |
| `amazon_marketplace_participations` | List the marketplaces this seller account participates in (id, country, currency, store name). | read |
| `amazon_list_orders` | List orders in the configured marketplace. | read |
| `amazon_get_order` | Fetch a single order by its AmazonOrderId (format 3-7-7, e.g. 902-3159896-1390916). | read |
| `amazon_get_order_items` | List the line items of an order: SellerSKU, ASIN, title, quantity ordered/shipped, item price, taxes, promotion discounts. | read |
| `amazon_search_catalog` | Search the Amazon product catalog of the configured marketplace by keywords or identifiers (ASIN/EAN/GTIN/UPC/ISBN). | read |
| `amazon_get_catalog_item` | Fetch a single catalog item by ASIN with the requested data sets (summaries, attributes, images, salesRanks, dimensions…). | read |
| `amazon_fba_inventory` | FBA inventory summaries for the configured marketplace: fulfillable, inbound, reserved, unfulfillable and researching quantities per SKU/ASIN. | read |
| `amazon_get_item_offers` | Current offers for an ASIN in the configured marketplace: buy-box winner, lowest prices by fulfillment channel, offer counts, shipping. | read |
| `amazon_get_fees_estimate` | Estimate the Amazon fees (referral fee, FBA fulfillment fee…) you would pay for an ASIN at a given selling price. | read |
| `amazon_list_financial_events` | Financial events (shipments settlements, refunds, fees, service charges, adjustments) posted in a date window. | read |
| `amazon_get_listings_item` | Fetch one of YOUR listings by seller SKU: summaries, attributes, issues (quality/compliance problems), offers and fulfillment availability. | read |
| `amazon_create_report` | Request generation of a report (step 1 of 3). | write |
| `amazon_get_report` | Check a report's processing status (step 2 of 3). | read |
| `amazon_get_report_document` | Get the download descriptor of a finished report (step 3 of 3). | read |

#### WooCommerce (49)

| Tool | What it does | Access |
|---|---|---|
| `woocommerce_search_products` | Search/list products with rich filters — keyword (`search`), SKU, status, type (simple/variable/grouped/external), stock_status, on_sale, price range,… | read |
| `woocommerce_get_product` | Get a single product by id, including all fields: name, slug, description, short_description, sku, price/regular_price/sale_price, stock_quantity,… | read |
| `woocommerce_create_product` | Create a product. | write |
| `woocommerce_update_product` | Partial-update a product by id. | write |
| `woocommerce_delete_product` | Move a product to trash, or pass `force=true` to delete permanently (cannot be undone). | write |
| `woocommerce_batch_update_products` | Bulk create / update / delete products in a single call. | write |
| `woocommerce_list_product_variations` | List variations for a variable product. | read |
| `woocommerce_update_product_variation` | Update a single variation of a variable product — price, SKU, stock, attributes. | write |
| `woocommerce_list_product_categories` | List product categories. | read |
| `woocommerce_create_product_category` | Create a product category. | write |
| `woocommerce_list_product_tags` | List product tags. | read |
| `woocommerce_list_product_attributes` | List the global attribute definitions configured for the store (e.g. Size, Colour). | read |
| `woocommerce_find_low_stock` | Find products that are out of stock OR have `manage_stock=true` with `stock_quantity` at/below `threshold`. | read |
| `woocommerce_update_stock` | Convenience wrapper over `update_product`: enables stock management and sets quantity + status in one call. | write |
| `woocommerce_list_orders` | List orders with status, date, customer, and product filters. | read |
| `woocommerce_get_order` | Get a single order by id — full payload incl. | read |
| `woocommerce_update_order_status` | Set an order's status (e.g. processing → completed, on-hold → cancelled). | write |
| `woocommerce_add_order_note` | Add a note to an order. | write |
| `woocommerce_list_refunds` | List refunds attached to an order. | read |
| `woocommerce_create_refund` | Create a refund against an order. | write |
| `woocommerce_list_customers` | List customers. | read |
| `woocommerce_get_customer` | Get a customer by id (includes billing/shipping addresses, order count, total spent, last_order info). | read |
| `woocommerce_sales_report` | Sales report for a date window or named period. | read |
| `woocommerce_top_sellers_report` | Top-selling products for a date window or named period. | read |
| `woocommerce_coupons_totals_report` | Coupon counts grouped by discount type (percent \| fixed_cart \| fixed_product). | read |
| `woocommerce_orders_totals_report` | Counts of orders grouped by status (pending, processing, completed, ...). | read |
| `woocommerce_update_customer` | Partial-update a customer by id. | write |
| `woocommerce_delete_customer` | Permanently delete a customer. | write |
| `woocommerce_create_customer` | Create a customer account. | write |
| `woocommerce_create_order` | Create an order. | write |
| `woocommerce_delete_order` | Move an order to trash, or pass `force=true` to delete permanently. | write |
| `woocommerce_list_order_notes` | List notes attached to an order (both internal admin notes and customer-visible notes). | read |
| `woocommerce_get_order_note` | Retrieve a single order note by id. | read |
| `woocommerce_delete_order_note` | Delete an order note. | write |
| `woocommerce_list_coupons` | List discount coupons in the store. | read |
| `woocommerce_create_coupon` | Create a discount coupon. | write |
| `woocommerce_get_coupon` | Get a single coupon by id, including full usage stats (`usage_count`, `used_by` array). | read |
| `woocommerce_update_coupon` | Partial-update a coupon. | write |
| `woocommerce_delete_coupon` | Move a coupon to trash, or pass `force=true` to delete permanently. | write |
| `woocommerce_list_order_status_options` | Reference card: valid order status slugs. | read |
| `woocommerce_list_product_type_options` | Reference card: valid `type` values for `woocommerce_create_product` / `woocommerce_update_product` and product type filter on search. | read |
| `woocommerce_list_stock_status_options` | Reference card: valid `stock_status` values for product create/update + list filter. | read |
| `woocommerce_list_report_period_options` | Reference card: valid `period` values for `woocommerce_sales_report` and `woocommerce_top_sellers_report`. | read |
| `woocommerce_skill_inventory_optimization` | Skill recipe: find out-of-stock and low-stock products, cross-reference with demand (top sellers), and bulk-bump stock via batch update. | read |
| `woocommerce_skill_product_seo_optimization` | Skill recipe: optimise a product's name, description, slug, and Yoast/Rank Math SEO meta. | read |
| `woocommerce_skill_upsell_cross_sell` | Skill recipe: build upsell + cross-sell relationships for a product based on category, price tier, and tags. | read |
| `woocommerce_skill_low_conversion_analysis` | Skill recipe: identify products visible in the catalogue but not selling, with an honest framing of what WooCommerce REST can and cannot measure. | read |
| `woocommerce_skill_abandoned_order_triage` | Skill recipe: process stuck orders (pending / on-hold / failed) — chase or cancel based on age and reason. | read |
| `woocommerce_skill_revenue_kpi_snapshot` | Skill recipe: build a one-page KPI snapshot — revenue, AOV, top sellers, pipeline state, coupon mix. | read |

#### Shopware 6 Store API (6)

| Tool | What it does | Access |
|---|---|---|
| `shopware_search_products` | Search products in the sales channel. | read |
| `shopware_get_product` | Retrieve a single product by id or product number, including description, pricing tiers, cross-sells, properties, media, and associations. | read |
| `shopware_search_categories` | List or search categories in the storefront category tree. | read |
| `shopware_get_category` | Retrieve a category and optionally its products by category id. | read |
| `shopware_search_suggest` | Shopware search suggest — returns product suggestions for as-you-type autocomplete. | read |
| `shopware_get_cross_sells` | Retrieve the cross-sell product streams configured for a product (e.g. 'Related products', 'Customers also bought'). | read |

#### Magento (Adobe Commerce) (13)

| Tool | What it does | Access |
|---|---|---|
| `magento_list_store_views` | List the store views of the Magento / Adobe Commerce instance (id, code, name, website). | read |
| `magento_search_products` | Search products with Magento's search criteria DSL. | read |
| `magento_get_product` | Fetch a single product by SKU. | read |
| `magento_create_product` | Create a product. | write |
| `magento_update_product` | Update a product by SKU (PUT). | write |
| `magento_delete_product` | Permanently delete a product by SKU. | write |
| `magento_update_stock` | Update inventory stock for a SKU at a source. | write |
| `magento_list_categories` | List the category tree (or below a rootCategoryId). | read |
| `magento_search_orders` | Search orders. | read |
| `magento_get_order` | Fetch one order by ID with billing/shipping addresses, items[], status history. | read |
| `magento_cancel_order` | Cancel an order (only valid in pending/processing status). | write |
| `magento_search_customers` | Search customers with the same DSL. | read |
| `magento_get_customer` | Fetch one customer by ID. | read |

#### BigCommerce (14)

| Tool | What it does | Access |
|---|---|---|
| `bigcommerce_list_products` | List products with filters. | read |
| `bigcommerce_get_product` | Fetch a single product. | read |
| `bigcommerce_create_product` | Create a product. | write |
| `bigcommerce_update_product` | Update a product. | write |
| `bigcommerce_delete_product` | Permanently delete a product. | write |
| `bigcommerce_list_product_variants` | List variants (SKUs) for a product. | read |
| `bigcommerce_update_variant_inventory` | Update a variant's inventory_level (stock quantity). | write |
| `bigcommerce_list_categories` | List categories with parent/tree structure. | read |
| `bigcommerce_list_orders` | List orders (uses v2 endpoint — V3 doesn't fully cover orders yet). | read |
| `bigcommerce_get_order` | Fetch one order (v2). | read |
| `bigcommerce_get_order_products` | List line items on an order. | read |
| `bigcommerce_update_order_status` | Update an order's status (use status code from instructions). | write |
| `bigcommerce_list_customers` | List customers (V3). | read |
| `bigcommerce_create_customer` | Create a customer. | write |

#### eBay Sell (10)

| Tool | What it does | Access |
|---|---|---|
| `ebay_sell_list_orders` | List orders with their buyer, line items, totals, payment status and fulfilment status. | read |
| `ebay_sell_get_order` | Read one order in full: every line item with SKU and price, the buyer, the shipping address, the payment summary and the fulfilment instructions. | read |
| `ebay_sell_list_inventory_items` | List inventory items — the SKU-level product records behind Sell-API listings. | read |
| `ebay_sell_get_inventory_item` | Read one inventory item by SKU: its product details, condition, package dimensions and available quantity per fulfilment channel. | read |
| `ebay_sell_list_offers` | List the offers (listings) for one SKU, with their marketplace, format, price, listing status and listing id. | read |
| `ebay_sell_list_fulfillment_policies` | List the seller's fulfilment (shipping) policies for the configured marketplace, with their services, costs and handling times. | read |
| `ebay_sell_list_return_policies` | List the seller's return policies: whether returns are accepted, the return window, and who pays the shipping. | read |
| `ebay_sell_list_payment_disputes` | List payment disputes opened against the seller, with the reason, amount, status and the deadline to respond. | read |
| `ebay_sell_get_privileges` | Read the selling privileges of the account: whether selling is enabled and what the current selling limits on quantity and value are. | read |
| `ebay_sell_update_offer_price` | Change the price of a published offer (eBay bulk_update_price_quantity). | write |

#### Etsy (22)

| Tool | What it does | Access |
|---|---|---|
| `etsy_get_authenticated_user` | Return the user the OAuth token belongs to. | read |
| `etsy_get_user_shops` | List shops owned by a user. | read |
| `etsy_get_shop` | Fetch one shop by shop_id with full details (announcement, sale message, etc.). | read |
| `etsy_get_shop_listings_active` | Public list of a shop's active listings, as any visitor sees them. | read |
| `etsy_get_listings_by_shop` | Listings of your own shop by state (active, inactive, sold_out, draft, removed, expired), as the shop owner sees them. | read |
| `etsy_get_listing` | Fetch one listing by listing_id with full details. | read |
| `etsy_get_shop_receipts` | List orders (receipts) for the shop. | read |
| `etsy_get_shop_receipt` | Fetch one receipt with buyer info, transactions[], shipping address. | read |
| `etsy_get_shop_reviews` | List reviews (transactions with feedback) for the shop. | read |
| `etsy_get_listings_by_shop_section` | List listings filtered by a shop section. | read |
| `etsy_list_seller_taxonomy` | The full tree of Etsy seller categories (id, name, children). | read |
| `etsy_list_taxonomy_properties` | Properties (size, colour, material…) and their allowed values for one seller category. | read |
| `etsy_list_shipping_profiles` | The shop's shipping profiles. | read |
| `etsy_list_processing_profiles` | The shop's processing profiles (Etsy calls them readiness states: ready to ship or made to order, with processing times). | read |
| `etsy_list_return_policies` | The shop's return policies. | read |
| `etsy_list_shop_sections` | The shop's sections, to file a listing under one with shop_section_id. | read |
| `etsy_read_listing_inventory` | Products, prices, quantities and SKUs of a listing, per variation. | read |
| `etsy_create_listing_draft` | Create a listing as a draft (not visible to buyers). | write |
| `etsy_edit_listing` | Change a listing: title, description, tags, category, shipping, section, or state. | write |
| `etsy_set_listing_inventory` | Set price, quantity and SKU of a listing, per variation. | write |
| `etsy_add_listing_image` | Add a photo to a listing from a public image URL (JPG, PNG or GIF, up to 10 MB). | write |
| `etsy_add_order_tracking` | Mark an order (receipt) as shipped with its tracking code. | write |

#### Ecwid (10)

| Tool | What it does | Access |
|---|---|---|
| `ecwid_get_profile` | Get store profile (name, currency, formats, plan). | read |
| `ecwid_search_products` | Search products with filters. | read |
| `ecwid_get_product` | Get a product by ID. | read |
| `ecwid_create_product` | Create a product. | write |
| `ecwid_update_product` | Update a product (PUT — full replacement of passed fields). | write |
| `ecwid_list_categories` | List categories. | read |
| `ecwid_search_orders` | Search orders. | read |
| `ecwid_get_order` | Get an order by number. | read |
| `ecwid_update_order` | Update order — common: change paymentStatus, fulfillmentStatus, set trackingNumber. | write |
| `ecwid_search_customers` | Search customers. | read |

#### Kaufland Marketplace (7)

| Tool | What it does | Access |
|---|---|---|
| `kaufland_list_warehouses` | List the seller's warehouses with their id, name and address. | read |
| `kaufland_list_orders` | List orders in a time window: id, storefront, creation time and number of units. | read |
| `kaufland_get_order` | Read one order in full: the buyer, the billing and shipping address and every order unit with its own price, status and delivery window. | read |
| `kaufland_list_order_units` | List individual order units — the level Kaufland actually fulfils, cancels and pays out at. | read |
| `kaufland_list_units` | List the seller's units (offers) with their EAN, condition, price, stock and the storefront each is listed on. | read |
| `kaufland_list_tickets` | List customer service tickets with their subject, status and the order they relate to — where a buyer complaint shows up before it becomes a rating. | read |
| `kaufland_list_storefronts` | List the storefronts (one per country) Kaufland runs, with the currency and locale of each. | read |

#### OTTO Market (8)

| Tool | What it does | Access |
|---|---|---|
| `otto_market_list_orders` | List orders with their positions, buyer, delivery address and fulfilment status, optionally from/to an order date. | read |
| `otto_market_get_order` | Read one order in full: every position with SKU, price and status, the delivery and invoice addresses, and the payment method. | read |
| `otto_market_list_products` | List the seller's product variations with their SKU, EAN, product reference and category, optionally filtered. | read |
| `otto_market_get_product` | Read one product variation by SKU: its attributes, category and media. | read |
| `otto_market_list_quantities` | Read the current stock quantities OTTO holds for the seller's SKUs (up to 200 per page), so a discrepancy with the ERP can be spotted. | read |
| `otto_market_list_returns` | List returned position items by return status, with their SKU, reason and the order they belong to — the input to any returns-rate question. | read |
| `otto_market_update_quantity` | Set the available stock for one SKU, as OTTO's availability interface holds it. | write |
| `otto_market_update_price` | Set the standard price for one SKU. | write |

#### Zalando Partner (ZDS) (5)

| Tool | What it does | Access |
|---|---|---|
| `zalando_zds_list_orders` | List orders for the merchant with their order number, date, status and totals. | read |
| `zalando_zds_get_order` | Read one order in full: its items with EAN and price, the delivery address, and the current fulfilment state of each item. | read |
| `zalando_zds_list_order_items` | List the individual items of one order with their EAN, article number, price and per-item status — the level Zalando actually fulfils and cancels at. | read |
| `zalando_zds_list_shipments` | List the shipments of one order, with their carrier, tracking number and the order items they cover. | read |
| `zalando_zds_list_returns` | List announced returns (a customer created a return label for a Partner Fulfilled order) with their items, reason and the order they belong to. | read |

#### Billbee Order Management (8)

| Tool | What it does | Access |
|---|---|---|
| `billbee_list_orders` | List orders from Billbee with filtering by order date range, modification date (incremental sync) and pagination. | read |
| `billbee_get_order` | Get a single Billbee order by its internal Billbee order id, returning full detail including line items, addresses, payment and shipping info. | read |
| `billbee_get_order_by_extref` | Look up a Billbee order by its external reference (the marketplace/shop order number), returning the full order detail. | read |
| `billbee_list_products` | List products/articles from Billbee with pagination. | read |
| `billbee_get_product` | Get a single Billbee product by id (or by SKU/EAN via lookupBy), returning full article detail including pricing and stock. | read |
| `billbee_list_customers` | List customers from Billbee with pagination. | read |
| `billbee_get_customer_orders` | List all orders belonging to a specific Billbee customer by customer id, with pagination. | read |
| `billbee_list_shipping_providers` | List the shipping providers configured in the Billbee account, returning provider names and their available shipping products. | read |

#### Mercado Libre (4)

| Tool | What it does | Access |
|---|---|---|
| `mercado_libre_search_items` | Search items in a Mercado Libre site (country marketplace). | read |
| `mercado_libre_get_item` | Fetch full details for a Mercado Libre item by id. | read |
| `mercado_libre_get_user` | Get a user's public profile (typically used to inspect a seller). | read |
| `mercado_libre_list_orders` | List orders for an authenticated seller. | read |
<!-- tools:end -->

## FAQ

### How do I connect my shop or marketplace to Claude?
Install the adapter for each channel in AnythingMCP, authorise it, and add the MCP server URL to Claude as a custom connector. ChatGPT, Copilot and Cursor use the same URL.

### Can I ask about several marketplaces in one question?
Yes. Put every channel on the same MCP server and the AI calls each one and combines the answers.

### Which channels are verified against a real account?
The "Verified live" column says so per channel, with the date. The others follow the vendor's API documentation and have not been confirmed yet.

### Can the AI change prices, stock or orders?
Only through write tools, and only when a role allows them. Most marketplace adapters only read; WooCommerce, Magento, BigCommerce, Ecwid, OTTO Market and eBay have write tools.

### Does customer data reach the AI provider?
Only the fields a tool returns. Response mapping drops addresses or phone numbers before they leave your AnythingMCP instance, and Amazon buyer data is not requested at all.

## Related

- [erp-mcp-server](https://github.com/HelpCode-ai/erp-mcp-server): ERP MCP server: connect 17 ERPs (SAP, Odoo, JTL-Wawi, Xentral, weclapp, ERPNext…) to Claude & ChatGPT. Self-hosted or cloud.
- [openapi-to-mcp](https://github.com/HelpCode-ai/openapi-to-mcp): OpenAPI to MCP: turn any OpenAPI/Swagger or REST API into an MCP server for Claude & ChatGPT. Every endpoint a tool, no code.
- [AnythingMCP](https://github.com/HelpCode-ai/anythingmcp): the open-source MCP server and gateway this repository is built on.

## License

AGPL-3.0-only. The adapter definition in `adapter/` comes from AnythingMCP (AGPL-3.0).
