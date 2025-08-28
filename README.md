# Mass Market ERC721 extension for Shops

This document describes changes to the [ERC721
standard](https://github.com/ethereum/ercs/blob/master/ERCS/erc-721.md), altering specifically
the optional Metadata extension expressed as [JSON Schema](https://json-schema.org/). The
changes are specified for use with the [Mass Market protocol](https://docs.mass.market/).

For more context, see: https://github.com/masslbs/Tennessine/issues/640

## Schema

The complete JSON schema is available in [`schema.json`](./schema.json). Key extensions to the ERC721 metadata standard include:

```diff
{
    "title": "Asset Metadata",
    "type": "object",
    "properties": {
        "name": {
            "type": "string",
            "description": "Identifies the asset to which this NFT represents"
        },
        "description": {
            "type": "string",
            "description": "Describes the asset to which this NFT represents"
        },
        "image": {
            "type": "string",
            "description": "A URI pointing to a resource with mime type image/* representing the asset to which this NFT represents. Consider making any images at a width between 320 and 1080 pixels and aspect ratio between 1.91:1 and 4:5 inclusive."
        },
+       "brief": {
+           "type": "string",
+           "description": "A shorter description of the the asset to which this NFT represents, recommended to 100-120 characters.",
+           "minLength": 100,
+           "maxLength": 120
+       },
+       "background": {
+           "type": "string",
+           "description": "A URI pointing to a resource with mime type image/* representing the asset to which this NFT represents. Consider making any images at a width between 320 and 1080 pixels and a rectangular aspect ratio of 1.91:1."
+       },
+       "discoverable": {
+           "type": "boolean",
+           "description": "Controls whether the referenced asset is allowed to be displayed through discovery mechanisms."
+       },
+       "paymentAddresses": {
+           "type": "array",
+           "description": "An array of ethereum addresses which the merchant accepts payments to",
+           "items": {
+                "$ref": "#/$defs/address"
+           }
+       },
+       "acceptedCurrencies": {
+           "type": "array",
+           "description": "An array of ethereum tokens which the merchant accepts as payments",
+           "items": {
+               "$ref": "#/$defs/address"
+           }
+       },
+       "pricingCurrency": {
+           "type": "object",
+           "description": "The currency which the listing in the shop are priced",
+           "properties": {
+               "address": { "$ref": "#/$defs/address" },
+               "chainId": { "type": "number" }
+           },
+           "required": ["address", "chainId"]
+       }
    },
+   "required": ["pricingCurrency", "acceptedCurrencies", "paymentAddresses", "name"]
}
```

## Field Descriptions

**Legend** with respect to interpreting the above schema for Mass Market purposes, given that the
underlying NFT represents a Mass Market `Shop`:

* `name` - the shop profile name. Its recommended length is 40 characters. **Required.**
* `description` - the full shop profile description.
* `image` - the shop profile image. The profile image should be a square 1:1 format in the range of `320px x 320px` to `1080px x 1080px`. It will be rendered with a circular passe-partout in the Mass Market interface.
* `brief` - a shorter shop description, displayed on aggregated shop discovery pages. Must be 100-120 characters. If the string is in excess of 120 characters, the 121th character onward will be trimmed in the Mass Market interface.
* `background` - the shop background image, displayed on aggregated shop discovery pages. The background image should be a rectangular 1.91:1 ratio in the range of `320px x 168px` to `1080px x 567px`.
* `discoverable` - controls whether the shop is displayed on discovery pages.
* `paymentAddresses` - array of Ethereum addresses where the shop accepts payments. **Required.**
* `acceptedCurrencies` - array of ERC20 token addresses that the shop accepts as payment. **Required.**
* `pricingCurrency` - the primary currency used for pricing items in the shop, with contract address and chain ID. **Required.**

## Development

This project uses Nix for development environment management.

### Setup

```bash
# Enter development environment (requires direnv or manual nix develop)
nix develop
```

### Testing

Validate the JSON schema:

```bash
# Run schema validation
just test

# Or directly
jv ./schema.json
```