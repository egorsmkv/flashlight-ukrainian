# The Ukrainian model (AM) for Flashlight

## Overview

This repository contains the acoustic model for Ukrainian trained on Flashlight framework: https://github.com/flashlight/flashlight/tree/main/flashlight/app/asr

- Architecture: Conformer (30m params)
- Trained epochs: 410

## Quality

- WER: 9.07775%
- TER: 1.98391%

## How to test?

Just with an AM:

```
/root/flashlight/build/bin/asr/fl_asr_test --am /models/uk_am.bin --datadir ''  --emission_dir '' --uselexicon false \
 --test /texts/filtered_cv10_test.lst --tokens /texts/tokens.txt --lexicon /texts/lexicon.txt --show
 ```
 
 With a LM:
 
 ```
 /root/flashlight/build/bin/asr/fl_asr_decode \
  --am=/models/uk_am.bin \
  --test=/texts/filtered_cv10_test.lst \
  --maxload=3477 \
  --nthread_decoder=2 \
  --show \
  --showletters \
  --lexicon=/texts/lexicon.txt \
  --uselexicon=false \
  --lm=/texts/lm_4gram_500k.binary \
  --lmtype=kenlm \
  --decodertype=wrd \
  --beamsize=200 \
  --beamsizetoken=200 \
  --beamthreshold=20 \
  --lmweight=0.75 \
  --wordscore=0 \
  --eosscore=0 \
  --silscore=0 \
  --unkscore=0 \
  --smearing=max
 ```
