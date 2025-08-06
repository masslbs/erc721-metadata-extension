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
+       "discoverable": {
+           "type": "boolean",
+           "description": "Controls whether the referenced asset is allowed to be displayed through discovery mechanisms."
+       }
    }
}
```
