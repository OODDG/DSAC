# Exploring Domain Shift Across Continents in Satellite Imagery Classification
<!--- 
## DSAC - Domain Shift Across Continents Dataset and Experiments
--->

<!---
Exploring Domain Shift Across Continents in Satellite Imagery Classification
Dataset and code coming soon!
--->

This repository includes Domain Shift Across Continents (<b>DSAC</b>) dataset and the code discussed in our paper [Exploring Domain Shift Across Continents in Satellite Imagery Classification](https://openreview.net/forum?id=AXc3X2nsbu&referrer=%5BAuthor%20Console%5D(%2Fgroup%3Fid%3DNeurIPS.cc%2F2023%2FTrack%2FDatasets_and_Benchmarks%2FAuthors%23your-submissions)).



--------------------------------------------------------------------------------
## DSAC Experiments - Dataset

--------------------------------------------------------------------------------

## DSAC Experiments - Specific Instructions 

<!---
Exploring Domain Shift Across Continents in Satellite Imagery Classification
Dataset and code coming soon!
--->

In this repo, we share the code and detailed instructions on how to replicate the experiments discussed in our paper [Exploring Domain Shift Across Continents in Satellite Imagery Classification](https://openreview.net/forum?id=AXc3X2nsbu&referrer=%5BAuthor%20Console%5D(%2Fgroup%3Fid%3DNeurIPS.cc%2F2023%2FTrack%2FDatasets_and_Benchmarks%2FAuthors%23your-submissions)).

<b>DSAC_Experiment_1_2</b> and <b>DSAC_Experiment_3</b> under DSAC_Experiment are a fork of the original WILDS repository. However, it is important to note that we have modified the underlying code extensively to suit our designed experimental setup and integrate our dataset. 

To run experiments 1 and/or 2, start by downloading the DSAC_Experiments_1_2. Similarly, if you are interested in Experiment 3, then download the directory DSAC_Experiment_3. 

Once the download is complete, install our version of WILDS package using:



```bash
cd DSAC_Experiments_1_2/wilds # Or DSAC_Experiment_3/wilds
pip install -e .
```
Next, download the original fMoW raw dataset as per the instructions in [WILDS](https://github.com/p-lambda/wilds) package.

<hr style="border:2px solid gray">

<ul>

## Experiment on the Upper Bound

</ul>


<ul>
<ul>

### Training and validating 
The following commend is used to train a model in the upperbound experiment:

```bash
python ./examples/run_expt.py --uniform_over_groups True \
--dataset fmow --seed SEED --algorithm ALGORITHM --root_dir wilds_fmow --log_dir LOG_DIRECTORY \
--n_epochs 50 --groupby_fields region --batch_size 64 --source_target_path PATH_TO_SOURCE_DATA_FILE \
--dataset_kwargs use_ood_val=False --evaluate_all_splits False
```
Where the <code>PATH_TO_SOURCE_DATA_FILE</code> is the path to the source domain(s) directory. For example in this experiment, the path is defined as:
```bash
... --source_target_path DSAC_Dataset/source_domains/Experiment_UpperBound_Dataset/exp_source_upperbound.csv ... 
```
</ul>

<ul>

### Evaluating and Testing
```bash
# For ERM and GroupDRO
python ./examples/run_expt.py --dataset fmow --algorithm ALGORTIHM --uniform_over_groups True --seed SEED --root_dir wilds_fmow \
--log_dir LOG_DIRECTORY  --batch_size 64 --groupby_fields region --log_every 1 --source_target_path PATH_TO_TARGET_DATA_FILE \
--eval_only True --evaluate_all_splits False --eval_splits iid_test

# For IRM and deepCORAL
python ./examples/run_expt.py --dataset fmow --algorithm ALGORTIHM --seed SEED --n_groups_per_batch 1 --uniform_over_groups True \
--root_dir wilds_fmow --log_dir LOG_DIRECTORY  --batch_size 64 --groupby_fields region --log_every 1 --source_target_path PATH_TO_TARGET_DATA_FILE \
--eval_only True --evaluate_all_splits False --eval_splits iid_test

```
</ul>
</ul>





--------------------------------------------------------------------------------

<ul>

## Experiment 1: Single-Source Domain

</ul>

<ul>
<ul>

### Training and validating 
The following commend is used to train a model in Experiment 1:

```bash
python ./examples/run_expt.py --uniform_over_groups True --dataset fmow --seed SEED --algorithm ALGORITHM --root_dir wilds_fmow \
  --log_dir LOG_DIRECTORY --n_epochs 50 --groupby_fields region --batch_size 64 --source_target_path PATH_TO_SOURCE_DATA_FILE \
  --dataset_kwargs use_ood_val=False --evaluate_all_splits False 
```
Where the <code>PATH_TO_SOURCE_DATA_FILE</code> is the path to the source domain directory. For example, if the source domain is Africa, the path is defined as:

```bash
... --source_target_path DSAC_Dataset/source_domains/Experiment_1_Dataset/exp_1_source_Africa.csv ... 
```
### Evaluating and Testing

```bash
# For ERM and groupDRO
python ./examples/run_expt.py --dataset fmow --algorithm ALGORTIHM --seed SEED --root_dir wilds_fmow --log_dir LOG_DIRECTORY  \
--batch_size 64 --groupby_fields region --log_every 1 --source_target_path PATH_TO_TARGET_DATA_FILE \
--eval_only True --evaluate_all_splits False --eval_splits iid_test

# For IRM and deepCORAL
python ./examples/run_expt.py --dataset fmow --algorithm ALGORTIHM --seed SEED --n_groups_per_batch 1 --uniform_over_groups True --root_dir wilds_fmow --log_dir LOG_DIRECTORY  \
--batch_size 64 --groupby_fields region --log_every 1 --source_target_path PATH_TO_TARGET_DATA_FILE \
--eval_only True --evaluate_all_splits False --eval_splits iid_test
```

</ul>
</ul>

--------------------------------------------------------------------------------
<ul>

## Experiment 2: Multi-Source Domains

</ul>

<ul>
<ul>

### Training and validating 
The following commend is used to train a model in Experiment 2:

```bash
# For ERM and GroupDRO
python ./examples/run_expt.py --dataset fmow --seed SEED --algorithm ALGORITHM --root_dir wilds_fmow --log_dir LOG_DIRECTORY --n_epochs 50 \
--groupby_fields region --batch_size 60 --source_target_path PATH_TO_SOURCE_DATA_FILE --dataset_kwargs use_ood_val=False --evaluate_all_splits False

# For IRM and deepCORAL
python ./examples/run_expt.py --dataset fmow --n_groups_per_batch 5 --uniform_over_groups True \
  --seed SEED --algorithm ALGORITHM --root_dir wilds_fmow --log_dir LOG_DIRECTORY --n_epochs 50 --groupby_fields region --batch_size 60 \
  --uniform_over_groups True --source_target_path PATH_TO_SOURCE_DATA_FILE --dataset_kwargs use_ood_val=False --evaluate_all_splits False 2>&1
```
Where the <code>PATH_TO_SOURCE_DATA_FILE</code> is the path to the source domains directory. For example, if the target (left-out) domain is Africa, the path is defined as:

```bash
... --source_target_path DSAC_Dataset/source_domains/Experiment_2_Dataset/exp_2_source_Africa.csv ... 
```
### Evaluating and Testing
```bash
# For ERM and GroupDRO
python ./examples/run_expt.py --dataset fmow --algorithm ALGORTIHM --seed SEED --root_dir wilds_fmow --log_dir LOG_DIRECTORY  --batch_size 64 \
--groupby_fields region --log_every 1 --source_target_path PATH_TO_TARGET_DATA_FILE --eval_only True --evaluate_all_splits False \
--eval_splits iid_test

# For IRM and deepCORAL
python ./examples/run_expt.py --dataset fmow --n_groups_per_batch 5 --uniform_over_groups True --algorithm ALGORTIHM --seed SEED \
--root_dir wilds_fmow --log_dir LOG_DIRECTORY  --batch_size 60 --groupby_fields region --log_every 1 --source_target_path PATH_TO_TARGET_DATA_FILE \
--eval_only True --evaluate_all_splits False --eval_splits iid_test
 
```
</ul>
</ul>

--------------------------------------------------------------------------------
<ul>

## Experiment 3: Multi-Source Domains with OOD Validation

</ul>

<ul>
<ul>

### Training and validating 
The following commend is used to train a model in Experiment 3:

```bash
# For ERM and GroupDRO
python ./examples/run_expt.py --dataset fmow --uniform_over_groups True --seed SEED --algorithm ALGORTIHM --root_dir wilds_fmow \
--log_dir LOG_DIRECTORY --n_epochs 50 --groupby_fields region --batch_size 64 --source_target_path PATH_TO_SOURCE_DATA_FILE \
--dataset_kwargs use_ood_val=True --evaluate_all_splits False

# For IRM and deepCORAL
python ./examples/run_expt.py --dataset fmow --n_groups_per_batch 4 --uniform_over_groups True --seed SEED --algorithm ALGORTIHM --root_dir wilds_fmow \
--log_dir LOG_DIRECTORY --n_epochs 50 --groupby_fields region --batch_size 64 --source_target_path PATH_TO_SOURCE_DATA_FILE \
--dataset_kwargs use_ood_val=True --evaluate_all_splits False
```
Where the <code>PATH_TO_SOURCE_DATA_FILE</code> is the path to the source domains directory. For example, if the target (left-out) domain is Africa and the OOD validation is Asia, the path is defined as:

```bash
... --source_target_path DSAC_Dataset/source_domains/Experiment_3_Dataset/exp_3_source_unseen_Africa_ood_val_Asia.csv ... 
```

### Evaluating and Testing
```bash
#For ERM and GroupDRO
python ./examples/run_expt.py --dataset fmow --algorithm ALGORTIHM --seed SEED --root_dir wilds_fmow \
--log_dir LOG_DIRECTORY  --batch_size 64 --groupby_fields region --log_every 1 --source_target_path PATH_TO_TARGET_DATA_FILE \
--eval_only True --evaluate_all_splits False --eval_splits iid_test

#For IRM and deepCORAL
python ./examples/run_expt.py --dataset fmow --algorithm ALGORTIHM --seed SEED --n_groups_per_batch 4 --uniform_over_groups True\
 --root_dir wilds_fmow --log_dir LOG_DIRECTORY  --batch_size 64 --groupby_fields region --log_every 1 --source_target_path PATH_TO_TARGET_DATA_FILE \
  --eval_only True --evaluate_all_splits False --eval_splits iid_test
```
</ul></ul>

<!---follow WILDS instruction on how to install the [WILDS](https://github.com/p-lambda/wilds) package along with fMoW dataset. --->

--------------------------------------------------------------------------------
