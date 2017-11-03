
## Rendering process

 - first the browser constructs the DOM(Markup)
 - constructs the CSSOM(from CSS rules)
 - generates the Render tree(DOm+CSSOM)
<<<<<<< HEAD
 - calls the layout process to compute the sizes of each element and the position in pixels
 - calls the paint process that actually draws the nodes.

This is the critical rendering path and optimizing it, means to decrease the time each of these operations takes

      !**One thing to notice is that after this process is done, if I do one small change in the CSS, the whole process is repeated**

## Css is a render blocking resource
The browser will stop rendering to load and compute CSS styles. This can be avoided by using a media query when importing a file as follows:
    `<link href="other.css" rel="stylesheet" media="(min-width: 40em)">`
so this resource will not block rendering in devices that dont satisfy the query(since it will not be computed) but will still be downloaded anyways with lower priority

## JS blocking render
JS is another obvious render blocking resource, we can stop it from the critical rendering path(when necessary), by declaring it as async or only running JS after the DOM is ready



### uselful links
[](http://www.stubbornella.org/content/2009/03/27/reflows-repaints-css-performance-making-your-javascript-slow/)
=======
 - 
>>>>>>> c4a37f55405525a4ba50a2bbe11d9a022cdc815f
