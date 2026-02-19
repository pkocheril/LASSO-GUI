# LASSO GUI
Graphical interface for performing LASSO spectral unmixing. Continuously a work-in-progress. No guarantees of accuracy, completeness, or functionality.

Written in MATLAB (R2024b).


## Highlights and main functions
* Data loading and saving with file browser windows
* Automatic unmixing and visualization
* Support for up to 12 colors
* Optional spectral normalization


## Prerequisites
Several MATLAB toolboxes (tested in v24.2) are required (or at least recommended):

* Communications Toolbox
* Curve Fitting Toolbox
* DSP System Toolbox
* Image Processing Toolbox
* Optimization Toolbox
* Signal Processing Toolbox
* Statistics and Machine Learning Toolbox
* Symbolic Math Toolbox
* System Identification Toolbox


## Installation
To use the GUI as packaged, simply double-click on the installer (```.mlappinstall```) and the LASSO GUI will install into MATLAB as an application.

Alternatively, the source code can be extracted from the app code file (```.mlapp```) and converted into a traditional MATLAB script (```.m```) to be run with modifications as desired.

## Usage
After installation, the GUI can be launched from the Apps menu in the top banner of MATLAB. Demo data is provided to illustrate the expected file formatting and validate that the code is working.

### Quick start
1. Load reference spectra (```Reference_spectra.csv```)
2. Load the hyperspectral image stack (```GNP_crop_denoised_bkgcorr.tif```)
3. Load the stack imaging parameters (```Frequency_power.csv```). **Frequencies are required**, but powers are optional (needed only if per-frame power correction is desired).
4. Run LASSO. Unmixing results can be viewed as a composite image in the "Results" tab on the right.
5. Tune the hyperparameter (λ) until satisfactory unmixing is achieved.
6. Check the box to "Save results" and run LASSO again. The unmixed results will be saved as a ```.tif``` stack, where the frames are the concentration maps (in the order of the reference spectra).


### Detailed instructions

(Sample images showing the GUI in each step are available in ```Demo/Guide_Images```. In general, if a file path is left empty, the GUI will attempt to use MATLAB's file browser UI to determine the missing paths as needed.)

1. Press the "1. Load reference" button. We load the reference spectra of the individual chemical species to be eventually unmixed (color-coded in order: cyan, yellow, magenta, green, blue, red, etc.). The input for the reference file should be a ```.csv``` file with paired lists of frequency and intensity for each spectrum. The different spectra do not need to have the same x-values. If loaded successfully, the spectra will plot on the axes at the top-right of the window. Optionally, check the "Normalize?" checkbox (prior to loading) to normalize the input reference spectra to a maximum value of 1.
2. Press the "2. Load image" button to load the image stack to be unmixed. Upon loading, the maximal intensity projection along the Z-axis will be plotted in the main window on the right, in the "Input" tab.
3. Press the "3. Load parameters" button to load the parameters for the image stack. Upon loading, open circle markers will be added to the reference spectra, indicating successful interpolation of the reference spectra to match the frequency spacing of the image stack. This is why the frequencies are required. A second column containing power values can also be included for power normalization on a per-frame basis, but this can be omitted if the image stack is already power-corrected.
4. Press the "4. Run LASSO" button. This may take a few seconds. After unmixing, a composite image will be shown in the "Result" tab on the right. The colors of the species correspond to the colors of the reference spectra. We note that the intensities are scaled in this composite to facilitate visualization in MATLAB.
5. Tune the hyperparameter (λ) until satisfactory unmixing is achieved. The larger the value of λ, the fewer species will be assigned to a pixel. After tuning λ, press "4. Run LASSO" again to see the updated results.
6. Once satisfactory unmixing is achieved, check the box for "Save results" and again press the "4. Run LASSO" button. The individual frames of the output image are the concentration maps of the unmixed components (in the order of the reference spectra). The output ```.tif``` stack can then be opened in ImageJ or another image processing program as desired for further visualization.


# How to cite
If you found this code useful, please cite the following paper:

1. RS Chadha‡, PA Kocheril‡, A Colazo‡, ED Kapelczak, B Suen, Z Yang, TA TeSlaa, and L Wei. Optical metabolic imaging of the tricarboxylic acid cycle. DOI: 10.64898/2026.01.28.702395

We also recommend citing the original development of LASSO by Tibshirani (*J. R. Statist. Soc. B*,
**1996**, *58*, 267-288).
