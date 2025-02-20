# Flashlight for Ukrainian

## Community

- Discord: https://bit.ly/discord-uds
- Speech Recognition: https://t.me/speech_recognition_uk
- Speech Synthesis: https://t.me/speech_synthesis_uk

See other Ukrainian models: https://github.com/egorsmkv/speech-recognition-uk

## Overview

This repository contains the acoustic model for Ukrainian trained on Flashlight framework: https://github.com/flashlight/flashlight/tree/main/flashlight/app/asr

- Architecture: Conformer (300m params)
- Data in train: Common Voice 10 & Voice of America
- Trained epochs: 410
- Train time: around a week (RTX A4000)

### Download

The AM model with configuration files published here: https://huggingface.co/Yehor/flashlight-uk/tree/main

## Quality

- WER: 9.0777% (id est the quality is 90.92%)
- TER: 1.9839%

## How to test?

### Run a container with Flashlight running with CPU

```bash
docker-compose up

# and in another termianl
docker exec -it flashlight_cpu bash
```

### Run

Just with an AM:

```
/root/flashlight/build/bin/asr/fl_asr_test --am /models/uk_am.bin --datadir ''  --emission_dir '' --uselexicon false \
 --test /data/rows.lst --tokens /models/tokens.txt --lexicon /models/lexicon.txt --show
 ```
 
 With an LM:
 
 ```
 /root/flashlight/build/bin/asr/fl_asr_decode \
  --am=/models/uk_am.bin \
  --test=/data/labels_absolute.lst \
  --maxload=3477 \
  --nthread_decoder=2 \
  --show \
  --showletters \
  --lexicon=/models/lexicon.txt \
  --uselexicon=false \
  --lm=/models/lm_4gram_500k.binary \
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

- **labels_absolute.lst** is from https://github.com/egorsmkv/cv10-uk-testset-clean
- **lm_4gram_500k.binary** is from https://huggingface.co/Yehor/kenlm-ukrainian/tree/main/news/lm-4gram-500k

## How to fine-tune on own data?

```
/root/flashlight/build/bin/asr/fl_asr_train continue /models/ --flagsfile /models/train.flags
```

`/models/` must contain .bin files
