title: "Learning css over time"
published: 2021-05-11
updated: 2021-05-12
summary: "With the recent heated discussions about whether tailwind is good or harmful to the web, I took some to reflect on the different ways I have used css since when the first time I styled an html element"
tags: [ 'css']

I wrote my first line of CSS code 7 yeas ago as a university student. I'm pretty sure that the concept I had of CSS was similar to how many other people started . At the time , all I knew is that CSS was used to style html documents and I could declare CSS documents either as inline styles, in a style tag within the same document or I could create a separate file with the CSS extension that I could import in my html document(at the time , I was taught that using external stylesheets was a best practice because they alllowed you to separate your styles from your document).

Adding CSS styles was quite simple, just create a selector and then add styles to them. For most cases, I had the option of using element selectors, class, selectors or Id selectors. It was very easy for me to understand why I shouldn't use element selectors, most of the times , I wanted to give different styles to different instances of the same element, therefore, I defaulted to using class selectors when I wanted to style multiple elements of the same "type" and I used id selectors for when I wanted to style a single element, although it also worked on multiple  elements with the same id(yikes).
I also learned that I could combine or nest selectors,  by combining selectors , I was able to find a paragraph that was next to an image, or a link that had an 'active class). By nesting selectors , I was be able to find every paragraph with a title class that was a child of a div with an article class.
Sometimes I'm unsure if I was able to communicate my thoughts clearly, so to exemplify my point above , I shared some code below :

After defining my selectors, to style them , I just needed to add key-value pairs that would describe the property that I wanted change and an associated value .

This was it! No loops , no conditions, no variables, no design patterns or SOLID principles, CSS was just too easy.

After having used it for a year or two, eventually, there would be conflicting CSS rules for the same element defined by different selectors. I didn't understand why those conflicts happened, and honestly, I didn't care , because I learned that I could just add '! important' to the rules I desperately needed to be active, so I kept going.
I used class or id selectors without putting much thought into it. I also combined and nested them as I pleased . Often times , I'd feel superiorly intelligent for writing selectors such as :
Div > P.highlight span:hover

If things didn't work as I expected, I'd just resort to !important or make use slightly different selectors and try not to break other things.

CSS was strange because adding something, caused me to break something else, but I believed that was inherent to the language.

[comment]: <> (<Add CSS meme  here >)


That's when I joined a company that had a very large codebase and in one of  my first PRs, my CSS caused some other components styles to break . In the review I received a comment from one of the senior engineers that basically advised me to only use class selectors and stop nesting selectors. I didn't understand why I should have proceeded as advised, after all nesting selectors seemed like a smart way of styling child elements without adding class names or IDs. Nonetheless, I was given a link to an introductory book on SMACSS that I could use to understand the advice.
The first few pages were enlightening, I learned to calculate the specificity of CSS selectors, I learned why changing the structure of my html , sometimes caused my CSS to break , I learned what I was doing wrong that caused me to resort to !important .
Asides from explaining the bad things about using very specific selectors , the book also suggested a methodology for writing resilient CSS and it was called SMACSS.
I tried to follow the methodology for a while but it was too difficult. I had to open the book and read the rules everytime I needed to write new CSS, so I stopped using it .
Although the  SMACSS methodology didn't work well for me(and my team), that book had provided me with the tools to battle CSS specificity, so I decided to abide by the following rules :
- only use class selectors
- don't nest selectors
- don't combine selectors
  Following these simple rules , allowed me to write css that was resilient to changes in the html structure and by adding specific classes for each specific rules I never again, needed to use !important .
  Fast forward a few months, I also found out about B.E.M that was supposed to be a leaner version of SMACCS, but the problem was the same , having to consult a guide before adding CSS was cumbersome, so B.E.M didn't work well for me either
  Even without BEM or SMACCS ,using the simple rule of avoiding selectors with high specificity still worked well for me, and It became even better when twitter  bootstrap v4 was released and it followed a utility-first approach. At the time I had no interest in building UIs with bootstrap , but I really liked their utility classes and luckily, somewhere in the web, I found a link to a file called bootstrap.utilities.css that contained all bootstrap helper/utility classes.
  This file contained bootstrap responsive classes (col-xs,col-sm, col-md,hidden-xs, visible-lg, etc) as well as a few othe helper classes (eg: h-100, w-100, d-flex, d-block)
  This meant that I was able to build responsive UIs using bootstrap classes,  without the overhead of the presentational styles(eg: alerts, dialogs, jumbotron, etc).
  At this point, I was using this file in all the projects I could  and was very happy with it.

I had heard of tailwind before , but I had dismissed it, since given that I had the bootstrap utility classes, I believed I didn't need another library with utility classes, just because there was a lot of  hype around it.

Since I like to experiment things 
