---
title:  ""
search: true
categories: 
  - category_1
  - category_2
tags:
    - tag_1
    - tag_2
toc: true
toc_sticky: true
toc_label: " Index"
toc_icon: "heart"
comments: true
show_date: true
read_time: true
related: true
share: true
excerpt: ""
excerpt_separator: <!--more-->
tagline: "This is a custom tagline content which overrides the *default* page excerpt."
header:
    # video
    video:
        id: 
        provider: 
    # teaser
    teaser: "image url"
    # image
    image: /assets/images/unsplash-image-6.jpg
    og_image: /assets/images/unsplash-image-6.jpg
    caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
    # overlay
    overlay_color: "#333"
    overlay_image: /assets/images/unsplash-image-1.jpg
    overlay_filter: rgba(255, 0, 0, 0.5)
    caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
    actions:
        - label: "Learn more"
        url: "https://unsplash.com"
sidebar:
  - title: "Title"
    image: http://placehold.it/350x250
    image_alt: "image"
    text: "Some text here."
  - title: "Another Title"
    text: "More text here."
    nav: sidebar-sample
gallery:
  - url: /assets/images/unsplash-gallery-image-1.jpg
    image_path: /assets/images/unsplash-gallery-image-1-th.jpg
    alt: "placeholder image 1"
    title: "Image 1 title caption"
    # >> x n
link: https://github.com
last_modified_at: 2018-02-19T08:06:00-05:00
---

<!-- side toc list -->
{% include toc %}

<!-- table template -->
| Parameter  | Required     | Description |
|----------  |---------     | ----------- |
| `id`       | **Required** | ID of the video |
| `provider` | **Required** | Hosting provider of the video, either `youtube` or `vimeo` |

<!-- video embeded -->
{% include video id="XsxDH4HcOWA" provider="youtube" %}
<!-- YouTube video embed below. -->
<iframe width="640" height="360" src="https://www.youtube-nocookie.com/embed/l2Of1-d5E5o?controls=0&amp;showinfo=0" frameborder="0" allowfullscreen></iframe>

<!-- notice markdown -->
**Note:** >> writing and either one as following,
{: .notice--info}
{: .notice--danger}
{: .notice--primary}
{: .notice--warning}
{: .notice--success}

<!-- Quote -->
> Only one thing is impossible for God: To find any sense in any copyright law on the planet.

<!-- link on text -->
[full documentation](https://community.algolia.com/jekyll-algolia/options.html)

<!-- button link -->
[File an issue](https://github.com/mmistakes/minimal-mistakes/issues/new){: .btn .btn--info .btn--large}

<!-- button style -->
<div markdown="0"><a href="#" class="btn">Primary Button</a></div>
<div markdown="0"><a href="#" class="btn btn--success">Success Button</a></div>
<div markdown="0"><a href="#" class="btn btn--warning">Warning Button</a></div>
<div markdown="0"><a href="#" class="btn btn--danger">Danger Button</a></div>
<div markdown="0"><a href="#" class="btn btn--info">Info Button</a></div>

<!-- An example of a Gist embed below. -->
<script src="https://gist.github.com/mmistakes/77c68fbb07731a456805a7b473f47841.js"></script>

<!-- image up -->
<!-- One Up -->
<figure>
	<a href="http://farm9.staticflickr.com/8426/7758832526_cc8f681e48_b.jpg"><img src="http://farm9.staticflickr.com/8426/7758832526_cc8f681e48_c.jpg"></a>
	<figcaption>
        <a href="http://www.flickr.com/photos/80901381@N04/7758832526/" title="Morning Fog Emerging From Trees by A Guy Taking Pictures, on Flickr">Morning Fog Emerging From Trees by A Guy Taking Pictures, on Flickr.</a>
    </figcaption>
</figure>
<!-- Two Up -->
<figure class="half">
    <a href="/assets/images/image-filename-1-large.jpg"><img src="/assets/images/image-filename-1.jpg"></a>
    <a href="/assets/images/image-filename-2-large.jpg"><img src="/assets/images/image-filename-2.jpg"></a>
    <figcaption>Caption describing these two images.</figcaption>
</figure>
<!-- Three Up -->
<figure class="third">
	<img src="/images/image-filename-1.jpg">
	<img src="/images/image-filename-2.jpg">
	<img src="/images/image-filename-3.jpg">
	<figcaption>Caption describing these three images.</figcaption>
</figure>

Image Alignment
{: .align-center}
{: .align-left}
{: .align-right}

<!-- Text Alignment -->
{: style="text-align: left;"}
{: style="text-align: center;"}
{: style="text-align: right;"}
{: style="text-align: justify;"}

```yaml
algolia:
  # Exclude more files from indexing
  files_to_exclude:
    - index.html
    - index.md
    - excluded-file.html
    - _posts/2017-11-28-post-exclude-search.md
    - subdirectory/*.html
```