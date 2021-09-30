# Color Matching
## Why Do We Specify Color Numerically?
We specify colors numerically, because we want to reproduce the colors accurately often for commercial use, and we want to be able to create a wide range of colors. 

## Color Reproduction Concern: Perception
Humans have photoreceptors specified by 3 cones known as L, M, and S, which are sensitive to different wavelengths. A color's appearance depends on illumination, the eye's adaptation level, and the color and scene surrounding the color influenced by factors such as geometry and color contrast. For the sake of this lecture, we assume the the spectrum of light coming to the eye completely determines the perceived color. 

## How Do We Sense Light Spectra?
Based on the assumption made in the previous section, we can mathematically express the biophysical response to light. We have an input test light, which is projected into 3D space with the dot product between the input spectrum and the cone sensitivity basis vectors. Based on this dot product, we get the L, M, and S responses. 

## The Color Matching Experiment
In the color matching experiment, the subject adjusts the intensities of the 3 primary lights to match the appearance of the test light. Based on experiments, we find that the weight of each primary light can be either positive or negative to match the test light. Furthermore, color matching superposition, also known as Grassman's Law, shows us that if lights A<sub>1</sub> and B<sub>1</sub> are equal and lights A<sub>2</sub> and B<sub>2</sub> are equal, then A<sub>1</sub> + A<sub>2</sub> = B<sub>1</sub> + B<sub>2</sub>.

## How to Measure a Color?
In order to measure a color, we model our procedure after the color matching experiment. First, choose 3 primary colors. Next, adjust the intensities with positive or negative weights to match the test light. Note that we can have weighted sums of primaries that are different, but ultimately result in the same perception of color because the projection to the 3D space with the cone sensitivity basis vectors leads to the same L, M, and S responses. 
