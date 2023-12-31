# tinySSG

A port from hilmanski/mini-SSG since the project is no longer updated but interesting. Dependencies are updated as needed, and so far got just minor tweaks. More customisation is likely to come later.

So far ... `npm install https://github.com/AndiKod/tinySSG` exposing the NPM Scripts `tinyssg` and `tinyssg -watch` trigering the SSG part.

I'm using that repo by importing it in other projects and it's likely to change over the time. A work in progress and exploration.

## Expected folders Structure

In the project importing tinyssg some folders are expected by the script:

- dev/_components (components with slots)
- dev/_imports (html partials)
- dev/_layouts (regular html with sections slots)
- dev/pages (call a layout, insert needed slots and/or partials)
- dev/static (all from here is copied to /public root)

On save, the content of /public is wiped and replaced with re-rendered html/css/js.

Any change (file addition/supression) in the /dev/pages content is watched and mirored into /public on the fly. Ex: adding /dev/pages/about.html will generate /public/about/index.html 

This is the most basic form. Other folders like devAssets for sass/tailwind/etc consummed by CLI scripts and rendered into /public onChange, are useful.

## Basic Page

```html
<!-- /dev/pages/index.html -->

<!-- Linking the page with /dev/_layouts/base.html -->
@layout(base)  

<!-- Single @section(key, value) tag -->
@section(title, Page Title)

<!-- Pair of @section(key) content @endsection tags -->
@section(main)
<main>
  <h1>My Homepage</h1>
</main>
@endsection
```

## Layout

```html
<!-- /dev/_layouts/base.html -->

<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
  <!-- Get the value of  @section(title, Page Title) -->
	<title>@get(title)</title>
	<link rel="stylesheet" href="style.css">
	<script src="script.js"></script>
</head>
<body>
  <!-- Include partial /dev/_imports/header.html -->
	@inc(header)

  <!-- Get & render the content between @section(main) and @endsection  -->
  <!-- ...from any page calling the layout -->
	@get(main)

  <!-- Include partial /dev/_imports/footer.html -->
  @inc(footer)
</body>
</html>
```

For the components it's unchanged from the original: https://minissg.vercel.app/tour


