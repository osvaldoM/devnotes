---
title: "Image formats for the web"
published: 2018-01-22
updated: 2021-02-09
summary: "A summary of the different available formats for web applications"
tags: [ 'web', 'images' ]
---


Images can be represented in two states:

**Raw images**

The format of the image when it is taken by a camera. I'm not going into much detail about this, because it's important to be aware of but not of much relevance in the context of the web, but basically it's the format of an unprocessed image.

**Compressed images**

This is how images are mostly presented. PNG,JPEG, GIF, TIFF etc are compressed image formats. after they have been processed

### Lossy vs lossless compression

Lossy means that after an image is compressed, it looses any attribute that is not considered essential for displaying it.
Lossless compression in the other hand, means exactly the opposite. Every piece of information that was there before the compression, can be restored when the image is uncompressed

Just because some formats allow lossless compression which is good if you are still going to edit the image, doesn't mean your final image should have all information in it.
As a general rule,use well compressed images in production, because it normally makes no sense to have images wasting bandwith with metadata that is not relevant to the experience you deliver to your user
There are a lot of programs that make good compression on images without negative effects to quality. I personally recommend [squooapp](https://squoosh.app/) if you want to have an idea of how much you could optimize an image without noticeable loss in quality

### PNG x JPEG x SVG x SPRITES


#### jpeg

- Lossy compressed img
- JPEG is ideal for images with gradients, several different colors and textures( eg. photos of landscapes, pictures, paintings, etc)

- doesn't allow transparent backgrounds(you have to explicitly make the background of the image match the color of your container/ website)
- Because of it's algorithm, compressing graphic images with JPEG might make the lines and text in your images blurry. which makes in inadequate for this type of image.

#### png

- PNG is usually better with images rich in text, that have sharp lines with clear separation between areas of flat colors and text (eg. icons, flat logos, graphics, etc)
- allows transparent backgrounds

- Creates larger images in terms of size.
- Compressing images with several different colors using PNG will not cause so noticeable negative effects, but will create images with larger size

#### svg

- great if you need to resize your image, while maintaining sharpness, since it's a vector format
- allows you to manipulate the different shapes within the svg, individually using javascript or css

- only supported from  IE 11+
- changing colors and other attributes is done by applying properties such as fill to an element within the svg
- you can only change colors and other visual properties if you load the img in an <svg> | <iframe> | <object> tag . It won't work if you load it within an <img> tag or as a css background image 



### gif
- only supports a a limited set of colors so it might not be a good idea to use it in static images , its the most supported format for animated images
- Despite the limited set of colours that it supports, gifs are usually larger in size compared to other formats

#### img-sprites
- great if you need multiple images(specially icons), but want to avoid many round-trips to the server

Although the reason for using them is pretty solid, I generally refrain from using img-sprites because:
 - they require non intuitive calculations for determining which image to show
 - if you need to reuse one of the images in the sprite, you need to request the entire sprite
 - because of the above reason, you are prone to have duplicated images and maintaining them becomes a nightmare
 
 ### More formats
 #### WebP , JPEGXR
 The interesting thing about these two formats is that at time of this writing, they only work in the browsers that belong to the organizations that created them, and I would only recommend them if you can afford to go the extra mile and cater each browser in a different manner.
 
 WebP is a format created by google that allows 25-34% smaller compressed images compared to PNG and JPEG, while maintaining the same image quality. However, it only works on chrome.
 
 **PS** : you compress can only encode images in either JPEG, PNG or TIFF format into WebP
 
  JPEGXR in the other hand, was created by microsoft and simillarly to WebP, allows better image compression, but it only works from IE8+ and ms edge. 
 
 refference 
 - [lossless-and-lossy-compression](https://whatis.techtarget.com/definition/lossless-and-lossy-compression)
 - [jpeg-vs-png](https://thrivethemes.com/jpeg-vs-png/)
 - [raw-vs-jpeg](https://digital-photography-school.com/raw-vs-jpeg/)
 - [webP](https://developers.google.com/speed/webp/)
