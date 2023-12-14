

## CSCI 596 Final Project

# Woven Textile Gravitational Deformation Simulation

## Overview

This project is a generalization of concepts of molecular dynamics in the way that it extends the principles of molecular dynamics, traditionally applied at the atomic and molecular scale, to investigate the dynamics of physical particles at a macroscopic level. While molecular dynamics scrutinizes the behavior of individual atoms and molecules within intricate structures, this project broadens the scope by focusing on the movement of macroscopic particles. In this context, each particle corresponds to a distinct node, representing the intersections of yarns within a textile's mesh structure. 

Woven textiles elongate over time with gravity in the diagonal direction. This phenomenon has nothing to do with stretch, but the weave. Many fabrics are woven in basket weave, which is a simple grid interlocking of yarns and is prone to extending its length diagonally, just like any rectangle would get pulled into a parallelogram with force. In order for clothing pattern pieces to keep their shape, they are cut along the vertical selvage of the fabric where there is very little or no stretch. However, when there are pieces that must be on a diagonal line, the diagonal region can “grow” longer over time, causing an uneven hem. This is common among garments with larger pieces such as dresses. Oftentimes consumers complain that their dresses fit perfectly on the sides but can be one or two inches longer in the center front and center back, giving an impression of low quality.

In couture dress-making methods, these pieces would be draped on the mannequin for an extended time, allowing it to settle to its final shape and then be trimmed, which is a costly process for regular, mass-produced garments. The goal of this project is to simulate the "stretching out" of such textiles with the related parameters applied so the final shape of pattern pieces can be predicted without having to physically draping them. This allows the pattern pieces to be pretrimmed and sewn into garments, and the consumer would have the garment with a final, balanced hem after one or two wears. While the project requirements sheet emphasizes a focus on molecular-level simulations, this project explores a related realm of study that can be seen as a broader application of the principles underlying molecular movements.


## Goal

Develop a comprehensive simulation model for fabric behavior under the influence of gravity, with a specific focus on the diagonal line of fabric pattern pieces. The model will utilize fabric-specific parameters such as weave tightness, weight, and affected area to predict and visualize the deformation of fabric pattern pieces over time. This simulation aims to enable precise pre-trimming and assembly of garments, enhancing the quality and fit of mass-produced textile products, with particular attention to gravity's impact along the diagonal line.



## Objectives

### Preliminary Step: Data Collection through Physical Fabric Draping

#### Objective: 

Gather empirical data by physically draping real fabrics to understand how they behave under gravity and determine the time required for them to settle into their final shape. This data will serve as the basis for establishing parameters and relationships used in the simulation.


#### Methodology:

- Select a set of representative fabric samples with varying characteristics (weave tightness, weight, etc.).

- Draping: Drape each fabric sample on a mannequin or support structure for an extended period to allow it to settle into its final shape.

- Measurement: Precisely measure the elongation or deformation of each fabric sample along the diagonal line and at other key points at specific time intervals (e.g., 1 day, 2 days, etc.).

- Record essential parameters, including initial weave tightness, weight, fabric dimensions, and the time duration of draping.


#### Data Collection:

- Analyze the collected data to identify patterns and relationships between fabric characteristics, time, and fabric behavior under gravity.

- Develop empirical relationships and parameterization formulas based on the analysis, including the time factor.

- Map each representative fabric’s behavior to its specific characteristics including yarn thickness, weave tightness, and weight.



### Step One: Initial Node Configuration

#### Objective: 

Define the initial configuration of nodes based on fabric characteristics to represent the fabric's physical structure, ensuring compatibility with various textile types. Each intersection of two perpendicular yarns is represented by a node within the disk shape of the mesh structure of the textile.


#### Methodology:

- Determine parameters describing fabric characteristics, such as yarn thickness and weave tightness: The tighter the weave, the further apart nodes will be. The thicker the yarn used to weave the fabric, the bigger the nodes are in size.

- Configure nodes within the fabric mesh to mirror the specific fabric's properties.

- Implement constraints: There should be constraints to prevent the user from accidentally inputting data that leads to impractical simulations that go beyond the real behavior of actual textiles. For example, nodes can never overlap since yarns can only go as close to almost touching each other but one yarn can never go into another yarn.



### Step Two: Weight-Dependent Affected Region Calculation

https://ibb.co/3MW0fg4

#### Objective: 

Integrate the weight parameter and calculate the size of the fan-shaped area which gets affected by gravitational deformation due to the structure of the particular fabric.

There are two key factors that affect calculation: the weight of the tightness of the fabric. The weight (ounces per Sq. yard) is given by the textile manufacturer. The tightness is represented by the number of warp (vertical) and weft (horizontal) yarns per inch.


#### How it affects the result of the simulation:


Since the stretching-out effect only occurs around the diagonal grain, the affected areas are typically two portions of the disk shape, which are in the shape of a fan. Meanwhile, the fan shape can be a larger or smaller portion of the disk depending on the structure of the fabric. When the weave is loose, a larger fan region with respect to the disk will be affected by gravity. An example is chiffon fabrics: they are woven so loosely that they are mostly transparent, and they are also some of the most diagonally stretchy fabrics, even though they have no stretch vertically.


#### Methodology:

