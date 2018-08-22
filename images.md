## [WIP]

Images can be represented in two states:

**raw images**
The format of the image when it is taken by a camera. I'm not going into much detail about this, because it's important to be aware of but not of much relevance in the context of the web, but basically it's the format of an unprocessed image.

**Compressed images**
This is how images are mostly presented. PNG,JPEG, GIF, TIFF etc are compressed image formats. after they have been processed

### lossy vs lossless compression
Lossy means that after an image is compressed, it looses any attribute that is not considered essential for displaying it.
Lossless compression in the other hand, means exactly the opposite. Every piece of information that was there before the compression, can be restored when the image is uncompressed

Just because some formats allow lossless compression which is good if you are still going to edit the image, doesn't mean your final image should have all information in it.
As a general rule,use well compressed images in production, because it normally makes no sense to have images wasting bandwith with metadata that is not relevant to the experience you deliver to your user
There are a lot of programs that make good compression on images without negative effects to quality

### png x jpeg x svg x sprites


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

- great if you need to resize your image, while maintaining sharpness, since it's a vector img
- allows you to manipulate the different shapes within the svg, individually using javascript or css

- only supported from  IE 11+
- changing colors and other attributes is done by applying properties such as fill to an element within
- you can only change colors and other visual properties if you load the img in an <svg> | <iframe> | <object> tag . It won't work if you load it within an <img> tag or as a css background image 

### WebP


### gif
- only supports a a limited set of colors so it might not be a good idea to use it in static images , its the most supported format for animated images

#### img-sprites
- great if you need multiple images(specially icons), but want to avoid many round-trips to the server

Although the reason for using them is pretty solid, I generally refrain from using img-sprites because:
 - they require non intuitive calculations for determining which image to show
 - if you need to reuse one of the images in the sprite, you need to request the entire sprite
 - because of the above reason, you are prone to have duplicated images and maintaining them becomes a nightmare
 
 
 refference 
 - [lossless-and-lossy-compression](https://whatis.techtarget.com/definition/lossless-and-lossy-compression)
 - [jpeg-vs-png](https://thrivethemes.com/jpeg-vs-png/)
 - [raw-vs-jpeg](https://digital-photography-school.com/raw-vs-jpeg/)
