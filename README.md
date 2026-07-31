# Decoding Visual Stimulus Orientation from Mouse Calcium Imaging

An RNN (GRU) built in PyTorch to decode drifting grating orientation from 
two-photon calcium imaging data recorded in mouse visual cortex.

## Motivation
Built this to get hands-on experience with real neuroscience data — working 
directly with calcium imaging traces and trial-based experimental structure — 
and to compare a model that uses the full time-course of neural activity 
against a simple activity-averaging baseline.

## Dataset
[Allen Institute – Visual Coding – Optical Physiology](https://dandiarchive.org/dandiset/000728) 
(DANDI Archive, Dandiset 000728). Two-photon calcium imaging (ΔF/F) from 89 
neurons in mouse visual cortex, recorded while the animal viewed drifting 
gratings at 8 orientations (0°–315°, 45° steps). 598 stimulus trials after 
excluding blank sweeps.

## Approach
- Segmented continuous ΔF/F traces into per-trial windows (0.5s pre-stimulus, 
  1.0s post-stimulus onset) aligned to each grating presentation
- **Baseline**: logistic regression on trial-averaged activity (collapses the 
  time dimension, uses only overall activity level per neuron)
- **RNN**: a GRU that reads the full time-course of population activity per 
  trial and predicts stimulus orientation from its final hidden state
- Custom PyTorch training loop with early stopping and checkpointing on best 
  validation accuracy
- Data loaded by streaming NWB files directly from DANDI's S3 storage 
  (`remfile` + `h5py` + `pynwb`), avoiding local download/corruption issues

## Results

| Model | Accuracy |
|---|---|
| Chance level | 12.5% |
| Baseline (averaged activity) | 18.3% |
| **RNN (full time-course)** | **37.5%** |

The RNN roughly doubled the baseline's accuracy, suggesting the *timing* of 
neural activity within a trial carries meaningful additional information 
about stimulus orientation, beyond what's captured by overall activity level.

The largest confusion is between 90° and 270° — orientations 180° apart. 
This is consistent with known visual cortex physiology: many neurons are 
orientation-selective (responsive to the axis/tilt of a grating) without 
being strongly direction-selective (they don't distinguish which way the 
grating drifts along that axis). Performance varied across orientations, 
with 135° and 180° decoded most reliably; given only 9–22 test trials per 
class, per-class differences should be interpreted with some caution.

## What I'd improve with more time
- Time-resolved decoding analysis — track when within the trial window 
  orientation information first becomes decodable
- Visualize the RNN's hidden states (e.g. via PCA) to see whether trials 
  cluster by orientation in the model's internal representation
- Combine multiple sessions to increase trial count and test generalization 
  across animals
- Try LSTM vs. GRU, and compare against a simple feedforward network on the 
  flattened time-course as an additional baseline

## How to run
Built and run in Google Colab. Data is streamed directly from DANDI 
(no local download required) via `remfile`. Open the notebook and run all 
cells in order.
