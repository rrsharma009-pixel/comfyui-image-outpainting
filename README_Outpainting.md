# Test 1 — Image Outpainting

## Project overview

This project extends the canvas of an existing photograph and generates plausible surrounding scene content in the newly added areas. The goal is to create a wider composition while retaining the original subject and the visual character of the source photograph.

## Files

- `2148503361.jpg` — original input image (667 × 1000 pixels).
- `Outpaint_final_00001_.png` — generated outpainting result (1488 × 992 pixels).
- `Flux2Klien_9B_outpaint_v01.json` — ComfyUI workflow.

## Workflow

The workflow uses ComfyUI with the Pixaroma outpainting nodes and the FLUX.2 Klein 9B model.

1. Load the source photograph with `PixaromaLoadImageMini`.
2. Use `PixaromaOutpaint` to define the expanded canvas.
3. Encode the expanded image with the VAE and prepare the latent input.
4. Apply the text conditioning and generate the extended scene with the sampler.
5. Decode the generated result.
6. Use `PixaromaOutpaintStitch` to combine the generated area with the original image region.
7. Save the result with the `Outpaint_final` filename prefix.

## Model and key settings

- **Diffusion model:** `flux2/flux-2-klein-9b-int8-convrot.safetensors`
- **Text encoder:** `qwen_3_8b_fp8mixed.safetensors` (FLUX.2 type)
- **VAE:** `flux2-vae.safetensors`
- **LoRA:** `Flux/pixaoutpaint.safetensors`, enabled at strength 1.0
- **Prompt text:** `pixaoutpaint, replace the solid gray area by naturally extending the surrounding scene`
- **Sampler:** Euler
- **Scheduler:** Simple
- **Steps:** 8
- **CFG:** 1
- **Stitch feather:** 64
- **Stitch color match:** 100

The workflow uses the Pixaroma outpainting interface to set the canvas and outpainting region. The final output is 1488 × 992 pixels. The exact outpaint region depends on the saved settings in the Pixaroma node interface.

## Installation and requirements

1. Install ComfyUI.
2. Install the custom node pack `ComfyUI-Pixaroma` and its required dependencies.
3. Place the model files in the appropriate ComfyUI model folders:
   - FLUX.2 Klein model in the diffusion model folder expected by `UNETLoader`.
   - Qwen 3 8B FP8 mixed text encoder in the CLIP/text-encoder folder.
   - FLUX.2 VAE in the VAE folder.
   - `pixaoutpaint.safetensors` in the LoRA folder.
4. Restart ComfyUI and load `Flux2Klien_9B_outpaint_v01.json`.
5. If the workflow's custom-node UI state does not restore, reopen the Pixaroma outpainting interface and set the desired canvas/regions before running.

## How to run

1. Load the input image.
2. Open the `PixaromaOutpaint` node and confirm the expanded canvas and outpaint area.
3. Confirm the positive prompt and model selections.
4. Queue the workflow.
5. Inspect the stitched result for visible seams, repeated details, or inconsistent perspective.
6. Save the final image.

## Evaluation

The output should be assessed by comparing it with the source image and checking:

- whether the original subject remains visually consistent;
- whether the generated extension fits the surrounding environment;
- whether lighting, perspective, and texture remain coherent;
- whether the stitch boundary is visible;
- whether any generated content contains distortions or repetition.

The supplied output demonstrates an expanded landscape composition from the original portrait-oriented image. This README does not claim a numerical quality score or a formal benchmark evaluation.

## Notes and limitations

- This is an inference workflow using pretrained models; it does not train a new model.
- Results depend on the selected outpaint region, prompt, model versions, and random seed.
- Custom nodes and model weights are not included in this project folder; install them separately.
- The workflow's sampler seed is managed through a Pixaroma seed node configured for fixed mode in the saved workflow, but the sampler's visible seed input is driven by that node.
