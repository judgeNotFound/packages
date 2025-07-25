# API

Arguments for `invoice`.

|Name|Type|Required|Default|Description|
|-|-|-|-|-|
|`items`|`array`|✅|-|Invoice items|
|`seller`|`dictionary`|✅|-|Seller information|
|`recipient`|`dictionary`|✅|-|Recipient information|
|`iban`|`str`|✅|-|Seller IBAN|
|`bic`|`str`|✅|-|Seller BIC|
|`lang`|`str`|❌|`en`|Language as ISO 639 language code|
|`date`|`datetime`|❌|`datetime.today()`|Invoice date|
|`footnotes`|`array`|❌|`[]`|Footnotes, displayed as is. Can contain contacts, reverse charge info, etc.|
|`payment-terms`|`int`|❌|`14`|Days to due date|
|`invoice-number`|`auto \| str`|❌|`auto`|Invoice number, only numbers are supported|
|`logo`|`image \| none`|❌|`none`|Seller logo|
|`vat-rate`|`decimal`|❌|`decimal("0.255")`|Default VAT rate|
|`reference-number`|`auto \| str`|❌|`auto`|ISO 11649 reference number (begins with RF, only digits after RF supported)|
|`barcode`|`bool`|❌|`true`|Show bank barcode|
|`show-barcode-text`|`bool`|❌|`true`|Show clear text above barcode|
|`qrcode`|`bool`|❌|`true`|Show EPC QR code|
|`font`|`auto \| str`|❌|`auto`|Text font|
|`colors`|`dictionary`|❌|`DEFAULT-COLORS`|Color settings|

## Seller and recipient

The arguments `seller` and `recipient` are expected to be dictionaries like:

```typst
(
    name: "Company Oy",
    business-id: "1234567-8",
    address: [Street 123\ 01234 City],
)
```

The key `business-id` is optional for recipient and required for seller.
The key `address` is displayed as is.
`address` can also be `str` type, in that case, use `\n` as newline.

## Items

The argument `items` are expected to be an array of dictionaries like:

```typst
(
    description: "Apple",
    quantity: 10,
    unit-price: "2",
    vat-rate: "0.14",
)
```

The key `vat-rate` is optional.
If missing, default VAT rate is used.
`unit-price` is assumed to include VAT.

> [!IMPORTANT]
> Write `unit-price` and `vat-rate` as string, so that they can be converted to decimal without errors.
> This avoids rounding errors due to imprecision of floating-point numbers.

## Colors

The argument `colors` is expected to be a dictionary like:

```typst
(
  bg-passive: gray.lighten(70%),
  passive: gray.lighten(25%),
  active: black,
)
```

All values are [`color`](https://typst.app/docs/reference/visualize/color/) type.
See [Color presets](./color_presets.md) for presets.
