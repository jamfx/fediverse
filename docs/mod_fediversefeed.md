# Fediverse - Mastodon Feed (Module)

This module is part of the Fediverse Tools for Joomla package.

The module displays the public toots stream of a Mastodon account. Please note that this only includes public and unlisted posts made directly, reblogged, or replied to by the account. It does not bookmarks, or toots made with any of the more private settings.

## Options

You can configure every instance of the module by editing its options. Only the options specific to this module are documented below; those which are managed by Joomla are not documented as they are considered common knowledge.

### Module options

**Username**. Enter the Mastodon username in the format `username@servername`, e.g. `nikosdion@fosstodon.org`.

**RTL Feed**. If the toots of that user are primarily written in a Right-To-Left language, such as Arabic, turn on this option. It will apply special CSS to display the toots stream correctly (right-aligned, instead of left-aligned). Please note that individual toots written in an RTL or LTR language will get the correct language direction automatically.

**Show Display Name**. Should the user's chosen Mastodon display name be presented above the toots stream?

**Show Avatar**. Should the user's avatar on Mastodon be presented above the toots stream? If both this and the Show Display Name options are selected, the avatar is displayed next to the display name. Please see the “Notice about media files loading” section at the bottom of this documentation page.

**Link to Profile**. Only applies and shown if Show Display Name and/or Show Avatar is enabled. When enabled the avatar and display name (whichever is shown) will become a link to the user's public Mastodon profile page.

**Show Profile Information**. Should the short description of the toots feed (“Public posts from such-and-such-user”) be displayed above the toots stream?

**Toot Link Title**. There is a link to the toot on the Mastodon server below each toot displayed by the module. By default, the _Item Title_ is displayed which is the date and time of the toot as formatted by the Mastodon server. This information might be in a language other than your site's displayed language and depends entirely on the Mastodon server itself. You can instead choose to display the _Publish Date_ which is the same information, but formatted by Joomla itself using the language currently active on your site.

**Maximum Toots**. The maximum number of toots to display. If the server returns fewer toots than this setting then only the available number of toots will be displayed, of course.

**Show Media**. Should the media files (images, videos) attached to the toot be displayed? Please see the “Notice about media files loading” section at the bottom of this documentation page.

### Feed Caching

This module uses the public API of Mastodon to retrieve the user's account information and the timeline (a feed of the latest toots). The options in this tab control how often this module makes API calls to the Mastodon server.

Please note that the feed caching works _independently_ of Joomla's global cache and the settings in the Advanced tab of the module. Joomla's global cache controls whether the HTML generated by the module will be cached. This option controls whether the API data is cached, before it's processed into HTML.

**Feed and Account Cache**. When you enable this option, the module will only make API calls to the Mastodon server every as many seconds as the options below. This is **VERY STRONGLY RECOMMENDED** as it reduces the load on the Mastodon instance and makes your site faster. If you disable this option the module will need to make API calls to the Mastodon server every time the page it's placed on is loaded (depending on Joomla's caching) which increases the load on the Mastodon server, makes your site slower to load, and could lead to your Mastodon account be suspended.

**Feed Cache Time (seconds)**. How often to check with the server for new toots. We strongly recommend using a value of at least 600 seconds. If you do not toot very often we recommend using a value of 3600 seconds (one hour, the default setting).

**Account Cache Time (seconds)**. How often to check with the server for the user's account information (display name, descriptions, avatar). It's recommended setting this to 86400 (one day).

### Advanced

**Request Timeout (seconds)**. Whenever the module needs to make an API call it makes an HTTPS request to the Mastodon server. If the server is unreachable, under maintenance, etc the request can take up to 30 seconds to time out, making your visitors think that your site has hung. This option limits the time Joomla will wait for the Mastodon server to return an API response. If the API fails to respond within that time, Joomla will give up and the feed module will not be displayed at all.

**Custom TLS Certificate Path**. If you are using this module against a test, local, or internal server which is using a self-signed TLS certificate for HTTPS enter the full path of the TLS certificate file (in PEM format) to allow Joomla to load the toots feed. This is NOT necessary for live Mastodon servers. This is only meant to be used for local tests and special use cases (like intranet, company-wide installations of Mastodon behind a firewall). If you do not understand what this is for, you don't need it.

## Frontend performance

The module will not load any CSS or JavaScript until it needs it. 

When no toots feed is available the module is not loaded, and as a result it loads no CSS or JavaScript. When a toots feed is available a small CSS file is loaded by default.

If you have turned on loading media files _and_ your toots use media files a JavaScript file will be loaded to support the media files display. If loading media is turned off _or_ your toots don't use any media files the JavaScript file will not be loaded.

All images are lazy-loaded for better performance.

## Content warnings

A major feature of Mastodon is content warnings, hiding toots or media files with potentially explicit, triggering, profane or otherwise inappropriate nature. This module honors content warnings both for entire toots and for individual media files.

Toots marked with a content warning will appear collapsed (using an HTML DETAILS) element and the content warning will appear. Clicking on the content warning expands the toot text and any media files contained. This may not work on older browsers which do not support the DETAILS element.

Media files marked as sensitive in a toot which is NOT marked with a content warning will appear blurred with a radius of 1.5em to make the unidentifiable. You will need to click on the media file to display it. This may not work on older browsers which do not support the `filter` CSS property.

## ALT attributes

Media files in Mastodon are encouraged to have descriptions (ALT attribute). This module honours the description and adds it as an ALT attribute to images to ensure that the displayed toots stream is accessible to people with disabilities. Furthermore, the description is rendered as a FIGCAPTION element for sighted users to read when you click on a media item.

If you would rather that the FIGCAPTION is not used you need to do a Joomla layout override.

## Template and Layout Overrides

You can customise the module by doing standard Joomla template and layout overrides.

The files in `modules/mod_fediversefeed/tmpl` are standard Joomla view templates and can be overridden using the standard Joomla template override way.

## Notice about media files loading

Media files —such as avatars, images, and videos— are loaded directly from the Mastodon server. They are NOT proxied by your site.

As a result, the Mastodon server will be notified about your visitor's IP address when your visitor is shown the toots stream with this module.

Letting a remote serer know of your visitor's IP address _MAY BE_ considered a transfer of Personally Identifiable Information under some circumstances and jurisdictions. If unsure, ask your lawyer or turn off the Show Avatar and Show Media options of this plugin.