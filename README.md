This is the StRoot implementation of PYTHIA8. In particular, there are filters set up to select two different kinds of PYTHIA events.

1. Events with a D0 meson (D0Filter)
2. Events with a D0 meson inside a jet (D0JetFilter)

The repository already contains PYTHIA STAR Tune (PYTHIA_8_3_03). 

To build this within StRoot, one only needs to include the FASTJET library.

```
cons EXTRA_CXXFLAGS=`fastjet-config --cxxflags`
```

There are 2 macros: starsim.C and starsim_D0jet.C. `starsim.C` uses the `D0Filter`, while `starsim_D0jet.C` uses the `D0JetFilter`.
