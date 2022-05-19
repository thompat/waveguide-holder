# Generating parameterized waveguide holder designs in OpenSCAD
This repository contains the code used to generate parameterized waveguide holders with [OpenSCAD](https://github.com/openscad/openscad). The waveguide holders were then exported as a .stl file-extension and sliced using [Cura](https://github.com/Ultimaker/Cura) for 3D printing.

#### To-do: Reposition and scale images, label parameters on images, complete example. 

## Purpose

The lab has a rather large waveguide with no practical means of mounting it to the optical bench. This holder is designed to fit tightly around the waveguide and be fastened to an optical post. To future-proof the design of the holder and test the viability of OpenSCAD, a parametric design approach was taken. This code allows the user to specify the cross-sectional height and width of the waveguide being held as well as the desired height from the bottom of the waveguide to the surface on which it rests. The lab uses Thorlabs optical post assemblies with 8-32 threads. All holes present in the holder are fitted for 8-32 screws.

## Design

The waveguide holder has four hexagonal counterbores, two above the waveguide and two on its side. Each counterbore houses a 8-32 nuts that helps secure the waveguide firmly in place. This is achieved using nylon-tipped set screws that thread into the nuts and force the waveguide into the holder. Nylon-tipped screws prevent scratching or otherwise damaging the waveguide. 

![wg_holder_angled](https://user-images.githubusercontent.com/105367588/169372129-8fc5ec4e-1e96-4011-8bcd-5621a27e4e02.png)

![wg_holder_upright](https://user-images.githubusercontent.com/105367588/169372138-b5aa7c61-f5ef-4d26-97ae-c40696516317.png)

## Orthographic Drawing

Below are the orthographic images of the waveguide obtained from the OpenSCAD viewer. The parameters readily changed when using the `waveguide_holder` module are `wg_height` - the height of the hole in which the waveguide will be inserted, `wg_width` - the width of the hole in which the waveguide will be inserted, and `height` - the distance from the bottom of the waveguide to the bottom of the holder. 

Other parameters defined using a `let` statement, along with their pre-defined values are `radius = 1`, `depth = 15`, `thickness = 5`, `separation = 30`, and `number_of_posts = 1`. An explanation of these can be found in the code and the relevant lengths are also labelled on the orthographic images. 

![wg_holder_orthographic1](https://user-images.githubusercontent.com/105367588/169372202-fa003b58-9e3e-42b1-9699-c2d9d5aa0250.png)
![wg_holder_orthographic4](https://user-images.githubusercontent.com/105367588/169372236-fe3871b4-a4bc-416a-8c0a-f3843e16b7c8.png)
![wg_holder_orthographic3](https://user-images.githubusercontent.com/105367588/169372228-108bf176-1bb0-4adf-bacc-3307a1b78754.png)
![wg_holder_orthographic2](https://user-images.githubusercontent.com/105367588/169372250-01c3ca8d-580e-44b9-8cd7-854dcdd85744.png)

## Minor Code Details

For full details, see the comments included in the waveguide-holder-generator file. 

The `waveguide_holder` module uses two helpers, `hex_generator` and `screw_generator` which can be found at the start of the code. These helper modules create a rough approximation for a nut and screw with parameterized diameters and lengths. Both solids are unthreaded but useful for creating the counterbores used in the waveguide holder. There is an unused `nut_generator` which compliments the screw generator. This module simply generators the `hex_generator` solid with a hole in it. 

Useful parameters corresponding to the 8-32 screws and nuts are as follows: `screw_generator(h_diameter = 7.25, t_diameter = 4.5,x-3,x)` for creating counterbores with 3 mm thick material left for the head to rest on, as well as `nut_generator(10,5,4,4.5) and `hex_generator(10,5,4)`. 

## Example

Below is a sample of the reasoning one may use when using this code to achieve certain goals.

Objective: Create a holder that can house a waveguide that is 30 mm wide and 15 mm high, measured facing the waveguide's cross-section. 
Secondary Objective: Make the center of the waveguide rest at 5.5'' when sitting on a fixed height of 2.625''. 
Tertiary Objective: Make the separation parameter larger, perhaps 60 mm instead of 30 mm. 

## Future Implementations



