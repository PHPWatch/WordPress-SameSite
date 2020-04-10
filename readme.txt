=== SameSite Cookies ===
Contributors: ayeshrajans
Tags: security, csrf, cookies, samesite
Requires at least: 4.3
Tested up to: 5.4
License: GPLv2 or later
Stable tag: 1.4

CSRF-protection for authentication cookies. When enabled, this plugin makes sure the "SameSite" flag is set in authentication cookies. SameSite flag on a cookie prevents the browser from sending the cookie (thus, the authentication) on Cross-Site requests. This protects users from Cross-Site Request Forgery attacks.

== Description ==
This plugin adds the "SameSite" cookie flag to WordPress's authentication cookies. On supported browsers (all current IE, Edge, Chrome, and Firefox), this can effectively prevent all Cross-Site Request Forgery attacks throughout your WordPress site.

SameSite cookie flag support was added to PHP on version 7.3, but this plugin ships with a workaround to **support all PHP versions** WordPress supports.

There is no administrative UI provided: Activate this plugin and you are all set!

You can configure the SameSite flag value from your WordPress configuration file. You cna pick a value from `Lax` (default), `Strict`, or `None`. You can read about [SameSite cookies here](https://php.watch/articles/PHP-Samesite-cookies).

To configure the `SameSite` flag value, edit your WordPress configuration file (`wp-config.php`), and add the following lines right above `/** Sets up WordPress vars and included files. */`. 

`define( 'WP_SAMESITE_COOKIE', 'Lax' ); // Pick from 'Lax', 'Strict', or 'None'.`

Note that only the authentication cookies are affected. Regular cookies that your installed plugins set will **not** be affected, nor provide any meaningful value with `SameSite` flags.

== Installation ==
1. Install this plugin as you would with any other plugin.
2. Enable it.
3. There is no third step - From this point afterwards, authentication cookies your WordPress site uses will contain SameSite flag, and you will be protected from CSRF attacks.

If you find this plugin useful, I'd appreciate you leaving a review on the plugin page.

== Frequently Asked Questions ==
= Do I need to have PHP 7.3 or later? =
No. [PHP 7.3 officially added SameSite cookie support](https://php.watch/versions/7.3/same-site-cookies), but this plugin comes with a polyfill to extend support to all previous PHP versions.

= Is WordPress vulnerable to CSRF attacks without this plugin? =
Without SameSite cookie, WordPress core and third party plugins must implement their own CSRF checks, which can be overlooked, [intentionally ignored](https://wordpress.org/plugins/comment-form-csrf-protection/), or sometimes not even have thought about, which can be the case for contributed plugin. This plugin attempts to solve this with  different take and complement existing solutions.
