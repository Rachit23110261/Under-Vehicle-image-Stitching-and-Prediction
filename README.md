# Under-Vehicle Image Stitching and Prediction

## Dataset Information
- **inputimageref**: Contains 48 transformed images.
- **Set01**: Contains 17 non-transformed images.
- **Set-03 full (Zip)**: Contains 135 new images.

## Code Structure
All `.ipynb` files inside `Stitch-images-using-SuperGlue-GNN-master` depend on the SuperGlue model (Models, `match_pairs.py`, etc.). The main working code is in `HALF_HALF.ipynb` inside `Stitch-images-using-SuperGlue-GNN-master`.

### SuperGlue Image Stitching Pipeline

This script automates the process of generating image pairs, running SuperGlue for feature matching, and stitching images into a panorama.

## Setup
1. Place the images in the `adobe_panorama/` or you can put it in any directory which have 'output/' and 'results/' directory.
For a clean push on github, I have removed input images from all the directory sources such as adobe_panaroma, Car_panaroma 1,2, cropped.

## Usage
1. **Generate image pair list**
   ```python
   generate_txt_file("adobe_panorama.txt", [(i, i-1) for i in range(2, 49)])
   ```
   This creates a text file containing image pairs for SuperGlue.

2. **Run SuperGlue feature matching**
   ```python
   run_superglue("adobe_panorama/", "adobe_panorama/output", "adobe_panorama.txt")
   ```
   This runs SuperGlue and stores feature matching results in `adobe_panorama/output`.

3. **Stitch images into a panorama**
   ```python
   stitch_images(1, 48, "adobe_panorama/", "adobe_panorama/output", "adobe_panorama/results")
   ```
   This generates a stitched panorama saved as `adobe_panorama/results/final_result.jpg`.

## Notes
- The script automatically processes images from `1.jpg` to `48.jpg`.
- Change `start_index` and `end_index` to modify the range.
- SuperGlue parameters such as `--match_threshold` can be adjusted in `run_superglue`.

## Output
- Feature match files (`.npz`) are saved in `adobe_panorama/output/`.
- The final stitched image is saved in `adobe_panorama/results/`.

## Other Trial Codes
- `observation.ipynb` (outside `Stitch-images-using-SuperGlue-GNN-master`) is based on simple SIFT features.

