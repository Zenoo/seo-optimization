# Optimize your website for SEO

Here are some tips to optimize your website for SEO:

* [Useful files](#useful-files)
	- [robots.txt](#robotstxt)
	- [sitemap.xml](#sitemapxml)
* [Error page](#error-page)
* [Loading time](#loading-time)
	- [Convert your images to `.webp`](#convert-your-images-to-webp)
	- [Delay Javascript non-necessary loading](#delay-javascript-non-necessary-loading)
	- [Load CSS without blocking render](#load-css-without-blocking-render)
* [Mobile version](#mobile-version)
* [Structured Data](#structured-data)
* [Online analyzers](#online-analyzers)

## Useful files

### `robots.txt`

This file is useful for search engines and allows you to tell the engine not to search through some files/folders.

You can also use it to link your `sitemap`.

> `robots.txt`  
> ```
> User-Agent: *
> Disallow: /randomFolder/*
> 
> Sitemap: https://link.to.your/sitemap.xml
>```

If one of your pages is already indexed and you don't want it to be anymore, you can add the tag  
`<meta name="robots" content="NOINDEX,NOFOLLOW" />`  
At the top of your `<head>` tag.

### `sitemap.xml`

This file allows your website to give every useful information it can to search engines for a better indexing.

Informations like the language, the priority level, the last edition date and the edition frequency of each page can help search engines index your website higher.

> `sitemap.xml`  
> ```xml
> <?xml version="1.0" encoding="UTF-8"?>
> <urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
>   <url>
>     <loc>https://your.website.com/</loc>
>     <lastmod>2018-09-11</lastmod>
>     <changefreq>monthly</changefreq>
>     <priority>1.0</priority>
>   </url>
>   <url>
>     <loc>https://your.website.com/another-page</loc>
>     <lastmod>2018-09-11</lastmod>
>     <changefreq>yearly</changefreq>
>     <priority>0.8</priority>
>   </url>
> </urlset>
>```

The `<changefreq>` tag accepts to following values: **always**, **hourly**, **daily**, **weekly**, **monthly**, **yearly**, **never**

The `<priority>` tag value ranges from `0.0` to `1.0`. Its default value if `0.5`.  
It lets search engines know which pages are the most important on your website *(the higher the most important)*.

## Error page

Whenever a page is removed or a user types an URL wrong, it's better to show him a specific error page instead of the default one.  
This page should retain the global aspect of your website and redirect the user to other pages related to his search, in order to keep the user invested.

Creating a `404.html` file and adding

```
ErrorDocument 404 /404.html
```

To your `.htaccess` will do the trick just fine.

## Loading time

### Convert your images to `.webp`

Using the new image format `WebP`, which allows for a powerful image size compression without losing quality can greatly improve your loading time.

I recommend using [WebPConv](http://www.romeolight.com/products/webpconv/) to convert your images to WebP.  
It's easy to use and requires no further configuration.  
The converted files can be found on your Desktop.

I suggest creating a `webp/` folder containing every converted source in your `image` folder, which retain the file tree of your original folder.

Then, all you have to do is replace your basic `<img src="logo.png" alt="Logo" class="whatev">` with:

```HTML
<picture>
  <source srcset="img/webp/logo.webp" type="image/webp">
  <source srcset="img/logo.png" type="image/png">
  <img src="img/logo.png" alt="Logo" class="whatev">
</picture>
```

The browser will first try to load `logo.webp`, if it can't, it will load `logo.png`. If the browser doesn't support the `<picture>` & `<source>` tags, it will default to the `<img>` tag.

### Delay Javascript non-necessary loading

You should try to load as little ressources as possible before the body of your page. The less time your page spends on loading Javascript, the more search engines will have to look at your website.

1. Use the `async` attribute: `<script src="..." async></script>`
2. Place your Javascript code at the end of your `<body>` tag.

### Load CSS without blocking render

Same as the Javascript, you should also deer as many CSS files as you can *(without impacting your page layout, though)*.

The trick here is to load the CSS without blocking the rest of the page.  
Replace your old CSS imports with:

```HTML
<link
  rel="stylesheet"
  href="css/yourcss.min.css" 
  media="none" 
  onload="if(media!='all')media='all'"
>
<noscript>
  <link rel="stylesheet" href="css/yourcss.min.css">
</noscript>
```

First, the `media` attribute of your `<link>` tags is set to `none`, which prevents the browser to load the CSS file.  
The `onload` attribute will set the `media` attribute back to `all`, triggering the loading of the file after the tag has been loaded, so the browser has moved on to render something else.  
If Javascript isn't enabled, the `<noscript>` tag imports your CSS file the usual way, ignoring the above statement.

## Mobile version

Make sure your website is adapted for every device out there. Keep in mind that more than 50% of users are visiting your website from a mobile device.  
Google now uses a mobile-based index, so having a functionnal mobile version is more important than ever.

## Strucutred Data

Including Structured Data on every page of your website will allow Google to display your pages in a better way. See [Intro to Structured Data](https://developers.google.com/search/docs/guides/intro-structured-data) for more informations.

Here is a basic example of what a Breadcrumb Structured Data script will look like in your HTML: 

```HTML
<script type="application/ld+json">
    {
    "@context": "http://schema.org",
    "@type": "BreadcrumbList",
    "itemListElement": [{
        "@type": "ListItem",
        "position": 1,
        "item": {
        "@id": "https://your.website.com/",
        "name": "Home"
        }
    },{
        "@type": "ListItem",
        "position": 2,
        "item": {
        "@id": "https://your.website.com/whatever",
        "name": "Whatever"
        }
    }]
    }
</script>
```

## Online analyzers

- [Google PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/)

## Authors

* **Zenoo** - *Initial work* - [Zenoo.fr](https://zenoo.fr)