# HTTP headers

转自[MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers)



| 消息头                             | 描述                                                         | 更多信息                                                     | 标准                                                         |
| ---------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `Accept`                           | 用户代理期望的MIME 类型列表                                  | [HTTP Content Negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation) | HTTP/1.1                                                     |
| `Accept-CH` **                     | 列出配置数据，服务器可据此来选择适当的响应。                 | [HTTP Client Hints](http://igrigorik.github.io/http-client-hints) |                                                              |
| `Accept-Charset`                   | 列出用户代理支持的字符集。                                   | [HTTP Content Negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation) | HTTP/1.1                                                     |
| `Accept-Features`                  |                                                              | [HTTP Content Negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation) | RFC 2295, §8.2                                               |
| `Accept-Encoding`                  | 列出用户代支持的压缩方法。                                   | [HTTP Content Negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation) | HTTP/1.1                                                     |
| `Accept-Language`                  | 列出用户代理期望的页面语言。                                 | [HTTP Content Negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation) | HTTP/1.1                                                     |
| `Accept-Ranges`                    |                                                              |                                                              |                                                              |
| `Access-Control-Allow-Credentials` |                                                              | [HTTP Access Control](https://developer.mozilla.org/en-US/docs/HTTP_access_control) and [Server Side Access Control](https://developer.mozilla.org/en-US/docs/Server-Side_Access_Control) | [W3C Cross-Origin Resource Sharing](http://www.w3.org/TR/cors/) |
| `Access-Control-Allow-Origin`      |                                                              | [HTTP Access Control](https://developer.mozilla.org/en-US/docs/HTTP_access_control) and [Server Side Access Control](https://developer.mozilla.org/en-US/docs/Server-Side_Access_Control) | [W3C Cross-Origin Resource Sharing](http://www.w3.org/TR/cors/) |
| `Access-Control-Allow-Methods`     |                                                              | [HTTP Access Control](https://developer.mozilla.org/en-US/docs/HTTP_access_control) and [Server Side Access Control](https://developer.mozilla.org/en-US/docs/Server-Side_Access_Control) | [W3C Cross-Origin Resource Sharing](http://www.w3.org/TR/cors/) |
| `Access-Control-Allow-Headers`     |                                                              | [HTTP Access Control](https://developer.mozilla.org/en-US/docs/HTTP_access_control) and [Server Side Access Control](https://developer.mozilla.org/en-US/docs/Server-Side_Access_Control) | [W3C Cross-Origin Resource Sharing](http://www.w3.org/TR/cors/) |
| `Access-Control-Max-Age`           |                                                              | [HTTP Access Control](https://developer.mozilla.org/en-US/docs/HTTP_access_control) and [Server Side Access Control](https://developer.mozilla.org/en-US/docs/Server-Side_Access_Control) | [W3C Cross-Origin Resource Sharing](http://www.w3.org/TR/cors/) |
| `Access-Control-Expose-Headers`    |                                                              | [HTTP Access Control](https://developer.mozilla.org/en-US/docs/HTTP_access_control) and [Server Side Access Control](https://developer.mozilla.org/en-US/docs/Server-Side_Access_Control) | [W3C Cross-Origin Resource Sharing](http://www.w3.org/TR/cors/) |
| `Access-Control-Request-Method`    |                                                              | [HTTP Access Control](https://developer.mozilla.org/en-US/docs/HTTP_access_control) and [Server Side Access Control](https://developer.mozilla.org/en-US/docs/Server-Side_Access_Control) | [W3C Cross-Origin Resource Sharing](http://www.w3.org/TR/cors/) |
| `Access-Control-Request-Headers`   |                                                              | [HTTP Access Control](https://developer.mozilla.org/en-US/docs/HTTP_access_control) and [Server Side Access Control](https://developer.mozilla.org/en-US/docs/Server-Side_Access_Control) | [W3C Cross-Origin Resource Sharing](http://www.w3.org/TR/cors/) |
| `Age`                              |                                                              |                                                              |                                                              |
| `Allow`                            |                                                              |                                                              |                                                              |
| `Alternates`                       |                                                              | [HTTP Content Negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation) | RFC 2295, §8.3                                               |
| `Authorization`                    |                                                              |                                                              |                                                              |
| `Cache-Control`                    |                                                              | [HTTP Caching FAQ](https://developer.mozilla.org/en-US/docs/HTTP_Caching_FAQ) |                                                              |
| `Connection`                       |                                                              |                                                              |                                                              |
| `Content-Encoding`                 |                                                              |                                                              |                                                              |
| `Content-Language`                 |                                                              |                                                              |                                                              |
| `Content-Length`                   |                                                              |                                                              |                                                              |
| `Content-Location`                 |                                                              |                                                              |                                                              |
| `Content-MD5`                      |                                                              | 未实现 (查看 [bug 232030](https://bugzilla.mozilla.org/show_bug.cgi?id=232030)) |                                                              |
| `Content-Range`                    |                                                              |                                                              |                                                              |
| `Content-Security-Policy`          | 控制用户代理在一个页面上可以加载使用的资源。                 | [CSP (Content Security Policy)](https://developer.mozilla.org/en/Security/CSP) | [W3C Content Security Policy](http://www.w3.org/TR/CSP2/)    |
| `Content-Type`                     | 指示服务器文档的MIME 类型。帮助用户代理（浏览器）去处理接收到的数据。 |                                                              |                                                              |
| `Cookie`                           |                                                              |                                                              | [RFC 2109](http://www.ietf.org/rfc/rfc2109.txt)              |
| `DNT`                              | 设置该值为1， 表明用户明确退出任何形式的网上跟踪。           | Supported by Firefox 4, Firefox 5 for mobile, IE9, and a few major companies. | [Tracking Preference Expression (DNT)](http://www.w3.org/2011/tracking-protection/drafts/tracking-dnt.html) |
| `Date`                             |                                                              |                                                              |                                                              |
| `ETag`                             |                                                              | [HTTP Caching FAQ](https://developer.mozilla.org/en-US/docs/HTTP_Caching_FAQ) |                                                              |
| `Expect`                           |                                                              |                                                              |                                                              |
| `Expires`                          |                                                              | [HTTP Caching FAQ](https://developer.mozilla.org/en-US/docs/HTTP_Caching_FAQ) |                                                              |
| `From`                             |                                                              |                                                              |                                                              |
| `Host`                             |                                                              |                                                              |                                                              |
| `If-Match`                         |                                                              |                                                              |                                                              |
| `If-Modified-Since`                |                                                              | [HTTP Caching FAQ](https://developer.mozilla.org/en-US/docs/HTTP_Caching_FAQ) |                                                              |
| `If-None-Match`                    |                                                              | [HTTP Caching FAQ](https://developer.mozilla.org/en-US/docs/HTTP_Caching_FAQ) |                                                              |
| `If-Range`                         |                                                              |                                                              |                                                              |
| `If-Unmodified-Since`              |                                                              |                                                              |                                                              |
| `Last-Event-ID`                    | 给出服务器在先前HTTP连接上接收的最后事件的ID。用于同步文本/事件流。 | [Server-Sent Events](https://developer.mozilla.org/en-US/docs/Server-sent_events) | [Server-Sent Events spec](http://dev.w3.org/html5/eventsource/) |
| `Last-Modified`                    |                                                              | [HTTP Caching FAQ](https://developer.mozilla.org/en-US/docs/HTTP_Caching_FAQ) |                                                              |
| `Link`                             | 等同于HTML标签中的"link"，但它是在HTTP层上，给出一个与获取的资源相关的URL以及关系的种类。 | For the `rel=prefetch`case, see [Link Prefetching FAQ](https://developer.mozilla.org/en-US/docs/Link_prefetching_FAQ) | Introduced in [HTTP 1.1's RFC 2068, section 19.6.2.4](http://tools.ietf.org/html/rfc2068#section-19.6.2.4), it was removed in the final [HTTP 1.1 spec](http://www.w3.org/Protocols/rfc2616/rfc2616.html), then reintroduced, with some extensions, in [RFC 5988](http://greenbytes.de/tech/webdav/rfc5988.html) |
| `Location`                         |                                                              |                                                              |                                                              |
| `Max-Forwards`                     |                                                              |                                                              |                                                              |
| `Negotiate`                        |                                                              | [HTTP Content Negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation) | RFC 2295, §8.4                                               |
| `Origin`                           |                                                              | [HTTP Access Control](https://developer.mozilla.org/en-US/docs/HTTP_access_control) and [Server Side Access Control](https://developer.mozilla.org/en-US/docs/Server-Side_Access_Control) | More recently defined in the [Fetch spec](https://fetch.spec.whatwg.org/#http-extensions) (see [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API).) Originally defined in [W3C Cross-Origin Resource Sharing](http://www.w3.org/TR/cors/) |
| `Pragma`                           |                                                              | for the pragma: nocache value see [HTTP Caching FAQ](https://developer.mozilla.org/en-US/docs/HTTP_Caching_FAQ) |                                                              |
| `Proxy-Authenticate`               |                                                              |                                                              |                                                              |
| `Proxy-Authorization`              |                                                              |                                                              |                                                              |
| `Range`                            |                                                              |                                                              |                                                              |
| `Referer`                          | （请注意，在HTTP / 0.9规范中引入的正交错误必须在协议的后续版本中保留） |                                                              |                                                              |
| `Retry-After`                      |                                                              |                                                              |                                                              |
| `Sec-Websocket-Extensions`         |                                                              |                                                              | [Websockets](http://tools.ietf.org/html/draft-ietf-hybi-thewebsocketprotocol-07) |
| `Sec-Websocket-Key`                |                                                              |                                                              | [Websockets](http://tools.ietf.org/html/draft-ietf-hybi-thewebsocketprotocol-07) |
| `Sec-Websocket-Origin`             |                                                              |                                                              | [Websockets](http://tools.ietf.org/html/draft-ietf-hybi-thewebsocketprotocol-07) |
| `Sec-Websocket-Protocol`           |                                                              |                                                              | [Websockets](http://tools.ietf.org/html/draft-ietf-hybi-thewebsocketprotocol-07) |
| `Sec-Websocket-Version`            |                                                              |                                                              | [Websockets](http://tools.ietf.org/html/draft-ietf-hybi-thewebsocketprotocol-07) |
| `Server`                           |                                                              |                                                              |                                                              |
| `Set-Cookie`                       |                                                              |                                                              | [RFC 2109](http://www.ietf.org/rfc/rfc2109.txt)              |
| `Set-Cookie2`                      |                                                              |                                                              | [RFC 2965](http://www.ietf.org/rfc/rfc2965.txt)              |
| `Strict-Transport-Security`        |                                                              | [HTTP Strict Transport Security](https://developer.mozilla.org/en-US/docs/Security/HTTP_Strict_Transport_Security) | [IETF reference](http://tools.ietf.org/html/draft-hodges-strict-transport-sec-02) |
| `TCN`                              |                                                              | [HTTP Content Negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation) | RFC 2295, §8.5                                               |
| `TE`                               |                                                              |                                                              |                                                              |
| `Trailer`                          | 列出将在消息正文之后在尾部块中传输的头。这允许服务器计算一些值，如Content-MD5：在传输数据时。请注意，Trailer：标头不得列出Content-Length :, Trailer：或Transfer-Encoding：headers。 |                                                              | [RFC 2616, §14.40](http://tools.ietf.org/html/rfc2616#section-14.40) |
| `Transfer-Encoding`                |                                                              |                                                              |                                                              |
| `Upgrade`                          |                                                              |                                                              |                                                              |
| `User-Agent`                       |                                                              | for Gecko's user agents see the [User Agents Reference](https://developer.mozilla.org/en-US/docs/User_Agent_Strings_Reference) |                                                              |
| `Variant-Vary`                     |                                                              | [HTTP Content Negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation) | RFC 2295, §8.6                                               |
| `Vary`                             | 列出了用作Web服务器选择特定内容的条件的标头。此服务器对于高效和正确缓存发送的资源很重要。 | [HTTP Content Negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation) & [HTTP Caching FAQ](https://developer.mozilla.org/en-US/docs/HTTP_Caching_FAQ) |                                                              |
| `Via`                              |                                                              |                                                              |                                                              |
| `Warning`                          |                                                              |                                                              |                                                              |
| `WWW-Authenticate`                 |                                                              |                                                              |                                                              |
| `X-Content-Duration`               |                                                              | [Configuring servers for Ogg media](https://developer.mozilla.org/en-US/docs/Configuring_servers_for_Ogg_media) |                                                              |
| `X-Content-Security-Policy`        |                                                              | Using [Content Security Policy](https://developer.mozilla.org/en-US/docs/Security/CSP/Using_Content_Security_Policy) |                                                              |
| `X-DNSPrefetch-Control`            |                                                              | [Controlling DNS prefetching](https://developer.mozilla.org/en-US/docs/Controlling_DNS_prefetching) |                                                              |
| `X-Frame-Options`                  |                                                              | [The XFrame-Option Response Header](https://developer.mozilla.org/en-US/docs/The_X-FRAME-OPTIONS_response_header) |                                                              |
| `X-Requested-With`                 | 通常在值为“XMLHttpRequest”时使用                             |                                                              | Not standard                                                 |