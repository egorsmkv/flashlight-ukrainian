# The Ukrainian Acoustic Model for Flashlight

πΊπ¦ Join Ukrainian Speech Recognition Community - https://t.me/speech_recognition_uk

β­ See other Ukrainian models - https://github.com/egorsmkv/speech-recognition-uk

## Overview

This repository contains the acoustic model for Ukrainian trained on Flashlight framework: https://github.com/flashlight/flashlight/tree/main/flashlight/app/asr

- Architecture: Conformer (30m params)
- Data in train: Common Voice 10 & Voice of America
- Trained epochs: 410
- Train time: around a week

## Quality

- WER: 9.07775% (id est the quality is 90.92%)
- TER: 1.98391%

## Download

All files are here: https://github.com/egorsmkv/flashlight-ukrainian/releases/tag/v1.0

## How to test?

Just with an AM:

```
/root/flashlight/build/bin/asr/fl_asr_test --am /models/uk_am.bin --datadir ''  --emission_dir '' --uselexicon false \
 --test /texts/rows.lst --tokens /texts/tokens.txt --lexicon /texts/lexicon.txt --show
 ```
 
 With a LM:
 
 ```
 /root/flashlight/build/bin/asr/fl_asr_decode \
  --am=/models/uk_am.bin \
  --test=/texts/rows.lst \
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

- **rows.lst** is from https://github.com/egorsmkv/cv10-uk-testset-clean
- **lm_4gram_500k.binary** is from https://huggingface.co/Yehor/kenlm-ukrainian/tree/main/news/lm-4gram-500k

## How to fine-tune on own data?

```
/root/flashlight/build/bin/asr/fl_asr_train continue /models/ --flagsfile /texts/train.flags
```

/models/ must contain .bin files
