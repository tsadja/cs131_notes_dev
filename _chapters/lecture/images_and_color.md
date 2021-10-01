---
title: Images and Color
keywords:
order: 0
---

The Table of Contents:
- [Images, Sampling, and Quantization](#images-sampling-and-quantization)
  - [Types of Images](#types-of-images)
  - [Sampling](#sampling)
  - [Quantization](#quantization)
- [Color Physics](#2-color-physics)
  - [Motivation Question](#motivation-question)
  - [The Physics of Light](#the-physics-of-light)
  - [Photon](#photon)
  - [Radiometry](#radiometry)
  - [Reflectance spectra of surfaces](#reflectance-spectra-of-surfaces)
- [Color Matching](#3-color-matching)
  - [Why Do We Specify Color Numerically?](#why-do-we-specify-color-numerically)
  - [Color Reproduction Concern: Perception](#color-reproduction-concern-perception)
  - [How Do We Sense Light Spectra?](#how-do-we-sense-light-spectra)
  - [The Color Matching Experiment](#the-color-matching-experiment)
  - [How to Measure a Color?](#how-to-measure-a-color?)
- [Color Constancy](#4-color-constancy)
  - [Color Perception](#color-perception)
  - [Lightness Constancy](#lightness-constancy)
  - [Retinex Theory](#retinex-theory)
  - [Moving to a 3D World](#moving-to-a-3d-world)

## 1. Images, Sampling and Quantization

### Types of Images
There exists three main types of images commonly processed using computer vision: binary, grayscale, and color images.

**How do computers store images?** A computer stores an image as a matrix of values. A q by p pixel image is stored in a computer as a matrix with q rows and p columns. Every element inside of the matrix is a pixel, and the data the pixel stores will depend on the type of image. 

- **Binary Images**:

  <p align="center">
    <img src="https://i.imgur.com/6NOAds5.png" width="500"> 
    <div class="figcaption">The first type of image is a binary image.</div>
  </p>

  A binary image is a matrix of pixels, where each pixel can only take two values. In this graphical display, pixels that have a value of '0' are displayed as black, while pixels with a value of '1' are displayed as white.

  <p align="center">
    <img src="https://i.imgur.com/vGHZYeS.png" width="200"> 
    <div class="figcaption">Above is a matrix representation of a binary image. All values are either '0' or '1'. </div>
  </p>


- **Grayscale Images**:

  <p align="center">
    <img src="https://i.imgur.com/iuFQceQ.png" width="500"> 
    <div class="figcaption">The second type of image is a grayscale image.</div>
  </p>

  A grayscale image is also a matrix of pixels, however each pixel is now a value, typically from 0 to 255, corresponding to the intensity of the light at each pixel. The higher the value, the lighter the pixel is, from black to white. Having a different value everywhere gives a way to represent different intensities in grayscale.

  <p align="center">
    <img src="https://i.imgur.com/Zsvd2r2.png" width="200"> 
    <div class="figcaption">Above is a matrix representation of a grayscale image. All values are integers between '0' and '255'. </div>
  </p>


- **Color Images**:


  <p align="center">
    <img src="https://i.imgur.com/KZRaADd.png" width="500"> 
    <div class="figcaption">The third type of image is a color image.</div>
  </p>

  A color image is a matrix of pixels where each pixel holds 3 values, all typically from 0 to 255. There are many ways to encode color, and one of the most common ways is RGB, where the three channels store how much red, green, and blue are in each pixel. 
<p align="center">
<p float="center">
  <img src="https://i.imgur.com/4BsaFME.png" width="200" />
  <img src="https://i.imgur.com/yirz9I9.png" width="200" /> 
  <img src="https://i.imgur.com/1pyZ3UC.png" width="200" />
</p>
</p>

<p align="center">
  <div class="figcaption">The color image above has been split into 3 channels corresponding to the amount of red, blue, and green light in each pixel. Each channel is itself a 2D matrix, with each pixel being the amount of the corresponding color in RGB space.</div>
  </p>


### Sampling

  <p align="center">
    <img src="https://i.imgur.com/iHWKOrT.png" width="200"> 
    <div class="figcaption">This is an example sine wave. The axes are spaced by light intensity.</div>
  </p>
  
    <p align="center">
    <img src="https://i.imgur.com/6WuH64Q.png" width="200"> 
    <div class="figcaption">This is a sampled sine wave. Information is lost as the original sine wave is being sampled at a discrete and finite amount of points.</div>
  </p>

Sampling involves the digitialization of image coordinates values. All digital images are sampled, and are thusly composed of discrete pixels that are arranged in a matrix. This means that the digital image is only an approximation of the real world. 



### Quantization

    <p align="center">
    <img src="https://i.imgur.com/kRWntCz.png" width="200"> 
    <div class="figcaption">This is a quantized sine wave. </div>
  </p>
  
Quantization involves the digitalization of image amplitude values. Due to dissonance between the fundamentally continuous nature of light and the discrete nature of digital images, the values of the individual pixels are also discretized. Therefore, each pixel undergoes a quantization function depending on the image type:

<p align="center">
  <img src="https://i.imgur.com/bNU3en5.png" width="500"> 
</p>


## 2. Color Physics

### Motivation Question
**Why does a visual system need color?**
To tell what food is edible, to distinguish material changes from shading
changes, to group parts of one object together in a scene...


### The Physics of Light
Any patch of light can be completely described physically by its spectrun: the number of photons (per time unit) at each wavelength 400 - 700 nm.

<p align="center">
  <img src="https://i.imgur.com/BlbK6eT.png" width="500"> 
</p>
  
- Example of light sources:
<p align="center">
  <img src="https://i.imgur.com/dbpIYBI.png" width="300">
</p>
  
- Colors and complements:
<p align="center">
  <img src="https://i.imgur.com/q8qljqw.png" width="400">
</p>

- **Additive color mixing**:
  - Colors combine by *adding* color spectra
  - Light adds to black
  - Ex. Cathode Ray Tube phosophors, multiple projectors
<p align="center">
  <img src="https://i.imgur.com/f1qDEvZ.png" width="350">
</p>

- **Subtractive color mixing**:
  - Colors combine by *multiplying* color spectra
  - Pigments remove color from incident light (white) 
  - Ex. Printing on paper, crayons, most photographic film
<p align="center">
  <img src="https://i.imgur.com/8IuyV6n.png" width="350">
</p>


### Photon
There are many possibilities when a photon is emitted:
- **Absorption**: photon absorbed by the surface
- **Diffuse reflection** (diffusion): reflected to any other directions with uniform distribution 
- **Specular Reflection**: reflected with respect to the normal vector of the surface
- **Transparency**: the photon may go through the surface
- **Refraction**: the photon goes through the surface but there is reflection within the surface
- **Flurorescence**: the outgoing photon wavelength is different from the incoming wavelength, and results in a change of colors
- **Subsurface scattering**: photon arrives in a certain surface position, but leaves from different positions
- **Phosphorescence**: there is a delay when the photon leaves the surface
- **Interreflection**: multiple surfaces causing multiple reflections

### Radiometry
- **Radiance** is the power emitted per unit area in a direction, and the directions are specified by polor angle and azimuth
- **Irradiance**: is the total incident power falling on a surface 
<p align="center">
  <img src="https://i.imgur.com/Tn8jTqq.png" width="400">
</p>

- **Bidirectional reflectance distribution function**: 
This function models the local reflection that tells how *bright* a surface appears when viewed from one direction when light falls on it from another 
 <p align="center">
  <img src="https://i.imgur.com/8fXB83n.png" width="400">
</p>

- **BRDF is a very general notion**
  - some surfaces need it 
  - very hard to measure (illuminate from one direction, view from another, repeat)
  - very unstable (minor surface damage can change the BRDF)
  - **For many surfaces, light leaving the surface is largely independent of exit angle** - regardless of the viewing angle, always the same fraction of the incoming light direction


- **Lambertian Reflectance**

  <p align="center">
    <img src="https://i.imgur.com/QQgn85Z.png" width="400">
  </p>
  Lambertian/diffuse surfaces: appear equally bright from all viewing directions (viewing direction no longer necessary in the equation vs. BRDF)

- **Simplified rendering models**
With a Lambertian assumption, element-wise multiplication with illumination gives the color signal
  
  - **BRDF -> reflectance**: For diffuse reflections, we replace the BRDF calculation with a wavelength-by-wavelength scalar multiplication
  
  <p align="center">
    <img src="https://i.imgur.com/uoInRKK.png" width="150">
    <img src="https://i.imgur.com/4ZsfyLu.png" width="600">
  </p>
  
  - **Transmittance**
  <p align="center">
    <img src="https://i.imgur.com/XG0qBug.png" width="200">
    <img src="https://i.imgur.com/tNKIzOc.png" width="600">
  </p>

<a name='ref'></a>

### Reflectance spectra of surfaces
Some surfaces reflect incoming lights (vs. light sources)
<p align="center">
  <img src="https://i.imgur.com/rkZ3YYP.png" width="400">
</p>

Notice that different colours typically have different spectral albedo, but that different spectral albedoes may result in the same perceived color (compare the two whites) because of our own perceptive systems.
<p align="center">
  <img align="center" src="https://i.imgur.com/URZitNz.png" width="400">
</p>


## 3. Color Matching
### Why Do We Specify Color Numerically?
We specify colors numerically, because we want to reproduce the colors accurately often for commercial use, and we want to be able to create a wide range of colors. 

### Color Reproduction Concern: Perception
Humans have photoreceptors specified by 3 cones known as L, M, and S, which are sensitive to different wavelengths. A color's appearance depends on illumination, the eye's adaptation level, and the color and scene surrounding the color influenced by factors such as geometry and color contrast. For the sake of this lecture, we assume the the spectrum of light coming to the eye completely determines the perceived color. 

<p align="center">
  <img src="https://i.imgur.com/kmsTEGh.png" width="350">
  <div class="figcaption">Spectral sensitivities of the L, M, and S cones.</div>
</p>

### How Do We Sense Light Spectra?
Based on the assumption made in the previous section, we can mathematically express the biophysical response to light. We have an input test light, which is projected into 3D space with the dot product between the input spectrum and the cone sensitivity basis vectors. Based on this dot product, we get the L, M, and S responses. 

### The Color Matching Experiment
In the color matching experiment, the subject adjusts the intensities of the 3 primary lights to match the appearance of the test light. Based on experiments, we find that the weight of each primary light can be either positive or negative to match the test light. Furthermore, color matching superposition, also known as Grassman's Law, shows us that if lights A<sub>1</sub> and B<sub>1</sub> are equal and lights A<sub>2</sub> and B<sub>2</sub> are equal, then A<sub>1</sub> + A<sub>2</sub> = B<sub>1</sub> + B<sub>2</sub>.

<p align="center">
  <img src="https://i.imgur.com/HwfIYhI.png" width="500">
  <div class="figcaption">(A) Illustration of the color matching experiment, where the subject views a bipartite field and adjusts the primary colors to match the test light. (B) Appearance of the experiment to the subject.</div>
</p>

### How to Measure a Color?
In order to measure a color, we model our procedure after the color matching experiment. First, choose 3 primary colors. Next, adjust the intensities with positive or negative weights to match the test light. Note that we can have weighted sums of primaries that are different, but ultimately result in the same perception of color because the projection to the 3D space with the cone sensitivity basis vectors leads to the same L, M, and S responses. 

## 4. Color Constancy
### Color Perception
The colors that we perceive are dependent on the colors surrounding them. Even though two colors may have different RGB values, we can still perceive them as the same color. Or, we can look at two colors with the same RGB values and perceive them as different colors

<p align="center">
  <img src="https://i.imgur.com/xtHMAwG.png" width="500">
  <div class="figcaption">An example of this principle. We can see that the squares that appear to have different RGB values are actually the same, and the blue squares that appear to be the same actually have different RGB values.</div>
</p>

<p align="center">
  <img src="https://i.imgur.com/CSGRfcH.png" width="500">
  <div class="figcaption">Another example. In the first figure, although the center square on the left appears to be brighter than the one on the right, they are both the same color. In the second figure, we can tell that the center square is meant to be red, but it does not share the same RGB value as the one on the left.</div>
</p>

The true color of a point cannot be directly inferred from its RGB value in an image. Rather, the effects of illumination on the scene must be considered as well.

### Lightness Constancy
We want to be able to find the true color of a surface regardless of the effects of illumination. We can do so through the equation below. Luminance represents the color that we perceive.
\\[Luminance (L) = Reflectance(R) * Illumination(I)\\] Our goal with this equation is to solve for the reflectance, R, and obtain the true color. This equation is based on the idea of **lightness constancy**.  That is, we will still perceive a surface to have the same reflectance under different lighting conditions because it will always reflect a constant proportion of the light coming in. So, even if we see two objects with the same luminance, we won't think of them as having the same reflectance if the lighting conditions are different because they are reflecting different proportions of light, so  they cannot have the same reflectance. 
<p align="center">
  <img src="https://i.imgur.com/vQQ6Dto.png" width="500">
  <div class="figcaption"> This figure shows how combinations of surfaces with different reflectances and different lighting can produce the same luminance as solutions to the L = IR equation. The example on the left shows no light on a surface with high reflectance. The middle example shows some light on a surface with moderate reflectance. The right example shows bright light on a surface with little reflectance.</div>
</p>


### Retinex Theory
Edges affect the way we perceive color.
<p align="center">
  <img src="https://i.imgur.com/gwnFxqK.png" width="500">
  <div class="figcaption">The Craik O' Brien-Cornsweet Illusion demonstrates how edges can change our perception of color. Though the color we observe on the top shape appears to be darker than the one we observe on the bottom, they do in fact have the same RGB value.</div>
</p>


According to Land and McCann's Retinex theory, this is because edges, or sharp changes in luminance, are due to changes in reflectance, which is why we perceive this as a change in color. Smooth changes in luminance can be explained due to changes in illumination.
<p align="center">
  <img src="https://i.imgur.com/8tYwV6l.png" width="500">
  <div class="figcaption">We perceive the subtle changes in luminance in each rectangle to still have the same reflectance. However, when the change is sharp, we can interpret it as having a different reflectance.</div>
</p>

<p align="center">
  <img src="https://i.imgur.com/SQRCUcH.png" width="500">
  <div class="figcaption">In Knill and Kersten's illusion, why do we perceive both  cylinders to have the same reflectance but the cubes as having different reflectances despite both shapes having the same changes in luminance? This is because the changes in orientation along the surface of the cylinders allows our eyes to explain the change in luminance, whereas the flat surface of the cube does not explain the change in luminance. </div>
</p>



### Moving to a 3D World
In a 3D world, we need to deal with changes in orientation and reflectance edges, making the previous ideas difficult to apply. These are problems that need to be tackled in computer vision.

<p align="center">
  <img src="https://i.imgur.com/iZyj6P4.png" width="500">
  <div class="figcaption">Surfaces in a flat world vs surfaces in a 3D world. Note that in the 3D example, the surfaces have sharp changes in luminance despite having the same reflectance due to the changes in geometry.</div>
</p>


