# CAENet-ASD
Autism Spectrum Disorder (ASD) is a complex neurodevelopmental condition that manifests through a range of symptoms, including difficulties in social communication, impaired social interaction, and restricted or repetitive patterns of behavior and interests. It is estimated to affect approximately one in every 68 children in the United States, though the presentation of symptoms and their severity can vary widely between individuals. Currently, the diagnostic process for ASD relies heavily on behavioral assessments conducted by clinicians. While these methods have proven valuable, they are inherently subjective and can result in inconsistencies across evaluations, particularly when symptoms are subtle or overlap with other developmental conditions.

nspired by Almuqhim and Saeed's ASD-SAENet. A deep learning model created to classify fMRI data from people with Autism Spectrum Disorder (ASD) and typical controls. Here attack the same problem using a concrete autoencoder.

## To Download the ABIDE data
The download_abide_preproc.py script allows any user to download outputs from the ABIDE preprocessed data release. The user specifies the desired derivative, pipeline, and noise removal strategy of interest, and the script finds the data on FCP-INDI's S3 bucket, hosted by Amazon Web Services, and downloads the data to a local directory. The script also allows for phenotypic specifications for targeting only the particpants whose information meets the desired criteria; these specifications include: diagnosis (either ASD, TDC, or both), an age range (e.g. particpants between 2 and 30 years of age), sex (male or female), and site (location where the images where acquired from). * Note the script only downloads images where the functional image's mean framewise displacement is less than 0.2.

At a minimum, the script needs a specific derivative, pipeline, and strategy to search for.
Acceptable derivatives include:
- alff (Amplitude of low frequency fluctuations)
- degree_binarize (Degree centrality with binarized weighting)
- degree_weighted (Degree centrality with correlation weighting)
- eigenvector_binarize (Eigenvector centrality with binarized weighting)
- eigenvector_weighted (Eigenvector centrality with correlation weighting)
- falff (Fractional ALFF)
- func_mask (Functional data mask)
- func_mean (Mean preprocessed functional image)
- func_preproc (Preprocessed functional image)
- lfcd (Local functional connectivity density)
- reho (Regional homogeneity)
- rois_aal (Timeseries extracted from the Automated Anatomical Labeling atlas)
- rois_cc200 (" " from Cameron Craddock's 200 ROI parcellation atlas)
- rois_cc400 (" " " 400 ROI parcellation atlas)
- rois_dosenbach160 (" " from the Dosenbach160 atlas)
- rois_ez (" " from the Eickhoff-Zilles atlas)
- rois_ho (" " from the Harvard-Oxford atlas)
- rois_tt (" " from the Talaraich and Tournoux atlas)
- vmhc (Voxel-mirrored homotopic connectivity)

Acceptable pipelines include:
- ccs
- cpac
- dparsf
- niak

Acceptable strategies include:
- filt_global (band-pass filtering and global signal regression)
- filt_noglobal (band-pass filtering only)
- nofilt_global (global signal regression only)
- nofilt_noglobal (neither)

For example, to download all particpants across all sites' ReHo images processed using C-PAC, without any frequency filtering or global signal regression:
```
    python download_abide_preproc.py -d reho -p cpac -s nofilt_noglobal -o /path/to/local/download/dir
```

The script will then search for and download the data to the local directory specified with the -o flag.

Participants can also be selected based on phenotypic information. For example, to download the same outputs from the previous example, but using only male ASD participants scanned from Caltech between the ages of 2 and 30 years:
```
    python download_abide_preproc.py -a -d reho -p cpac -s nofilt_noglobal -o /path/to/local/download/dir -gt 2 -lt 30 -x M -t Caltech
```

For more information on the ABIDE preprocessed initiative, please check out http://preprocessed-connectomes-project.github.io/abide
## Install Dependencies in a virtual environment
Create a virtual environment
```
python3 -m venv .venv
```
Install Dependencies
```
pip install -r /path/to/requirements.txt
```
## To change the value of the number of features in the latent space you must update the value of K in the second and third cell of the notebook.


