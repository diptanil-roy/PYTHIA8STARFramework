This is the StRoot implementation of PYTHIA8. In particular, there are filters set up to select two different kinds of PYTHIA events.

1. Events with a D0 meson (D0Filter)
2. Events with a D0 meson inside a jet (D0JetFilter)

The repository already contains PYTHIA STAR Tune (PYTHIA_8_3_03). 

To build this within StRoot, one only needs to include the FASTJET library.

```
cons EXTRA_CXXFLAGS=`fastjet-config --cxxflags`
```

There are 2 macros: `starsim.C` and `starsim_D0jet.C`. `starsim.C` uses the `D0Filter`, while `starsim_D0jet.C` uses the `D0JetFilter`.

##### April 30 2023

If everything above has run properly, then you should have a *.fzd file and *.root file. In case you want the original parton information, you should retain the *.root file. The *.fzd file is the geant output that we are going to feed to the 'Big Full Chain' code.

##### Notes about Big Full Chain (bfc)
Before running bfc, one needs to be aware of a bunch of things.
1. The settings in this file are only valid for Run 14 AuAu 200 GeV (low + mid lumi) MuDst files made with SL16d_embed library. The options will change for other runs. 
2. These options assume that the HFT detector is part of the system. If you need to do analysis without HFT, please contact the STAR embedding pages.

To run the Big Full Chain which converts GEANT File (of digitised PYTHIA events) into MuDst files, these are the steps:
```
starver SL16d_embed
root4star -l -b -q 'runBfc.C(NEvents, "fzdfilename")'
```

##### Making Picos
Ideally, this should be enough if you only want to use MuDsts for your analysis. But if you want to generate picoDsts, you need to do one more step.
```
starver dev
root4star -l -b -q 'genDst.C\(-1,"picoDst,PicoVtxMode:PicoVtxVpdOrDefault,PicoCovMtxMode:PicoCovMtxWrite","mudstfilename")'
```

There you go. You should have a picoDst file ready. The MC Info can be found in MCVertex and MCTracks branches. More information can be found in the StPicoDst class documentation.

