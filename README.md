# Mass Market ERC721 extension for Shops

This document describes changes to the [ERC721
standard](https://github.com/ethereum/ercs/blob/master/ERCS/erc-721.md), altering specifically
the optional Metadata extension expressed as [JSON Schema](https://json-schema.org/). The
changes are specified for use with the [Mass Market protocol](https://docs.mass.market/).

For more context, see: https://github.com/masslbs/Tennessine/issues/640

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
+           "description": "A shorter description of the the asset to which this NFT represents, recommended to 100-120 characters."
+       },
+       "background": {
+           "type": "string",
+           "description": "A URI pointing to a resource with mime type image/* representing the asset to which this NFT represents. Consider making any images at a width between 320 and 1080 pixels and a rectangular aspect ratio of 1.91:1."
+       },
+       "discoverable": {
+           "type": "boolean",
+           "description": "Controls whether the referenced asset is allowed to be displayed through discovery mechanisms."
+       }
    }
}
```

**Legend** with respect to interpreting the above schema for Mass Market purposes, given that the
underlying NFT represents a Mass Market `Shop`:

* `name` - the shop profile name. Its recommended length is 40 characters.
* `description` - the full shop profile description.
* `image` - the shop profile image. The profile image should be a square 1:1 format in the range of `320px x 320px` to `1080px x 1080px`. It will be rendered with a circular passe-partout in the Mass Market interface.
* `brief` - a shorter shop description, displayed on aggregated shop discovery pages. If the string is in excess of 120 characters, the 121th character onward will be trimmed in the Mass Market interface.
* `background` - the shop background image, displayed on aggregated shop discovery pages. The background image should be a rectangular 1.91:1 ratio in the range of `320px x 168px` to `1080px x 567px`.
* `discoverable` - controls whether the shop is displayed on discovery pages.
