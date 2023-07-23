=== SameSite Cookies ===
Contributors: ayeshrajans
Tags: security, csrf, cookies, samesite
Requires at least: 6.2
Tested up to: 6.3
License: GPLv2 or later
Stable tag: 2.0
Requires PHP: 7.0

CSRF-protection for authentication cookies. When enabled, this plugin makes sure the "SameSite" flag is set in authentication cookies. SameSite flag on a cookie prevents the browser from sending the cookie (thus, the authentication) on Cross-Site requests. This protects users from Cross-Site Request Forgery attacks.

== Description ==
This plugin adds the "SameSite" cookie flag to WordPress's authentication cookies. On supported browsers (all current IE, Edge, Chrome, and Firefox), this can effectively prevent all Cross-Site Request Forgery attacks throughout your WordPress site.

SameSite cookie flag support was added to PHP on version 7.3, but this plugin ships with a workaround to **support all PHP versions** WordPress supports.

There is no administrative UI provided: Activate this plugin, and you are all set!

You can configure the SameSite flag value from your WordPress configuration file. You cna pick a value from `Lax` (default), `Strict`, or `None`. You can read about [SameSite cookies here](https://php.watch/articles/PHP-Samesite-cookies).

To configure the `SameSite` flag value, edit your WordPress configuration file (`wp-config.php`), and add the following lines right above `/** Sets up WordPress vars and included files. */`. 

```php
define( 'WP_SAMESITE_COOKIE', 'Lax' ); // Pick from 'Lax', 'Strict', or 'None'.
```

Note that **only the authentication cookies are affected**. Regular cookies that your installed plugins set will **not** be affected, nor provide any meaningful value with `SameSite` flags.

== Installation ==
1. Install this plugin as you would with any other plugin.
2. Enable it.
3. There is no third step - From this point afterward, authentication cookies your WordPress site uses will contain SameSite flag, and you will be protected from CSRF attacks.

If you find this plugin useful, I'd appreciate you leaving a review on the plugin page.

== Frequently Asked Questions ==
= The plugin doesn't work !?!? =
Yeah, probably. This plugin uses what's called "pluggable functions" supported in WordPress to replace `wp_set_auth_cookie` function.
This means that any other plugin that tampers with the login cookie parameters will override this plugin, and this plugin may not even get a chance to do what it does.

= How do I test if the plugin works =
Go to the Login page of your WordPress site, and open your browser's development tools. Inspect the HTTP POST request made by the browser when you submit the login form. The response headers for `Setcookie` response headers must contain `Samesite=Lax` (or the configured value) if the plugin is working.

Note that cookies apart from the authentication cookies are **not** handled by this plugin, nor it makes sense to add SameSite attribute to them.

See the screenshot as well.

= Do I need to have PHP 7.3 or later? =
No. [PHP 7.3 officially added SameSite cookie support](https://php.watch/versions/7.3/same-site-cookies), but this plugin comes with a polyfill to extend support to all previous PHP versions.

= Is WordPress vulnerable to CSRF attacks without this plugin? =
Without SameSite cookie, WordPress core and third party plugins must implement their own CSRF checks, which can be overlooked, [intentionally ignored](https://wordpress.org/plugins/comment-form-csrf-protection/), or sometimes not even have thought about, which can be the case for contributed plugin. This plugin attempts to solve this with  different take and complement existing solutions.


== Screenshots ==

1. Browser response containing the SameSite attribute in Setcookie headers.

== Changelog ==

= 1.5 =
* Fixes a cookie expiration issue that was reported multiple times in the issue queue. Thanks to Jamie Magin (@jamagin at GitHub).

= 2.0 =
* Requires PHP 7.0+
* Synced pluggable code from upstream for better compatibility with hooks.
