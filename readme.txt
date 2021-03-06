netrics: a Python 2.7 package for econometric analysis of networks
-----------------------------------------------------------------------------
by Bryan S. Graham, UC - Berkeley, e-mail: bgraham@econ.berkeley.edu


This package includes a Python 2.7 implementation of the two econometric
network formation models introduced in Graham (2014, NBER).

This package is offered "as is", without warranty, implicit or otherwise. While I would
appreciate bug reports, suggestions for improvements and so on, I am unable to provide any
meaningful user-support. Please e-mail me at bgraham@econ.berkeley.edu

Please cite both the code and the underlying source articles listed below when using this 
code in your research.

A simple example script to get started is::

	>>>> # Import numpy in order to correctly read test data
	>>>> import numpy as np

	>>>> # Import urllib in order to download test data from Github repo
	>>>> import urllib

	>>>> # Append location of netrics module base directory to system path
	>>>> # NOTE: only required if permanent install not made 
	>>>> # NOTE: edit path to location on netrics package on local machine
	>>>> import sys
	>>>> sys.path.append('/Users/bgraham/Dropbox/Sites/software/netrics/')

	>>>> # Load netrics module
	>>>> import netrics as netrics
	
	>>>> # Download Nyakatoke test dataset from GitHub
	>>>> download =  '/Users/bgraham/Dropbox/' # Edit to location on your machine   
	>>>> url = 'https://github.com/bryangraham/netrics/blob/master/Notebooks/Nyakatoke_Example.npz?raw=true'
	>>>> urllib.urlretrieve(url, download + "Nyakatoke_Example.npz")

	>>>> # Open dataset
	>>>> NyakatokeTestDataset = np.load(download + "Nyakatoke_Example.npz")

	>>>> # Extract adjacency matrix
	>>>> D = NyakatokeTestDataset['D']

	>>>> # Initialize list of dyad-specific covariates as elements
	>>>> # W = [W0, W1, W2,...WK-1]
	>>>> W = []

	>>>> # Initialize list with covariate labels
	>>>> cov_names = []

	>>>> # Construct list of regressor matrices and corresponding variable names
	>>>> for matrix in NyakatokeTestDataset.files:
	>>>>     if matrix != 'D':
	>>>>         W.append(NyakatokeTestDataset[matrix])
	>>>>         cov_names.append(matrix)   

	>>>> # Apply tetrad logit procedure to dataset	
	>>>> [beta_TL, vcov_beta_TL, tetrad_frac_TL, success] = \
    	 	 netrics.tetrad_logit(D, W, dtcon=None, silent=False, W_names=cov_names)


CODE CITATION
---------------
Graham, Bryan S. (2016). "netrics: a Python 2.7  package for econometric analysis of 
	networks," (Version 0.0.1) [Computer program]. Available at 
	https://github.com/bryangraham/netrics (Accessed 04 September 2016) 
	
PAPER CITATIONS
---------------
Graham, Bryan S. (2014). "An econometric model of link formation with degree 
	heterogeneity," NBER Working Paper No. w20341.	