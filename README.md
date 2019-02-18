# Optimize your website for SEO

Here are some tips to optimize your website for SEO:

* [Useful files](#useful-files)
	- [robots.txt](#robotstxt)
	- [sitemap.xml](#sitemapxml)
* [Loading time](#loading-time)
	- [Convert your images to `.webp`](#convert-your-images-to-webp)

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

## Authors

* **Zenoo** - *Initial work* - [Zenoo.fr](https://zenoo.fr)