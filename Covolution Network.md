# Tips related to CNN
Random knowledge on CNN models
- [Tips related to CNN](#tips-related-to-cnn)
  * [What filters do exactly?](#what-filters-do-exactly-)
  * [Why padding layer is useful?](#why-padding-layer-is-useful-)
  * [Why deeper layers capture larger scale features than previous layers?](#why-deeper-layers-capture-larger-scale-features-than-previous-layers-)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>


## What filters do exactly?
An image kernel is a small matrix used to apply effects like the ones you might find in Photoshop or Gimp, such as blurring, sharpening, outlining or embossing. Here is a link to show some example: https://setosa.io/ev/image-kernels/

For example if we apply identity filter on image we get following:
![enter image description here](https://raw.github.com/XINZHANG-ops/LearningNotes/master/images/identity.png)

 If we apply blur filter on image we get following:
![enter image description here](https://raw.github.com/XINZHANG-ops/LearningNotes/master/images/blur.png)

 If we apply sharpen filter on image we get following:
![enter image description here](https://raw.github.com/XINZHANG-ops/LearningNotes/master/images/sharpen.png)
Thus, it is clear that kernels just like filters we apply on camera photos, different kernels will extract very different features images.


## Why padding layer is useful?
Padding layer is useful due to the reason that convolutional layers pay less attention on image edges.
See this example below without padding, a filter scan through a image. We notice that the 4 corner grids are only scanned once, however, all other grids are scanned twice. Which means the resulting 2by2 image pay less attention on the 4 corners compare to the rest of the grids. Typically, grids closer to center are scanned more than grids on edge, depending on kernel size and stride size.
![enter image description here](https://raw.github.com/XINZHANG-ops/LearningNotes/master/images/no_padding_no_strides.gif)

Now if we add padding(zeros around the image) around the image, we are putting the edge grids torwards center, thus increase their attention. Also the padding values are zero which has no side effect on the result.
![enter image description here](https://raw.github.com/XINZHANG-ops/LearningNotes/master/images/padding_example.png)


## Why deeper layers capture larger scale features than previous layers?
This is counter-intuitive that deeper layers in CNN actually captures larger scale features of image, and the reason is shown below.
Assume Layer1 is the original image, each grid is a pixel. Every gird in Layer2 sees 9 grids in Layer1, and every gird in Layer3 sees 9 grids in Layer2, which means every gird in Layer3 sees all grids in Layer1 in this particular example. Thus previous layers focus more on smaller regions compare to later layers. 
![enter image description here](https://raw.github.com/XINZHANG-ops/LearningNotes/master/images/receptive_field.png)
This is called receptive field in CNN. And in fact, 3 consecutive CNN layers with kernel size 3x3 is equivalent to one 7x7 CNN layer. 
However, use 3 consecutive CNN layers with kernel size 3x3 instead of one 7x7 CNN layer, since 3 consecutive CNN layers with kernel size 3x3 has only 
$$
3 * C * (3 * 3 * C) = 27C^{2}
$$
weights, where C is channel number. 
And one 7x7 CNN layer has 
$$
C * (7 * 7 * C) = 49C^{2}
$$
weights, where C is channel number. 
It is easy to see 3 consecutive CNN layers with kernel size 3x3 has much less weights than one 7x7 CNN layer, which is more efficient.



