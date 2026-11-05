# Chromecast casting

Media Baker's Cast sender page is available at `/cast.html` after installing this branch.

## Cast a video

1. Sign in to Media Baker and open the media item's details.
2. Select the desired audio, subtitle, and quality options.
3. Use **Copy URL** to create a copied playback link. The account must have the existing **Copy playback URLs** permission.
4. Open `/cast.html` on a browser that supports Google Cast and paste the copied link.
5. Choose **Choose device and cast** (or the Cast icon) and select the Chromecast.

The copied HLS URL contains a signed playback token scoped to that media item; it is not an account API key or session token. The Chromecast requests the URL and its HLS segments directly. The sender page does not send account credentials to the receiver.

## Requirements and limitations

- The browser hosting the sender page must be on HTTPS (localhost is also treated as a secure development origin by modern browsers) for the Google Cast sender SDK.
- The Chromecast must be able to reach the full URL in the copied link, including the host, scheme, port, and all playlist/segment routes. A public/reverse-proxied URL is fine; it does not have to be on the local network.
- Treat a copied playback URL as a bearer link and keep it private. Anyone who obtains it can play that item until the playback token expires. The deployment's HLS TTL controls the token lifetime.
- Start with H.264/AAC-compatible copied streams. Source codecs and particular Chromecast generations can still affect playback compatibility.
- This initial integration is a standalone Cast sender page. It loads a single HLS item and does not yet mirror remote controls, report precise Cast playback progress, or automatically advance to the next item. Existing copied-stream segment delivery provides the server's approximate external-playback progress tracking.
- No physical Chromecast is available in CI, so actual device discovery, codec support, and playback should be validated against the instance and receiver.