- Develop a parameterization formula that relates fabric weight to the affected area size. 

- Given that the tightness of the weave and the affected area have an inverse relationship while the weight of the fabric and the affected area have a direct relationship, we can describe the relationship of the affected area for the simulation as:

                     A = T/a​  + b * W + c
Where T represents the tightness of the weave W represents the weight of the fabric weight
            a and b are coefficients that we collected during our preliminary data collection step
            c is a constant based on our experimental experience

- Estimate the size of the fan-shaped affected region based on fabric weave tightness and the given weight parameter.

- Integrate the calculated affected area size and weight parameter into the simulation code.

- Validate simulation results against real-world data to ensure accuracy.



### Step Three: Apply Gravity Force to Fan-shaped Regions

#### Objective: 

Simulate the effect of gravity on the fabric by applying force to the fan-shaped regions, considering the varying weight distribution on each section of the fan shape.


#### Methodology:

- Divide the fan-shaped region into discrete segments to represent the fabric's curvature.

- Calculate the varying weight distribution within each segment based on the fabric's weight parameter.

- Apply a force to each segment, with greater force at the top part and gradually decreasing force towards the bottom.

- Model the response of nodes within each segment, allowing them to move apart in response to the applied force.

- Implement a time parameter to simulate how fabric behavior evolves and find the final settle time for the particular fabric.

- Validate simulation results against real-world observations to ensure accuracy.



## Current State of the Knowledge / Previous Work

In textile engineering and fabric design, current developments have focused on harnessing the unique stretching characteristics of the diagonal grain, often referred to as "bias stretch." Many fabrics exhibit diagonal stretch properties, allowing for increased flexibility and comfort in clothing.

However, it is crucial to recognize that while diagonal stretch can enhance comfort under circumstances, it also has limitations. In certain pattern pieces, especially larger pieces often seen in dresses, the diagonal stretch plays a negative role as it causes an uneven hem after a certain amount of time with the effect of gravity. 

Our project seeks to address the challenges associated with the stretching behavior of diagonal grain in fabrics. While some current trends in textile engineering have leveraged and made use of the diagonal stretch, our project takes a novel approach by focusing on rectifying the potential downsides of this behavior. By addressing and correcting the negative effects of diagonal grain stretch, we aim to offer a cost-effective solution for estimated pre-trimming and shape retention. 



## Techniques to be Used

While the number of nodes in a physical piece of fabric is much smaller than the number of atoms on the microscopic level, the simulation of our project can still benefit from techniques such as parallel computing. Since the fan-shaped regions need to be divided into discrete segments and the movements of nodes within each segment need to be calculated separately, we can take the characteristics of parallel computing, helping us to achieve an accurate and more efficient simulation. 

- Data Parallelism: Dividing the fan-shaped regions into segments and calculating node movements separately is a form of data parallelism. Each segment can be treated as an independent data unit, and computations can be performed concurrently for these segments.

- Concurrency: We can implement concurrency within our code to process these segments simultaneously. Depending on the programming language and framework, techniques like multi-threading or asynchronous programming can be employed.

- Performance Optimization: The use of parallelism in this context can help improve the computational efficiency of our simulations. It allows us to distribute the workload across multiple processing units (e.g., CPU cores) and potentially speed up the calculations.



## Expected Results

Our goal is to develop a versatile simulation tool, potentially in the form of a library, that revolutionizes the way to examine textile behavior under the influence of gravity. This innovative tool will empower users, including manufacturers and designers, to predict and visualize how basket weave fabrics drape and settle into their final shapes, taking into account various fabric parameters such as weight, thread count, weave tightness, and garment sizing.

Key features of the expected result include:

- User-Friendly Interface: The simulation tool will offer an intuitive and user-friendly interface where users can input fabric-specific parameters, including weight, thread count, weave tightness, and garment size.

- Accurate Fabric Behavior Simulation: Leveraging advanced computational techniques, the tool will simulate how fabrics respond to gravity over time. It will precisely predict the deformation and elongation of fabric pattern pieces, particularly along the diagonal grain.

- Pre-Trimming Guides: Based on the simulation results, the tool will provide recommendations for precise pre-trimming and assembly of garments. Manufacturers can optimize their production processes to ensure garments settle into their ideal shapes after one or two wears.

- Ability to Account for Garment Sizing: The simulation tool will accommodate different garment sizes, recognizing that larger sizes may require segmenting into more pieces of smaller flatter stipes of fan shapes for accurate simulation. It will ensure versatility in handling a range of garment sizes.

- Efficiency and Performance: The tool will be designed for computational efficiency, potentially incorporating parallel computing techniques to speed up simulations. This ensures that users can obtain quick and accurate results.

- Applicability Beyond Textiles: While primarily designed for textiles, the principles underlying this project can be extended to other fields, offering insights into the dynamics of interconnected elements at a macroscopic level.





Reference URLs for textile diagonal grain:

https://www.cottoneerfabrics.com/facts-about-fabric-grain/#:~:text=The%20lengthwise%2C%20crosswise%20and%20bias,the%20most%20along%20the%20bias

https://refiberdesigns.com/blog/the-why-and-how-of-stretch-fabrics#:~:text=The%20bias%20stretches%20for%20the,stretch%20(see%20figure%204)
