# Image Outpainting — ComfyUI Assessment

## Project Overview

This project demonstrates image outpainting using ComfyUI and the Flux.2 Klein 9B model. The workflow extends the original image beyond its existing boundaries to generate additional scene content while aiming to maintain visual consistency.

## Repository Contents

- `2148503361.jpg` — original input image.
- `Flux2Klien_9B_outpaint_v01.json` — ComfyUI outpainting workflow.
- `Outpaint_final_00001_.png` — final outpainted result.

## Workflow

The workflow uses the Flux.2 Klein 9B model to generate content in the extended image area while preserving the original scene as much as possible.

## Usage

1. Install ComfyUI and the required custom nodes.
2. Ensure the required Flux.2 Klein model, text encoder, and VAE are available.
3. Load `Flux2Klien_9B_outpaint_v01.json` into ComfyUI.
4. Load the provided input image and configure the outpainting settings.
5. Run the workflow and review the generated result.

## Output

The repository includes the original input image, the workflow JSON, and the final outpainted image for review.

