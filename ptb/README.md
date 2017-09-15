# Introduction
This is code a modified version of https://www.tensorflow.org/tutorials/recurrent

Use `python ptb_word_lm.py --help` for usage.

By default, LSTMs have hidden sizes of 1500.

# Get ptb data
```
./get_ptd_data.sh
```
# To run
By default, trained models are saved similarly as `/tmp/2017-06-12___22-48-13/`, where foldername is the time when training started.

## learning non-structurally sparse LSTMs with L1-norm regularization
Finetuning trained model by L1-norm regularization
```
python ptb_word_lm.py --model sparselarge \
--data_path simple-examples/data/ \
--restore_path  /tmp/ptb_large_baseline/  \
--config_file l1.json
```
Weight decay of L1-norm, dropout, etc., are configured in `l1.json`.

## learning ISS with group Lasso regularization
```
python ptb_word_lm.py --model sparselarge \
--data_path simple-examples/data/  \
--config_file structure_grouplasso.json 
```
To finetune a model, we can restore the model by `--restore_path ${HOME}/trained_models/ptb/ptb_large_baseline/`, which points to the path of checkpoint files of `model.ckpt-xxx`.

To freeze zero weights during finetuning, we can use `--freeze_mode element`.

## Evaluate and display weight matrices of trained model
```
python ptb_word_lm.py \
--model validtestlarge \
--data_path simple-examples/data/ \
--display_weights True \
--config_file l1.json \
--restore_path /tmp/2017-06-12___22-48-13/
```

## Train two stacked LSTMs with heterogeneous hidden sizes
```
python ptb_word_lm_heter.py \
--model large \
--data_path simple-examples/data/ \
--hidden_size1 373 \
--hidden_size2 315 \
--config_file from_scratch.json 
```

