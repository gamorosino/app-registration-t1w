<h1 align="center">T1w-to-T1w Registration</h1>

<p align="center">
  Registers a moving T1-weighted image to a fixed T1-weighted image with ANTs antsRegistration (translation, rigid, affine and optional SyN stages) and outputs the transforms and the registered image.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/brainlife.app.861"><img src="https://img.shields.io/badge/Brainlife-brainlife.app.861-blue.svg" alt="Run on brainlife.io"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-see_LICENSE-lightgrey.svg" alt="License"></a>
</p>

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Registers a moving T1-weighted image to a fixed T1-weighted image with ANTs antsRegistration (translation, rigid, affine and optional SyN stages) and outputs the transforms and the registered image.**

Runs a multi-stage ANTs registration whose last stage is set by transformation (translation, rigid, affine or nonlinear SyN) and whose multiresolution depth is set by settings, then applies the result to the moving T1w. Use it for intra-subject longitudinal alignment or inter-subject/template normalisation of T1w images; the transforms can be reused by other Apps (for example tract transformation).

| | |
|---|---|
| **Inputs** | `neuro/anat/t1w` ×2 |
| **Outputs** | `neuro/transform/nifti` · `neuro/anat/t1w` |
| **Container** | `brainlife/ants:2.2.0-1bc` |
| **Resources** | 1 CPUs · 2 h walltime |
| **Run it** | [doi.org/10.25663/brainlife.app.861](https://doi.org/10.25663/brainlife.app.861) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `t1_moving` | `neuro/anat/t1w` | yes | T1-weighted image to be registered (moving). |
| `t1_fixed` | `neuro/anat/t1w` | yes | T1-weighted reference image (fixed/target space). |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `transformations` | `neuro/transform/nifti` | ANTs affine (affine.txt) and, for nonlinear registration, the warp and inverse warp fields. |
| `transformed` | `neuro/anat/t1w` | Moving T1w resampled into the fixed image space. |

<details>
<summary><b>Parameters</b> (2)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `settings` | enum | `4` | The `settings` parameter controls the depth of the multiresolution (pyramidal) registration strategy used by ANTs. Higher settings correspond to more levels in the registration pyramid, starting from coarse alignment and progressively refining toward finer spatial correspondence. Options: `1`, `2`, `3`, `4`. |
| `transformation` | enum | `nonlinear` | Last registration stage to run: translation, rigid, affine or nonlinear (SyN); earlier stages are always included. Options: `translation`, `rigid`, `affine`, `nonlinear`. |

</details>

<!-- brainlife-app:end -->

## Running the App

### On brainlife.io

Open the App at [doi.org/10.25663/brainlife.app.861](https://doi.org/10.25663/brainlife.app.861), choose `neuro/anat/t1w`, `neuro/anat/t1w` from your project, set the parameters and press **Execute**. The results are saved to your project as `neuro/transform/nifti`, `neuro/anat/t1w`.

### Locally

You need [Singularity/Apptainer](https://apptainer.org/) (the App runs in `brainlife/ants:2.2.0-1bc`), [`jq`](https://jqlang.github.io/jq/).

1. Clone this repository.
2. Create `config.json` with the paths to your inputs and the parameters:

   ```json
   {
       "t1": "/path/to/t1_moving/t1",
       "t1_fixed": "/path/to/t1_fixed/t1_fixed",
       "settings": "4",
       "transformation": "nonlinear"
   }
   ```

3. Run `./main`.

## Citing

If you use this App, please cite it, the software it builds on and brainlife.io:

- T1w-to-T1w Registration. brainlife.io App. [doi:10.25663/brainlife.app.861](https://doi.org/10.25663/brainlife.app.861)
- Avants, B. B., Tustison, N. J., Song, G., Cook, P. A., Klein, A., & Gee, J. C. (2011). A reproducible evaluation of ANTs similarity metric performance in brain image registration. Neuroimage, 54(3), 2033-2044.
- Hayashi, S., Caron, B. A., Heinsfeld, A. S., ... & Pestilli, F. (2024). brainlife. io: a decentralized and open-source cloud platform to support neuroscience research. Nature methods, 21(5), 809-813. ---
- Avants et al. A reproducible evaluation of ANTs similarity metric performance in brain image registration. *NeuroImage* 54:2033-2044 (2011). [doi:10.1016/j.neuroimage.2010.09.025](https://doi.org/10.1016/j.neuroimage.2010.09.025)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

**Gabriele Amorosino**  
(email:

---

## License

See [LICENSE](LICENSE).
