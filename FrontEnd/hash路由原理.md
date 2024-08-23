Vue Router 的 Hash 模式是通过使用浏览器的URL哈希来实现客户端路由的。

在 Hash 模式下，Vue Router 会将路由路径追加到 URL 的哈希部分中，而不是将其作为标准的 URL 路径。例如，假设我们有一个路由 /users，在 Hash 模式下，浏览器的 URL 将变为 http://example.com/#/users。

Hash 模式的实现主要依赖于以下几点：

>浏览器的 URL 哈希（Hash）：浏览器的 URL 哈希是指 URL 中的 # 符号后的部分。在 Hash 模式下，Vue Router 会将路由路径追加到 URL 的哈希部分中。
window.location.hash 属性：浏览器提供了 window.location.hash 属性，可以用来读取和设置 URL 的哈希部分。
window.addEventListener('hashchange', ...) 事件：浏览器提供了 hashchange 事件，当 URL 的哈希部分发生变化时，该事件将被触发。Vue Router 会监听这个事件，以便在路由变化时更新应用状态。
当用户点击链接或使用浏览器的前进和后退按钮时，浏览器的 URL 哈希部分将发生变化。Vue Router会监听 hashchange 事件，并根据新的哈希值来更新应用状态和渲染对应的路由组件。

Hash 模式的优点是：
> 不需要服务器端支持，可以在客户端完全实现路由。
可以在不刷新页面的情况下实现路由切换。

然而，Hash 模式也有一些缺点，例如：
>SEO 不友好，因为搜索引擎无法索引哈希路由。
不支持服务器端渲染（SSR），因为服务器端无法获取哈希路由信息。

知道原理及如何获取hash属性后，可以解决我遇到过的场景：企业微信登录回调中返回的地址是这样的格式：`http://localhost:8090/?code=12212121ertfertr&a=100&&&&#/reputationRisk/workstand/home`
参数被加在原本的/#/中间，虽然对页面没影响，但是路径显得很乱，如果要剔除掉参数，之前我是使用匹配正则，现在知道原理后，可以直接使用hash属性来获取，代码如下：
```javascript
const hash = window.location.hash;
const url = window.location.origin + '/' +  hash //获取到完整的hash地址
```
