#LazyLoading #WebPerformance #Preload #Prefetch 
# Lazy Loading
Lazy loading is an `<img>`  attribute, it modifies the download behavior. When a html is readed from the client, web assets are downloaded one by one, when all petitions are successed (or failed) the html document is rendered. Lazy loading avoids the initial downloading of the asset and download the asset when it is needed (reached during scrolling).
```HTML
<img src=".../imgs/img.png" loading="lazy" />
```
# Preload
Preload marks as higher priority download the assets from `<link>` tag.
```HTML
<link rel="preload" href="asset/url/asset.extension" as="extension"/>
```
# Prefetch
Loads assets as "I probably use it in the future", does faster asset loading when the user requires it. [[Google Analytics]] can provide ideas for desition gaps.
```HTML
<link rel="prefetch" href="page/url/about.html" as="document"/>
```
# Image formats
PNG and JPEG are heavier image formats compared with Webp, Webp is the recommended image format to work. Webp is not supported for al web browsers, thus, browser feature checking in the scripting side is required. Modernizer simplify the task, embeding classes to the html tag for the features checking. With this, is easier to manage styles and script paths for the supported or not supported features like webp images rendering.
```HTML
<html>
	<!--> Head block <-->
	<!--> 
	Modernizer script, detects if feature is supported
	Result checking should embed a class name in the html tag
	<-->
	<script src="modernizer.js" defer></script>
</html>
```

```CSS
/*If webp is supported, .banner styles will be selected by this way*/
.webp .banner{
	background: url("img/back.webp");
}
/*Other wise...*/
.no-webp .banner{
	background: url("img/back.png");
}
```
# SEO
`<meta>` tag allows better site description for the site