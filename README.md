# DozyState_Detection_CLSA
In our simulated driving experiments, subjects exhibited repeated episodes of dozing off, accompanied by consistent patterns in EEG and EOG signals. When dozing off, an alpha wave attenuation-disappearance phenomenon and alpha blocking phenomenon alternates in the eye-closed periods. As illustrated in Figure, the alpha wave attenuation-disappearance phenomenon exhibits a distinct attenuation pattern during an eye-closed period labeled as Doze², where alpha waves persist until a specific time point before nearly disappearing thereafter. Additionally, alpha blocking—a reduction in alpha rhythm due to visual stimulus attention (e.g., eye opening)—was observed during another eye-closed period labeled as Doze1 in the Figure 1.
 
Figure 1. Two types of dozy states: (1) Type Doze1 is with alpha blocking phenomenon; (2) Type Doze`` is with alpha wave attenuation-disappearance phenomenon. 

As illustrated in the Figure 1, we manually labeled the signals as follows: (1) the Type I alpha wave epoch (AWE), whose start time and end time points are sa1 and ea1 in Doze1, or are sa2 and ea2 in Doze2 ; (2) the rising edge waveform, whose start point is sd1 in Doze1 or sd2 in Doze2; (3) the falling edge waveform, whose end point is ed1 in Doze1 or ed2 in Doze2. A complete dozy state is defined as the period between the start time point sd1 (or sd2) of the rising edge cased by closing eyes and the end time point ed1 (or ed2) of the falling edge caused by reopening eyes. Type I alpha wave epoch (AWE) occurs at the onset of a doze and is characterized by continuous alpha waves. The start time point of Type I AWE is labeled as sa1 or sa2 and its end time point is labeled as ea1 or ea2.

The detection of physiological indicators such as alpha waves, rising/falling edge waveform, was effectively formulated as a classification problem, solvable through machine learning or deep learning approaches. The proposed framework consists of three interconnected sub-modules, each implementing a dedicated CLSA model for specific binary classification tasks. the proposed framework consists of three interconnected sub-modules, each implementing a dedicated CLSA model for specific binary classification tasks:

(1) Alpha wave detection module. The alpha wave detection task is formulated as a time-series binary classification problem. During model development, CLSA 1 was trained using a two-class windowed data samples (alpha wave present vs. absent) to derive the optimal model M1. These two-class windowed data samples are obtained by applying window 1 (1-s duration) as a sliding window across all labeled AWEs and non-AWEs, respectively. These two-class windowed data samples are provided as follows:
 
The code for the CLSA 1 model is:
 
(2) Rising edge waveform detection module.  The rising edge waveform detection problem is formulated as a binary classification task. We train a CLSA 2 model using two-class windowed data samples: one class containing rising edge waveforms and the other without them, thereby obtaining the optimal CLSA 2 model M2. Each positive sample (with rising edge waveform) consists of a 1.5-s window spanning from 0.5 seconds before to 1 second after the labeled start time point sd1 (or sd2) of the rising edge, as shown in Figure 1. Accordingly, the two-class training data uploaded are:
 
The code for the CLSA 2 model is the same as CLSA 1.
 
(3) Doze type determination module. As illustrated in Figure 1, Type I alpha wave epoch (AWE) end time points exhibit two distinct types: (1) one (ea1 in Doze1) associated with the alpha blocking phenomenon, corresponding to the falling edge waveform in VEOG signals, and (2) the other one (ea2 in Doze2) associated with the alpha wave attenuation-disappearance phenomenon, corresponding to smooth line in VEOG signals. The detection of a falling edge waveform indicates an end time point (ea1 ) belonging to the alpha blocking phenomenon, corresponding to the sleepiness level of relaxed wakefulness. In contrast, the absence of this falling edge waveform signifies the end time point (ea2) linked to the alpha wave attenuation-disappearance phenomenon, corresponding to the sleepiness level of sleep onset. Therefore, by detecting the falling edge it is possible to determine whether the end time point type belongs to  Doze1 or Doze2. The falling edge waveform detection problem is formulated as a binary classification task. We train a CLSA 3 model using two-class windowed samples: positive samples containing falling edge waveforms and negative samples without them, thereby obtaining the optimal CLSA 3 model M3. Each positive sample consists of a 1-s window data centered on the labeled end time point of the falling edge. The two-class training data uploaded are:

 
The code for the CLSA 3 model is the same as CLSA 1.
 
During the testing phase, our framework performs simulated real-time detection on continuous test data. The continuous test data (VEOG_O2_raw_S1.mat) and the corresponding manually labeled file(MarkTestingdata_S1.xlsx) for physiological indicators are uploaded as follows:
 
where, VEOG_O2_raw_S1 include two-channel signals: O2 and VEOG.MarkTestingdata_S1.xlsx give the makers for the physiological indicators including, referring to Figure 1:  (1) the Type I alpha wave epoch (AWE), whose start time and end time points are sa1 and ea1 in Doze1, or are sa2 and ea2 in Doze2 ; (2) the rising edge waveform, whose start point is sd1 in Doze1 or sd2 in Doze2; (3) the falling edge waveform, whose end point is ed1 in Doze1 or ed2 in Doze2. A complete dozy state is defined as the period between the start time point sd1 (or sd2) of the rising edge cased by closing eyes and the end time point ed1 (or ed2) of the falling edge caused by reopening eyes. 


The CLSA model was simulated using the Keras deep learning framework, with Windows 11 as the operating system and an NVIDIA GeForce RTX 3060 GPU with 12.0 GB of dedicated memory. The program code for this model was executed in Python 3.8 through Anaconda Navigator, utilizing the Pandas, Keras, and Scikit-learn libraries. 

The continuous test data is the VEOG_O2_raw_S1.mat file, which can be opened and displayed graphically using EEGLAB software.Its corresponding manually labeled file for physiological indicators is MarkTestingdata_S1 .xlsx. 
 






