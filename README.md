# FERMI-correlation-spectroscopy

======================================================
========   Stochastic Spectroscopy at TIMEX   ========
======   An IgorPro 8 suite for data analysis   ======
        written by Dario De Angelis 13/02/2023
======================================================

Step 1:	INSTALLATION 
		- Install IgorPro 8.
		- Copy the "WaveMetrix" folder in your Document folder 
		- Verify XOP Toolkit 8 is properly installed
		- Verify HDF5 Extension is present in
		  C:\Program Files\WaveMetrics\Igor Pro 8 Folder\More Extensions (64-bit)\File Loaders
		  otherwise install it (copy "File Loaders" folder in the aforementioned path

Step 2: EXPERIMENT FILE SETTING
		- Open IgorPro 8 and copy in the procedure the following line:
		  #include "Reconstruction_Live2"
		- Compile the procedure.
		"T-Reconstruction" menu should appear in the menu bar.
		
Step 3: DATA ANALYSIS
		- Load Data (ctrl+1) 
		  Select the "rawdata" folder in the online4eis store.
		  Follow the "Load H5 file" prompt window instruction.
		- Repeat for the back ground data. 
		  BG data are defined as data acquired with no FEL on presto and west. 
		  It is used to subtract the electronic BG of the instruments.
		  Energy calibration is already done for presto spectra. Scaling is set for the presto WAVEs.
		  West will be calibrated afterwards.
		- Subtract background.
		- Reconstruct RIXS
		    Use the panel to select the spectral subrange. 
			(Define with cursors is recommended at the beginning)
			Use default Alpha for the first run
			Set Binning such as Binning > number_of_spectra/1000
		    Binning is the number of chuncks the -huge- dataset is subdivided. 
			Binning = 1 means that dataset is analysed all at once by pseudo-inversion of a matrix about 1000x100000 (n_pixels x n_shots)
			Binning = 100 means inversion of 100 matrices 1000x1000 (much faster and recommended to eliminate part of the noise)
			
			At the end of reconstruction, follow the instruction to calibrate west over presto energy scale.
		- Calculate L-curve
		  Time is needed to calculate RIXS map using a series of values for Alpha. 
		  Repeat for different values of Binning also. Keep the lowest reasonable value for Binning (depending on time consumption and noise on the RIXS map)
		- Select the Alpha value at the corner of the L-curve
		- Calculate the map with selected Binning and Alpha.
		  For datasets with same statistic and same FEL intensity, is reasonable to take the same value and avoid L-curve calculation (keep same spectral ranges!)

