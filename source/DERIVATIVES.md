# Derivatives

This is the part of the data that you will likely be interested to feed in your analyses. This page is still under construction, but should be completed soon.

## Anatomical preprocessing

 WIP

 See fMRIPrep section below for the brain anatomical preprocessing.

## fMRI preprocessing

We are developing a tool [fmriprep_confound_loader](https://github.com/SIMEXP/fmriprep_confound_loader) to load confounds from preprocessing pipeline outputs ([fMRIPrep](https://fmriprep.readthedocs.io/en/stable/#) only for now).

### fMRIPrep

[Version: 1.5.0](https://fmriprep.readthedocs.io/en/stable/installation.html)
Options: slicetiming and recon-all was skipped. (`fmriprep --fs-no-reconall --ignore slicetiming ...`)


FmriPrep is an fMRI data preprocessing pipeline that requires minimal user input, while providing error and output reporting. It performs basic processing steps (coregistration, normalization, unwarping, noise component extraction, segmentation, skullstripping etc.) and provides outputs that can be easily submitted to a variety of group level analyses, including task-based or resting-state fMRI, graph theory measures, surface or volume-based statistics, etc.

The fmriprep pipeline uses a combination of tools from well-known software packages, including FSL, ANTs, FreeSurfer and [AFNI](https://afni.nimh.nih.gov/). This pipeline was designed to provide the best software implementation for each state of preprocessing, and will be updated as newer and better neuroimaging software become available.

For additional information fMRIPrep's installion process, it's pipeline, or it's outputs, please visit it's documentation pages [here]https://fmriprep.readthedocs.io/en/stable/installation.html.



The output can be found in `derivatives/fmriprep`, each participant folder (`sub-*`) contains:

- `anat` folder with T1 preprocessed and segmented in native and MNI space, registration parameters
- `ses-*/func` containing for each fMRI run of that session file prefixed with:
  - `_boldref.nii.gz` : a BOLD single volume reference
  - `_desc-brain_mask.nii.gz` : the brain mask in fMRI space.
  - `_desc-preproc_bold.nii.gz` : the preprocessed BOLD timeseries.
  - `_desc-confounds_regressors.tsv` : a tabular tsv file, containing a large set of confounds to use in analysis steps (eg. GLM). Note that regressors are likely correlated, thus it is recommended to use a subset of these regressors or components of an orthogonal decomposition (eg. PCA) that explains a large share of the variance.
