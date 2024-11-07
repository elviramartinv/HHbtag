# HH-btag   
Interface providing feature computation for CMS RunII HH-btag NN to the identification of the reconstructed b-jets for the final state of hh->bbtautau

# Installation

```sh
cmsrel CMSSW_12_4_10 # or above
cd CMSSW_12_4_10/src
cmsenv
git clone git@github.com:hh-italian-group/HHbtag.git HHTools/HHbtag
scram b
```

# Testing
1. hhBtagTest
Will produce the resulting scores for the input values for two events

# Features

- The reconstructed jets are selected using bbtautau baseline selection for the b jet candidates, describe at the twiki:
https://twiki.cern.ch/twiki/bin/viewauth/CMS/DoubleHiggsToBBTauTauWorkingLegacyRun2#Baseline_selection.

- The maximum number of jets considered considered is 10 for event.

- The jets must be ordered using the corresponding b-tagger (DeepFlavour for v1 & v2 or ParticleNet for v3) score in descending order.

- The taus are selected as specified for the baseline at the working twiki.

- The range used to calculate delta phi should be between [-pi, pi]

- The features used for the training are:

1. jet_pt: pT of each of the jets.
1. jet_eta: eta of each of the jets.
1. rel_jet_M_pt: Relative mass of the b-jet candidate: jet M / jet pT.
1. rel_jet_E_pt Relative energy of the b-jet candidate: jet E / jet pT.
1. jet_htt_deta: Eta between the b-jet and the visible 4-momentum of the HTT.
1. jet_btagScore: The score of the b-jet candidate given by the b-tagger : v1 & v2: DeepFlavour ; v3: ParticleNet
1. jet_htt_dphi: Phi between the b-jet and the visible 4-momentum of the HTT.
1. sample_year: Year of the sample : v1 & v2: (2016, 2017 or 2018); for v3 is era_id: (0 - 2022preEE, 1 - 2022postEE, 2 - 2023preBPix, 3 - 2023postBPix)
1. channelId: v1 & v2: 0 - ETau, 1 - MuTau, 2 - TauTau; v3: 0 - MuTau, 1 - ETau, 2 - TauTau, 3 - MuMu, 4 - EE, 5 - EMu
1. htt_pt: pT of visible 4-momentum of the HTT candidate.
1. htt_eta: eta of HTT visible 4-momentum of the HTT candidate.
1. htt_met_dphi: Phi between the visible 4-momentum of the HTT candidate and the MET.
1. rel_met_pt_htt_pt: Relative MET:  MET / pT of the visible 4-momentum of the HTT candidate.
1. htt_scalar_pt: Sum of the pT of the 2 selected taus.

# Output

The output of the HH-Btag interfase will be a vector with the score for each of the jets.
The two jets with the highest score will be more likely to be originated from the H->bb candidate.

# Model version
v1: Run2 pre-UL samples
v2: Run2 UL samples
v3: Run3 2022+2023 samples