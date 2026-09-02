# Restore GCLID Tag Template for GTM

Use this GTM web tag template to restore the Google Ads conversion attribution cookie (`_gcl_aw`) when Safari strips the `gclid` parameter from the landing page URL. It reads the click ID from a fallback URL parameter that Safari leaves alone and rebuilds the cookie in Google's own format (`GCL.{timestamp}.{gclid}`), so your Google Ads conversion tags attribute the conversion as if the `gclid` was never lost.

The cookie is only written when `ad_storage` consent is granted. If the real `gclid` is present in the URL, the tag does nothing and lets the Google tag handle it. If the cookie already holds a click ID, it is left untouched.

## Installation

### Google Ads

1. Go to **Admin**, then **Account settings**, then **Tracking**.
2. Set the account-level tracking template to:

   ```
   {lpurl}?lnid={gclid}
   ```

   If you already use a tracking template, append `&lnid={gclid}` to it. The parameter name is configurable in the tag.

### GTM

1. Download [`template.tpl`](template.tpl).
2. In GTM, go to **Templates**, then **Tag Templates**, then **New**.
3. Open the menu in the top right, click **Import**, and select `template.tpl`.
4. Click **Save**.
5. Create a new tag of type **Restore GCLID** and fire it on **Initialization - All Pages**, so it runs before your Google Ads conversion tags.

## Settings

| Field | Default | Description |
|---|---|---|
| Cookie Name | `_gcl_aw` | The cookie to write when the click ID arrives through the fallback parameter. |
| URL Parameter Name | `lnid` | The fallback parameter that carries the `gclid` value. Must match the tracking template in Google Ads. |

The cookie lifetime is 90 days, matching Google's own `_gcl_aw` cookie.

## Companion templates

- [Shopify Custom Pixel](https://github.com/lucnugteren/shopify_custom_pixel) for a GTM dataLayer in Shopify checkout.
- [User ID tag template](https://github.com/lucnugteren/gtm_web_tag_template_user_id) for external ID matching in Meta.
- [Purchase Count tag template](https://github.com/lucnugteren/gtm_web_tag_template_purchase_count) for new vs. returning customers in Google Ads.

More at [lucnugteren.com/resources](https://lucnugteren.com/resources).
