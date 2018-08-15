# Loss aversion study as pyMVPA analysis
2016.04 ~ 2016.06

## Introduction
- I perfomed searchlight analysis on rapid ER design fMRI images.
- They aren't neat codes, but I uploaded them for a backup purpose.
- I had many other analyses... but I don't know which codes should be need to perform searchlight analysis. So, I roughly choose some codes 😅

## Data structure example
### Open FMRI Dataset
For using `OpenFMRIDataset` function, all files were organized like these:

```
brain@neurodebian:~/Desktop/data/LAstudy2$ ls
code           sub001  sub005  sub009  sub013  sub018  task_key.txt
model_key.txt  sub002  sub006  sub010  sub014  sub019
models         sub003  sub007  sub011  sub015  sub022
scan_key.txt   sub004  sub008  sub012  sub016  sub023

brain@neurodebian:~/Desktop/data/LAstudy2$ cat model_key.txt
model001 accept_v_reject

brain@neurodebian:~/Desktop/data/LAstudy2$ cat scan_key.txt
TR 2

brain@neurodebian:~/Desktop/data/LAstudy2$ cat task_key.txt
task001 mixed gamble task

brain@neurodebian:~/Desktop/data/LAstudy2$ ls sub001/*/*/*
sub001/BOLD/task001_run001/bold_events.tsv
sub001/BOLD/task001_run001/bold_filtered.nii.gz
sub001/BOLD/task001_run001/bold_moest.txt
sub001/BOLD/task001_run001/bold.nii.gz
sub001/BOLD/task001_run002/bold_events.tsv
sub001/BOLD/task001_run002/bold_filtered.nii.gz
sub001/BOLD/task001_run002/bold_moest.txt
sub001/BOLD/task001_run002/bold.nii.gz
sub001/BOLD/task001_run002/bold_reg.mat
sub001/BOLD/task001_run003/bold_events.tsv
sub001/BOLD/task001_run003/bold_filtered.nii.gz
sub001/BOLD/task001_run003/bold_moest.txt
sub001/BOLD/task001_run003/bold.nii.gz
sub001/BOLD/task001_run003/bold_reg.mat
sub001/mask/run01/mask.nii.gz
sub001/mask/run02/mask.nii.gz
sub001/mask/run03/mask.nii.gz

sub001/BOLD/task001_run001/bold.feat:
absbrainthresh.txt  design.ppm                 report.html
design.con          design.trg                 report_log.html
design_cov.png      example_func.nii.gz        report_poststats.html
design_cov.ppm      filtered_func_data.nii.gz  report_prestats.html
design.frf          logs                       report_reg.html
design.fsf          mask.nii.gz                report_stats.html
design.mat          mc                         report_unwarp.html
design.min          mean_func.nii.gz
design.png          reg

sub001/BOLD/task001_run002/bold.feat:
absbrainthresh.txt  design.ppm                 report.html
design.con          design.trg                 report_log.html
design_cov.png      example_func.nii.gz        report_poststats.html
design_cov.ppm      filtered_func_data.nii.gz  report_prestats.html
design.frf          logs                       report_reg.html
design.fsf          mask.nii.gz                report_stats.html
design.mat          mc                         report_unwarp.html
design.min          mean_func.nii.gz
design.png          reg

sub001/BOLD/task001_run003/bold.feat:
absbrainthresh.txt  design.ppm                 report.html
design.con          design.trg                 report_log.html
design_cov.png      example_func.nii.gz        report_poststats.html
design_cov.ppm      filtered_func_data.nii.gz  report_prestats.html
design.frf          logs                       report_reg.html
design.fsf          mask.nii.gz                report_stats.html
design.mat          mc                         report_unwarp.html
design.min          mean_func.nii.gz
design.png          reg

sub001/model/model001/onsets:
task001_run001  task001_run002  task001_run003
brain@neurodebian:~/Desktop/data/LAstudy2$ ls sub001/*/*/*/*
sub001/BOLD/task001_run001/bold.feat/absbrainthresh.txt
sub001/BOLD/task001_run001/bold.feat/design.con
sub001/BOLD/task001_run001/bold.feat/design_cov.png
sub001/BOLD/task001_run001/bold.feat/design_cov.ppm
sub001/BOLD/task001_run001/bold.feat/design.frf
sub001/BOLD/task001_run001/bold.feat/design.fsf
sub001/BOLD/task001_run001/bold.feat/design.mat
sub001/BOLD/task001_run001/bold.feat/design.min
sub001/BOLD/task001_run001/bold.feat/design.png
sub001/BOLD/task001_run001/bold.feat/design.ppm
sub001/BOLD/task001_run001/bold.feat/design.trg
sub001/BOLD/task001_run001/bold.feat/example_func.nii.gz
sub001/BOLD/task001_run001/bold.feat/filtered_func_data.nii.gz
sub001/BOLD/task001_run001/bold.feat/mask.nii.gz
sub001/BOLD/task001_run001/bold.feat/mean_func.nii.gz
sub001/BOLD/task001_run001/bold.feat/report.html
sub001/BOLD/task001_run001/bold.feat/report_log.html
sub001/BOLD/task001_run001/bold.feat/report_poststats.html
sub001/BOLD/task001_run001/bold.feat/report_prestats.html
sub001/BOLD/task001_run001/bold.feat/report_reg.html
sub001/BOLD/task001_run001/bold.feat/report_stats.html
sub001/BOLD/task001_run001/bold.feat/report_unwarp.html
sub001/BOLD/task001_run002/bold.feat/absbrainthresh.txt
sub001/BOLD/task001_run002/bold.feat/design.con
sub001/BOLD/task001_run002/bold.feat/design_cov.png
sub001/BOLD/task001_run002/bold.feat/design_cov.ppm
sub001/BOLD/task001_run002/bold.feat/design.frf
sub001/BOLD/task001_run002/bold.feat/design.fsf
sub001/BOLD/task001_run002/bold.feat/design.mat
sub001/BOLD/task001_run002/bold.feat/design.min
sub001/BOLD/task001_run002/bold.feat/design.png
sub001/BOLD/task001_run002/bold.feat/design.ppm
sub001/BOLD/task001_run002/bold.feat/design.trg
sub001/BOLD/task001_run002/bold.feat/example_func.nii.gz
sub001/BOLD/task001_run002/bold.feat/filtered_func_data.nii.gz
sub001/BOLD/task001_run002/bold.feat/mask.nii.gz
sub001/BOLD/task001_run002/bold.feat/mean_func.nii.gz
sub001/BOLD/task001_run002/bold.feat/report.html
sub001/BOLD/task001_run002/bold.feat/report_log.html
sub001/BOLD/task001_run002/bold.feat/report_poststats.html
sub001/BOLD/task001_run002/bold.feat/report_prestats.html
sub001/BOLD/task001_run002/bold.feat/report_reg.html
sub001/BOLD/task001_run002/bold.feat/report_stats.html
sub001/BOLD/task001_run002/bold.feat/report_unwarp.html
sub001/BOLD/task001_run003/bold.feat/absbrainthresh.txt
sub001/BOLD/task001_run003/bold.feat/design.con
sub001/BOLD/task001_run003/bold.feat/design_cov.png
sub001/BOLD/task001_run003/bold.feat/design_cov.ppm
sub001/BOLD/task001_run003/bold.feat/design.frf
sub001/BOLD/task001_run003/bold.feat/design.fsf
sub001/BOLD/task001_run003/bold.feat/design.mat
sub001/BOLD/task001_run003/bold.feat/design.min
sub001/BOLD/task001_run003/bold.feat/design.png
sub001/BOLD/task001_run003/bold.feat/design.ppm
sub001/BOLD/task001_run003/bold.feat/design.trg
sub001/BOLD/task001_run003/bold.feat/example_func.nii.gz
sub001/BOLD/task001_run003/bold.feat/filtered_func_data.nii.gz
sub001/BOLD/task001_run003/bold.feat/mask.nii.gz
sub001/BOLD/task001_run003/bold.feat/mean_func.nii.gz
sub001/BOLD/task001_run003/bold.feat/report.html
sub001/BOLD/task001_run003/bold.feat/report_log.html
sub001/BOLD/task001_run003/bold.feat/report_poststats.html
sub001/BOLD/task001_run003/bold.feat/report_prestats.html
sub001/BOLD/task001_run003/bold.feat/report_reg.html
sub001/BOLD/task001_run003/bold.feat/report_stats.html
sub001/BOLD/task001_run003/bold.feat/report_unwarp.html

sub001/BOLD/task001_run001/bold.feat/logs:
feat0             feat1        feat2_pre.e8614    feat5_stop.o12859
feat0_init.e8463  feat1a_init  feat2_pre.o8614    feat9
feat0_init.o8463  feat2_pre    feat5_stop.e12859

sub001/BOLD/task001_run001/bold.feat/mc:
disp.png                                prefiltered_func_data_mcf_rel_mean.rms
prefiltered_func_data_mcf_abs_mean.rms  prefiltered_func_data_mcf_rel.rms
prefiltered_func_data_mcf_abs.rms       rot.png
prefiltered_func_data_mcf.mat           trans.png
prefiltered_func_data_mcf.par

sub001/BOLD/task001_run001/bold.feat/reg:
example_func2highres_fast_wmedge.nii.gz  example_func.nii.gz
example_func2highres_fast_wmseg.nii.gz   highres2example_func.mat
example_func2highres_init.mat            highres2standard.mat
example_func2highres.mat                 highres2standard.nii.gz
example_func2highres.nii.gz              highres2standard.png
example_func2highres.png                 highres_head.nii.gz
example_func2standard1.png               highres.nii.gz
example_func2standard.mat                standard2example_func.mat
example_func2standard.nii.gz             standard2highres.mat
example_func2standard.png                standard.nii.gz

sub001/BOLD/task001_run002/bold.feat/logs:
feat0              feat1        feat2_pre.e27883  feat5_stop.o3814
feat0_init.e27734  feat1a_init  feat2_pre.o27883  feat9
feat0_init.o27734  feat2_pre    feat5_stop.e3814

sub001/BOLD/task001_run002/bold.feat/mc:
disp.png                                prefiltered_func_data_mcf_rel_mean.rms
prefiltered_func_data_mcf_abs_mean.rms  prefiltered_func_data_mcf_rel.rms
prefiltered_func_data_mcf_abs.rms       rot.png
prefiltered_func_data_mcf.mat           trans.png
prefiltered_func_data_mcf.par

sub001/BOLD/task001_run002/bold.feat/reg:
example_func2highres_fast_wmedge.nii.gz  example_func.nii.gz
example_func2highres_fast_wmseg.nii.gz   highres2example_func.mat
example_func2highres_init.mat            highres2standard.mat
example_func2highres.mat                 highres2standard.nii.gz
example_func2highres.nii.gz              highres2standard.png
example_func2highres.png                 highres_head.nii.gz
example_func2standard1.png               highres.nii.gz
example_func2standard.mat                standard2example_func.mat
example_func2standard.nii.gz             standard2highres.mat
example_func2standard.png                standard.nii.gz

sub001/BOLD/task001_run003/bold.feat/logs:
feat0             feat1        feat2_pre.e4350    feat5_stop.o13400
feat0_init.e4193  feat1a_init  feat2_pre.o4350    feat9
feat0_init.o4193  feat2_pre    feat5_stop.e13400

sub001/BOLD/task001_run003/bold.feat/mc:
disp.png                                prefiltered_func_data_mcf_rel_mean.rms
prefiltered_func_data_mcf_abs_mean.rms  prefiltered_func_data_mcf_rel.rms
prefiltered_func_data_mcf_abs.rms       rot.png
prefiltered_func_data_mcf.mat           trans.png
prefiltered_func_data_mcf.par

sub001/BOLD/task001_run003/bold.feat/reg:
example_func2highres_fast_wmedge.nii.gz  example_func.nii.gz
example_func2highres_fast_wmseg.nii.gz   highres2example_func.mat
example_func2highres_init.mat            highres2standard.mat
example_func2highres.mat                 highres2standard.nii.gz
example_func2highres.nii.gz              highres2standard.png
example_func2highres.png                 highres_head.nii.gz
example_func2standard1.png               highres.nii.gz
example_func2standard.mat                standard2example_func.mat
example_func2standard.nii.gz             standard2highres.mat
example_func2standard.png                standard.nii.gz

sub001/model/model001/onsets/task001_run001:
cond001.txt  cond002.txt

sub001/model/model001/onsets/task001_run002:
cond001.txt  cond002.txt

sub001/model/model001/onsets/task001_run003:
cond001.txt  cond002.txt
```

### Searchlight
For performing searchlight analysis, I organized files like these:

```
brain@neurodebian:~/Desktop/data/20160601/bs_add6$ ls
sub001.hdf5  sub005.hdf5  sub009.hdf5  sub013.hdf5  sub018.hdf5
sub002.hdf5  sub006.hdf5  sub010.hdf5  sub014.hdf5  sub019.hdf5
sub003.hdf5  sub007.hdf5  sub011.hdf5  sub015.hdf5  sub022.hdf5
sub004.hdf5  sub008.hdf5  sub012.hdf5  sub016.hdf5  sub023.hdf5
```

