# Correlation-Method-first-2019-
**Paolo Marcoccia<sup>1</sup>, Felicia Frederiksson<sup>2</sup>, Alex B. Nielsen<sup>1</sup> and Germano Nardini<sup>1</sup>**

<sub>1. University of Stavanger, Institutt for Matematikk og Fysikk, Kjølv Egelands hus, 5.etg, E-blokk, 4021 Stavanger, Norway </sub>  
<sub>2. University of Uppsala, Department of Physics and Astronomy,Ångströmlaboratoriet, Lägerhyddsvägen 1, 751 20 Uppsala, Sweden</sub>  

## Introduction ##

In the following, we use the Pearson cross-correlation statistic proposed by [Liu and Jackson](http://iopscience.iop.org/article/10.1088/1475-7516/2016/10/014/meta),
and employed by [Creswell et al.](http://iopscience.iop.org/article/10.1088/1475-7516/2017/08/013/meta), [Nielsen et al.](https://arxiv.org/abs/1811.04071) to look for statistically significant correlations between
the _LIGO_ Hanford and Livingston detectors at the time of the binary black hole mergers detected during _O1_.
Furthermore, the same analysis will be done for event _GW170104_, as problems concerning the residual correlation of the detectors were raised also for that particular event of _O2_ [Creswell et al.](http://iopscience.iop.org/article/10.1088/1475-7516/2017/08/013/meta).
The analysis will follow the same pipelines used in [GW150914_investigation](https://github.com/gwastro/gw150914_investigation), in particular, we will generate the residuals.hdf file for each event by subtracting the Maximum-Likelihood Waveforms generated by [Biwer et al.](https://github.com/gwastro/pycbc-inference-paper), while the raw strain data of the detectors at the time of the events will be obtained by [GWOSC](https://www.gw-openscience.org/catalog/GWTC-1-confident/).
However, we'll use whitened data of the events for the following analysis, and instead of estimating the cross-correlations among the two detectors at the coalescence time suggested by the posteriors, we'll run a new pipeline that will determine the correlations (with a fixed time shift, both for rough strain and residuals) in function of a _200ms_ wide GPS time around the event.
By doing so, we may both observe how the correlations evolve in function of physical time and find the best coalescence time for each event, in order to maximize the correlation value of the original data or the difference among original data and residuals after the subtraction.
The obtained values of the correlations, will then be evaluated from a statistical point of view, by comparing them with the cross-correlation obtained from both simulated Gaussian noise and data from the LIGO detectors, at times during which no detection of gravitational waves has been claimed.
For each event, as a different frequency range was used for the whitening, will be generated a whitened background both for simulated Gaussian noise and data from the _LIGO_ detectors, in order to define the significance of the correlations by comparing with a custom-built environment.     
We find that after subtracting the maximum likelihood waveform, there are no statistically significant correlations between the residuals of the two detectors at the time of all the events reported above.

## Analysis Details ##

Details of the analaysis can be found in our [preprint paper](http://google.com/2r09324).

## Additional Material ##

In order to reproduce the results of our paper, an [Anaconda](https://www.anaconda.com/distribution/) environment with _python 2.7_ is needed.
The supplementary libraries needed, may be checked from the file [init_module.py](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/blob/master/Code/init_module.py).
In particular :

- The notebooks, require the installation of [PyCBC](https://pycbc.org/) v1.12.4 and [LALSuite](https://git.ligo.org/lscsoft/lalsuite) 6.49, which contains version 1.8.0 of the LALSimulation library used to generate the maximum likelihood waveform. Both of these libraries can be installed using [pip](https://pip.pypa.io/en/stable/) with the command:
```sh
pip install 'pycbc==1.12.4' 'lalsuite==6.49'
```
- Some function will require a _C_, _C++_ compiler in order to run, the [GCC](https://gcc.gnu.org/) compiler may be easily installed by running : 

```sh
sudo apt-get update
sudo apt-get install build-essential
```

- A new version of the file [res.py](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/blob/master/Code/res.py) is available in the code directory. The latter, need to be copied and pasted in the directory  
```sh
/home/*username*/anaconda2/lib/python2.7/site-packages
```

- The standard version of [Astropy](https://www.astropy.org/) will result into a problem while downloading the additional needed data due to a server that went down, a new version of the [iers.py](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/blob/master/Code/iers.py) was added in the [code](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/tree/master/Code) directory in order to fix the problem.
The new file should be copied in the directory :

```sh
/home/*username*/anaconda2/lib/python2.7/site-packages/astropy/utils/iers
```

- A copy of the notebooks developed by [Nielsen et al.](https://github.com/gwastro/gw150914_investigation) may be found in the [code](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/tree/master/Code) directory.

## How to run the Correlation Analysis ##

The Correlation Analysis, will be run for a single event at a time.
The steps to do in order to generate the results of our paper are :

1. Download the data of the two detectors _H1_,_L1_ for the event you wish to analyze from [GWOSC](https://www.gw-openscience.org/catalog/GWTC-1-confident/) and copy them in their respective directory, we used the _4096 s_, _4 KHz_ _.gwf_ files for our analysis;

2. Download the posteriors for the events of _O1_ from [Biwer et al.](https://github.com/gwastro/pycbc-inference-paper/tree/master/posteriors), the posteriors for _GW170104_ instead may be found [here](https://github.com/gwastro/o2-bbh-pe/tree/master/posteriors);

3. Run the [CreateResiduals.ipynb](https://github.com/gwastro/gw150914_investigation/blob/master/CreateResiduals.ipynb) to create the _residuals.hdf_ file, the previous notebook was built for _GW150914_, how to run that for other events will be briefly described in the **Additional information** section below. The correctness of the results for the _GW150914_ may be checked from the previous notebook, the results for the other events are written in the files [GW151012obtinf.txt](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/blob/master/Code/GW151012Final/151012obtinf.txt), [GW151226obtinf.txt](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/blob/master/Code/GW151226Final/151226obtinf.txt) and [GW170104obtinf.txt](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/blob/master/Code/GW170104Final/170104obtinf.txt) (There could be small variations in the value of _SNR_ and _Phase Shift_);

4. Run the [CorrVsTime.ipynb](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/blob/master/Code/CorrVsTime.ipynb) to generate the [CorrVsTime.csv](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/blob/master/Code/GW151012Final/CorrVsTime.csv) for the desired event.
The previous notebook was written for [GW151012](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/tree/master/Code/GW151012Final) but the changing needed to be run for other events are pretty straight-forward !

5. Run the [PltCorrVsTime.ipynb](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/blob/master/Code/PltCorrVsTime.ipynb) to plot the [GW*event-name*CorrVsTime.png](https://raw.githubusercontent.com/GravWaves-IMF/Correlation-Method-first-2019-/master/Code/GW151012Final/GW151012CorrVsTime.png?token=AFQOQTNWQSTT6INIMW5PN2S57DOCY) and find the _GPS_ Time of the max strain correlation.
The latter, will be needed to run the next point and is saved in [GW*event-name*data.py](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/blob/master/Code/GW151012Final/GW151012data.py) as <code> cort </code>;

6. Run the [Fig1_Fig2_Correlation.ipynb](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/blob/master/Code/Fig1_Fig2_Correlation.ipynb) to generate the [AllMaxCorrVsTimeShift.png](https://raw.githubusercontent.com/GravWaves-IMF/Correlation-Method-first-2019-/master/Code/AllMaxCorrVsTimeShift.png?token=AFQOQTO2FCNQ2H4BHDMHRBK57HYZQ) figure.
The only correlations needed for our analysis will be generated by <code> In[4] </code> and <code> In[6]</code> of the previous notebook, in order to create the [Fig2.png](https://arxiv.org/pdf/1811.04071.pdf) of the paper.
Furthermore, the <code> strain </code> and <code> resstrain </code> data for the previous analysis may be loaded by running
<code> In[2], In[3], In[5] </code> and <code> In[7] </code> of [CorrVsTime.ipynb](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/blob/master/Code/CorrVsTime.ipynb);

7. Run the [Fig3_Background.ipynb](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/blob/master/Code/Fig3_Background.ipynb) in order to generate the significance curve of correlation in function of the whitening band of the event [AllBackgrounds.png](https://raw.githubusercontent.com/GravWaves-IMF/Correlation-Method-first-2019-/master/Code/Backgrounds/AllBackgrounds.png?token=AFQOQTOMEUSMDWIOUTTATS257H2YA).
This process, would need the [strain]((https://www.gw-openscience.org/catalog/GWTC-1-confident/)) data of _GW150914_ to be run, and would be really slow !!
In the [Backgrounds](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/tree/master/Code/Backgrounds) directory, you would find the [tevent.py](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/blob/master/Code/Backgrounds/tevent.py) script, that once runned will automatically set up the psd starting time _5_ minutes after _GW150914_ coalescence time, as well as an already run version of the background for the various frequency bands.
If you're aiming to rerun the [Fig3_Background.ipynb](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/blob/master/Code/Fig3_Background.ipynb) by yourself, please note that <code> In[5] </code> should be replaced with the whitening function, and you need to generate one background for each whitening frequency range used in your event analysis ! 


## Additional information about the execution of the notebooks

- In order to run the [CreateResiduals.ipynb](https://github.com/gwastro/gw150914_investigation/blob/master/CreateResiduals.ipynb) for events different from _GW150914_, one should first of all move to the choosed event directory using <code> cd _directoryname_ </code>, then check that all the additional data said in points __1)__ and __2)__ of the __How to run__ section was correctly downloaded, and finally launch the two scripts [init_module.py](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/blob/master/Code/init_module.py) and [GW*event-name*data.py](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/blob/master/Code/GW151012Final/GW151012data.py) using the magic command <code> %run _scriptname_ </code>.
Once all these preparation steps are done, the script [CreateResiduals.ipynb] (https://github.com/gwastro/gw150914_investigation/blob/master/CreateResiduals.ipynb) may be easily run for different events by replacing <code> In[3] </code> with the version using auxiliary variables :

  <code> data_files = {'H1': 'H-H1_' + hd_nm, 'L1': 'L-L1_' + hd_nm} </code> 

  and replacing <code> In[9] </code> with line :

  <code> fp = InferenceFile(pst_nm,'r') </code> 
  
- Depending on how old your strain data is, it may be saved either with the acronym _LOSC_ or _GWOSC_, differences in the data sets may results in errors while trying to load the data, so always double check that the name of the files are matching. In particular, the strain arrays inside the data files would have their channel named differently according to what stated at the [GWOSC](https://www.gw-openscience.org/o2_details/), to solve the channel name problem one simply need to replace the '_LOSC-STRAIN_' string passed in <code> In[5] </code> and <code> In[7] </code> at [CreateResiduals.ipynb](https://github.com/gwastro/gw150914_investigation/blob/master/CreateResiduals.ipynb) using '<em>GWOSC-4KHZ_R1_STRAIN</em>'.

- The strain data of event [GW151226](https://github.com/GravWaves-IMF/Correlation-Method-first-2019-/tree/master/Code/GW151226Final) has got _NAN_ values at the start, this will result in numerical errors during the _PSD_ estimation, in particular, you would notice that from a _NAN_ result from <code> Out[20] </code> of [CreateResiduals.ipynb](https://github.com/gwastro/gw150914_investigation/blob/master/CreateResiduals.ipynb). To avoid problems one simply need to add the two labels <code> start_time=psd_start_time-pad_data,
                                     end_time=psd_end_time+pad_data </code> when running reading commands like <code> In[7] </code> in  [CreateResiduals.ipynb](https://github.com/gwastro/gw150914_investigation/blob/master/CreateResiduals.ipynb).
                                     
- If you wish to reproduce the multiple subplots, as done for [AllMaxCorrVsTimeShift.png](https://raw.githubusercontent.com/GravWaves-IMF/Correlation-Method-first-2019-/master/Code/AllMaxCorrVsTimeShift.png?token=AFQOQTO2FCNQ2H4BHDMHRBK57HYZQ) and [AllBackgrounds.png](https://raw.githubusercontent.com/GravWaves-IMF/Correlation-Method-first-2019-/master/Code/Backgrounds/AllBackgrounds.png?token=AFQOQTOMEUSMDWIOUTTATS257H2YA), a guide on how to generate multiple subplots may be found in the [Jake VanderPlas D.S Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/04.08-multiple-subplots.html)                                    
