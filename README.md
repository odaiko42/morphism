# Image Morphing using Delaunay Triangles

Author: Emmanuel Forgues  
Date: June 13, 2024

## Description

This script performs image morphing between two images using Delaunay triangles. It generates either a series of intermediate images or an animated GIF.

## Usage

```bash
python.exe .\main.py --num_images 50 --image1 .\image1.jpg --image2 .\image2.jpg --output_format gif
Arguments
--num_images: Number of intermediate images to generate (default: 10)
--image1: Path to the first image
--image2: Path to the second image
--output_format: Output format ('images' for intermediate images, 'gif' for an animated GIF, default: 'images')
Required Python Packages
opencv-python
numpy
argparse
tqdm
imageio
Installation
To install the required packages, run:

bash
Copier le code
pip install opencv-python numpy argparse tqdm imageio
Detailed Description
parse_args()
Parses command-line arguments.

Returns:

args: Namespace containing the arguments and their values.
extract_index(points, triangle)
Extracts the indices of the points forming a triangle.

Arguments:

points: List of points in the image.
triangle: List of triangle coordinates.
Returns:

indices: List of indices corresponding to the triangle points.
morph_triangle(img1, img2, img, t1, t2, t, alpha)
Performs morphing between two triangles.

Arguments:

img1: First source image.
img2: Second source image.
img: Destination image for morphing.
t1: Triangle in the first image.
t2: Triangle in the second image.
t: Interpolated triangle.
alpha: Interpolation weight.
morph_images(img1, img2, points1, points2, triangles_indices, alpha)
Performs image morphing using Delaunay triangles.

Arguments:

img1: First source image.
img2: Second source image.
points1: Key points in the first image.
points2: Key points in the second image.
triangles_indices: Indices of Delaunay triangles.
alpha: Interpolation weight.
Returns:

img_morphed: Resulting morphed image.
Creating the pictures directory
The script creates the pictures directory if it does not exist:

python
Copier le code
output_dir = 'pictures'
if not os.path.exists(output_dir):
    os.makedirs(output_dir)
Generating and Saving Morphed Images
The script generates morphed images with a progress bar and saves them either as individual images or as a GIF, depending on the specified output format.

If the output format is images:

python
Copier le code
if args.output_format == 'images':
    cv2.imwrite(os.path.join(output_dir, f'morphed_image_{i}.jpg'), morphed_image)
If the output format is gif:

python
Copier le code
elif args.output_format == 'gif':
    images.append(cv2.cvtColor(morphed_image, cv2.COLOR_BGR2RGB))  # Convert to RGB for imageio
Creating the animated GIF:

python
Copier le code
if args.output_format == 'gif':
    gif_path = os.path.join(output_dir, 'morphed_animation.gif')
    imageio.mimsave(gif_path, images, duration=0.1)
    print(f'GIF created: {gif_path}')
Example
To generate 50 intermediate images and save them as a GIF, run:

bash
Copier le code
python.exe .\main.py --num_images 50 --image1 .\image1.jpg --image2 .\image2.jpg --output_format gif
This will create a series of images or an animated GIF in the pictures directory.

License
This project is licensed under the MIT License - see the LICENSE file for details.

perl
Copier le code

### Notes

- Ensure the paths to `image1.jpg` and `image2.jpg` are correct when running the script.
- The script assumes the `pictures` directory is in the same location as the script unless otherwise specified.

This `README.md` provides a detailed overview of the script, including installation instructions, usage examples, and descriptions of each function and its purpose.