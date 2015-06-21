"Streams" refer to collections of items in the Google Reader API. This includes feeds, items with a specific tag, or folders. Stream IDs are are string-based identifiers used to identify streams and are passed to many API methods.

# Feed stream IDs #

Streams that correspond to data that come from crawled feeds are of the form `feed/<feed URL>`, for example:

  * <tt><code>feed/http://googleblog.blogspot.com/atom.xml</code></tt>
  * <tt><code>feed/http://blogsearch.google.com/blogsearch_feeds?q=mihai%20parparita&amp;hl=en&amp;scoring=d&amp;num=10&amp;output=atom</code></tt>

# Tag stream IDs #

Tags can be applied to items via the [edit tag](ApiEditTag.md) method and to subscriptions via the [edit subscription](ApiEditSubscription.md) method. Once a tag is applied, the tag is available as a stream, with the tag itself becoming the stream ID.

Tag stream IDs are of the form `user/<user ID>/<tail>`. `<user ID>` is the user's identifier, normally a numeric value obtained from the [user info](ApiUserInfo.md) method, but "`-`" may also be used for authenticated requests to signify the ID of the authenticated user.

`<tail>` is different depending on the kind of tag being used:

## System tag stream IDs ##

System tags have a tail of the form `state/com.google/<type>`. Here are common item-level tags:

  * `user/-/state/com.google/read`: applied to read items
  * `user/-/state/com.google/kept-unread`: applied to items that have been kept unread, removed onc they are marked as read
  * `user/-/state/com.google/starred`: applied to starred items
  * `user/-/state/com.google/broadcast`: applied to shared items
  * `user/-/state/com.google/like`: applied to liked items

Here are common subscription-level tags:

  * `user/-/state/com.google/reading-list`: applied to all subscriptions, corresponds to the "All items" view in the UI
  * `user/-/state/com.google/broadcast-friends`: applied to the shared items of the users that are being followed, subscriptions, corresponds to the "People you follow" view in the UI

## User-created tag stream IDs ##

User-created tags are added to items via the "Add tags" or "Edit tags" UI. They are of the form `user/-/label/<name>`, for example:

  * `user/-/label/Foo`
  * `user/-/label/Foo Bar`
  * `user/-/label/Foo Bar™`

Any character may be used as the name with the exception of:  <tt><code>" ^ &lt; &gt; ? &amp; \ /,</code></tt>.

## Folder stream IDs ##

Folder stream IDs are the same as user-created tag stream IDs (i.e. they are in the same namespace).

# Use in URLs #

When used as query parameters, stream IDs should be escaped as usual. More subtly, when used in paths (e.g. for the [stream contents method](ApiStreamContents.md)) the stream ID should be escaped too.

  * **Incorrect**: <tt><code>http://www.google.com/reader/api/0/stream/contents/feed/http://example.com/search?q=foo</code></tt>
  * **Correct**: <tt><code>http://www.google.com/reader/api/0/stream/contents/feed%2Fhttp%3A%2F%2Fwww.example.com%2Fsearch%3Fq%3Dfoo</code></tt>