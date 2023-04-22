# Journal to track what we have been up to.
* [Training Status](#day-month-year)
* [2¨2 April 2023](#22-April-2023) 
* [21 April 2023](#21-April-2023) 
* [20 April 2023](#20-April-2023) 
* [19 April 2023](#19-April-2023)
* [18 April 2023](#18-April-2023)
* [17 April 2023](#17-April-2023)
* [16 April 2023](#16-April-2023)
* [14 April 2023](#14-April-2023)
* [13 April 2023](#13-April-2023)
* [10 April 2023](#10-April-2023)
* [9 April 2023](#9-April-2023)
* [7 April 2023](#7-April-2023)
* [6 April 2023](#6-April-2023)
* [1 April 2023](#1-April-2023)
* [23 March 2023](#23-march-2023)
* [18 March 2023](#18-march-2023)
* [16 March 2023](#16-march-2023)
* [March 2023](#march-2023)
* [February 2023](#february-2023)

### day month year Training Status
Carbon Footprint results located in [results.md](https://github.com/carbonCostKaggle/carbon-cost-kaggle/blob/main/results/results.md)
## Dovile's Project
| Dataset | Dataframe Status | Job | Training Status (Freeze=False) | Job | 
| ------- | ----------------- | --- | --------------- | --- |
| Isic | Done | deleted | Complete w/ correct image/batch size | `job.122952.out` |
| Breast | Done | deleted | Complete, correct image/batch size | `job.125144.out` |
| Chest | Done | `job.124916.out` | Complete w/ correct image/batch size | `job.125142.out` |
| Knee | Done | `job.124944.out` | Complete w/ correct image/batch size | `job.125145.out` |
| Mammograms | Done | `job.125408.out` | reran: bug:`ValueError`, rerunning | `job.125135.out` `job.125368.out`|
| Thyroid | Done (locally) | no job file | submitted | `job.125550.out` |
| Kimia | Done | deleted | Complete (check image/batch size) | `job.123577.out`
| Pcam-small | bug:`ValueError: No objects to concatenate`. folder in HPC seems empty | `job.123806.out` | - | - |

## Kaggle Project
| Stage | Runs | Job | Splits | Job | W/ CarbonTracker | Job | Status | 
| ----- | ---- | --- | ------ | --- | ---------------- | --- | ------ |
| P1:pretrain | yes | `pt_wo_ct.out` | 7 files, 5 folds, 15 epochs | `job.124727.out` | runs desktop 18, not 9 | `job.123687.out` `job.125114.out` `job.125319.out`| done:3day limit, didn't print results, need to rerun. short test with commented out training. re-running w/o comments |
| P1:train | yes, hit timelimit | `job.122954.out` | 7 files, 5 folds, 15 epochs | `job.124717.out` | short test | `job.124726.out`,`job.125115.out` | failed, env or hardware issue?, need to wait for pretraining? |
| P2:.. | not started | - | - | - | - | - | - |

### 22 April 2023
- **Kaggle Project**
    - Pretraining fails on Desktop 9, and runs on Desktop 18. Need to figure out how to exclude a particular desktop, or range of desktops.
    - Resubmitted for desktop 18 (`job.125448.out`)
- **Dovile's Project**
    - Re-ran making dataframes for mamms with new file location, with all images in one location (`job.125408.out`). Seems ok. Reran training (`job.125419.out`) and failed again. There was a missing "/" for making the dataframes. Fixed this error, re-made dataframes, and submitted the training job.
    - Made dataframes for the thyroid dataset locally by downloaded the images from the HPC. Submitted a job for training (`job.125550.out`)
- **Meta Kaggle**
    - Isolated code competitions tagged with 'image'. Older code competitions refer to the notebooks as 'kernels', they are the same thing. Kaggle's description of the different [competitions](https://www.kaggle.com/docs/competitions) links to [one](https://www.kaggle.com/c/quora-insincere-questions-classification) described as a kernel competition as an example of a code competition. Need to decide what we want from this. Have average submisions per team, and average number of teams per competition, but is this enough? Avg submissions ~18, but thee range within this is huge, with some in their hundreds and others hardly any - maybe they entered but didn't actually get very far, so maybe we need to account for this somehow? Some competitions get a lot more entrants than others (maybe those with bigger prizes?).

### 21 April 2023
- Worked on creating the mammograms database csv, from a folder with symlinks to all the images. (`job.125320.out`) Now we need to see if it can actually train this way.
- Training failed. Upon inspection of file paths, it seems to be off. Modified path and sent file to re-make dataframes (`job.125135.out`). Training after this failed to find images. Moved all images into a shared folder, and am re-running pips.job to make mamms dataframes.
- Found a better meta-dataset to work with to find the data we need to estimate number of submissions per competitions. Filtered for competitions tagged as 'image' as the siim set has this tag, along with some of the others we considered. Trying to find some way of distinguishing code competitions from traditional ones, but this is not so obvious. It may be that they are 'kernal only submissions'. These competitions appeared around 2019, which seems to coincide with code competitions but this needs to be verified.
- pretraining job submitted, with break statement put in after 1 epoch runs (`job.125319.out`)

### 20 April 2023
- **For Dovile's Project**
    - Sanna will try to simlink the folders for the mammagrams dataset (cbis-ddsm). The path on `data_import.py` line `403` will need to be changed to our simlinked folder
    - Debugged errors with making chest and knee dataframes. Unable to run training due to lack of permissions to submit jobs on the HPC.
    - Chest dataframe file failed `job.124930.out` because of a hardware issue. The job happened to get the wrong Desktop, it seems.
- **Kaggle Project**
    - figured out that both pretraining and training run 7 times, with 5 folds within each, and 15 epochs within each fold. Setting up CT to track a fold, run all epochs, and break after 1 fold to predict how many it would be with 5 folds.
    - pretraining was commented out to make sure CT was in the correct place, and the break works. pretrain.job is ready to run (I do not currently have permissions for some unknown reason
    - training was set up with CT and break to stop after 1 fold runs. train.job is ready to run a short version to test first.

### 19 April 2023
- 3 hrs trying to join tables to isolate image competition submissions. I think we have about got there. Working out which tables we need to join was the biggest challenge due to the not-particularly clear column-names.

### 18 April 2023
- Got help from Joachim at HPC to debug pandas error in the mammograms dataset. The solution did not work. Spent 3 hours throughout the day trying to debug the issue with no success. Issue seems to be with a not-updated veresion of anaconda Tried:
    - upgrading pandas with pip
    - installing pandas with pip and conda
    - modifying order of loaded modules, pip installing requirements, etc
    - updating anaconda (I don't have write permissions)

### 17 April 2023
- **For Dovile's Project**:
    - Results (`job.122952.out`) of running training on the **isic** data:
    Only Ran training once.
    - Results for the **kimia** dataset (`job.123577.out`)
    - Need to get chest, knee, mammograms, pcam-small, chest, and thyroid datasplits working
    - Attempting to debug with 1 dataset at a time.
    - Ran pips.job for **mammmograms** data (`job.123742.out` and `job.123802.out`). Dataframes are not changed... the data on purrlab seems to be structured differently.
    - Fixed path on `data_imports.py` for mammograms data. Ran pips.job again (`job.123802.out`).
    - Ran train.job for **mammograms** data (`job.123808.out`). Error `ValueError: Asked to retrieve element 0, but the Sequence has length 0`
    - Ran pips.job for **thyroid** data (`job.123703.out`). Error `AttributeError: module 'pandas' has no attribute 'read_xml'`. Wth? Need to get help from HPC about this Tuesday (tomorrow) between 9-11.
    - Ran pips.job for **chest** data (`job.123721.out`). Error `ValueError: 7 is not in range`
    - Ran pips.job for **knee** data (`job.123744.out`). Error `ValueError: 7 is not in range`
    - Ran pips.job for **pcam-small** (`job.123749.out`). Typo in job file. Rerunning (`job.123806.out`). Error `ValueError: No objects to concatenate`
 - **For Kaggle project**:
    - Re-ran pretraining with correct number of epochs (4 folds, 15 epochs each). Gave limit of 3 days, but requested more from HPC. 
    - Need to get these results. (`job.123687.out`)
    - Training ran successfully, just ran out of time. (`job.122954.out`)
    - Ran training with actual training commented out to see number of epochs (`job.123717.out`)
    - Added CarbonTracker to training script. Need to re-run with correct epochs, more time, and comments removed.

### 16 April 2023
- For Dovile's Project:
    - The job submitted for the **breast** dataset showed a typo in the fix in the CarbonTracker code. It has now been fixed and re-run. 
    - The results prior to re-running (`job.122945.out`) are as follows:
    - ```
        CarbonTracker:
        Actual consumption for 1 epoch(s):
                Time:   0:14:58
                Energy: 0.051023 kWh
                CO2eq:  5.204317 g
                This is equivalent to:
                0.048412 km travelled by car
        CarbonTracker:
        Predicted consumption for 200 epoch(s):
                Time:   49:53:53
                Energy: 10.204543 kWh
                CO2eq:  1051.017129 g
                This is equivalent to:
                9.776904 km travelled by car
        CarbonTracker: Finished monitoring.
        ```
    - Need to check results after re-running (`job.122952.out`)
- For the Kaggle Project:
    - Time limit hit and pretraining did not finish. The results of this (in file `job.122234.out`) are as follows:
    ```
    Actual consumption for 1 epoch(s):
        Time:   19:01:56
        Energy: 12.282045 kWh
        CO2eq:  1049.397093 g
        This is equivalent to:
        9.761833 km travelled by car
    CarbonTracker:
    Predicted consumption for 5 epoch(s):
            Time:   95:09:41
            Energy: 61.410227 kWh
            CO2eq:  8532.031854 g
            This is equivalent to:
            79.367738 km travelled by car
    CarbonTracker: Finished monitoring.
    ```
    - Re-submitted a job with training commented out to verify the number of epochs. I think it is actually 15 epochs, but 5 folds. Only just under 2 folds finished within 36 hours.
    - Need to re-run pretraining with correct number of epochs.

### 14 April 2023
- For Dovile's Project:
    - Started a job file for training on the breast dataset. Seems to be working.
    - Started jobs for the isic and kimia datasets. Both failed. Seems like it could be due to a resource issue, but I'm not sure.
- For the Kaggle Project:
    - Modified the pretraining job file to have the correct number of epochs and a long enough running time. Changed nothing else, but started running into the following error again: ``AttributeError: 'str' object has no attribute 'decode'```. 
    - Apptempted to solve this for about an hour by selecting specific GPU's. Then went to DASYA lab. Lottie helped debug the issue. We tried specifying specific Desktops to see which one would work. After that we went to the GitHub for CarbonTracker and found 2 related issues. 
    - For the above attribute error we had to go ``` "/home/ddeq/.local/lib/python3.8/site-packages/carbontracker/components/gpu/nvidia.py"``` and comment out line 25 where it says ```devices = [name.decode("utf-8") for name in names]```, then add ```devices = names``` on a line before the return statement. Lottie suggests that their package might not robust to handle different setups, which causes this issue.
    - We also went to ```carbontracker/emissions/intensity/fetchers/energidataservice.py``` and added ```from_str = from_str.replace(' ','T')``` below line 44 and ```to_str = to_str.replace(' ','T')``` below that. 
    - On a side note, even though I am using an anaconda environment, the error seemed to come from the pip installed version. Lottie did not understand why the anaconda version of CarbonTracker was not being used, if it was in the environment.
    - job file is set up to run for whenever the pretrain job is finished.
- Total time spent today: 5 hours 

- Downloadeded all the [kaggle metadata](https://www.kaggle.com/datasets/kaggle/meta-kaggle?select=KernelVersionCompetitionSources.csv). There is a lot of tables, so started working out which were hopefully useful. We want to know how many competitions(ideally the code competitions, but this might not be easy to isolate), how many entrants for each, and ideally, how many times they submitted. There isn't any description of the tables, that I can find, so it's a case of looking at them and working out what the hell they have recorded.

### 13 April 2023
- For Dovile's project:
    - the job for ```make_dataframe.py``` only seems to have worked for the breast, ISIC, and kimia datasets.
    - We get errors for making the dataframes for the chest, knee, mammograms, pcam-small, and thyroid datasets.
    - Made Job file for training
    - Ran training successfully on Imagenet for the breast dataset with 2 cpu cores only. Took 23 minutes
    - Added carbon tracker and re-ran training on breast dataset. Failed: ```OUT_OF_MEMORY```
    - Changed to 8 CPU cores and GPU. Failed ```AttributeError: 'str' object has no attribute 'decode'``` Traceback ended here... ``` "/home/ddeq/.local/lib/python3.8/site-packages/carbontracker/components/gpu/nvidia.py"```. So removing GPU from the train.job file.
    - Job completed successfully. Now we need to figure out if we used carbon tracker correctly.
    - ```
        CarbonTracker:
            Actual consumption for 1 epoch(s):
            Time:   0:08:15
            Energy: 0.010210 kWh
            CO2eq:  0.418615 g
            This is equivalent to:
            0.003894 km travelled by car
            ```
- For the kaggle project:
    - Messed with cpu/gpu settings on the HPC until the pretrain job started working. 1st epoch done 79% before leaving ITU. Assume it will finish.
    - Modified pretraining.py to include carbon tracker.
    - Made a job file for running training
- Total time spent on this part today: 10:30am-4:00pm (5.5 hours)

### 10 April 2023
- Spent 1 more hour and fixed missing package errors for the kaggle repo. Had to re-run pip with the requirements.txt file, which was already did in the installation step for pipeline1, and additionally run some pip installs. So even though the steps were outlined "clearly" in their Readme, the installation instructions were not sufficient to get the project running.
- Now getting errors related to Cuda and pytorch

### 9 April 2023
- Created a job file to run ```python create_folds.py``` for the siim kaggle challenge. Even after following the installation instructions, having errors with "No module named": 'cv2', 'neptune', 'torch', 'albumentations', 'torchvision'... and others
    - Started at 11:00 am. Ended at 1:30 pm. So 2.5 hours spent, and still having missing package errors.

### 7 April 2023
-  Used the kaggle API on HPC to download the final dataset directly. It took about 5 mins to download, once everything was set up correctly (I didn't time that bit :'( as I was working with many distractions.). Unzipping it took longer, but I was baking brownies simultaneously.
-  Ran a job on the HPC for ```python create_folds.py``` to create the data splits. Stage 2: Data Preparation in pipeline1 is officially finished.

### 6 April 2023
- The 2nd place team requires 2 datasets for training in pipeline1 for part 2.Data Preparation. Downloaded the first dataset (resized SIIM2021) to the HPC
    - Took about 1.5 hours to download and extract
- Downloaded the second dataset. Tried to upload to HPC but the estimated time was ~35 hours. It might be faster if we can download it directly. Is this possible?
    - Tried curl and wget locally, but it doesn't download the dataset. Is there another way?
- Timelines aligned so we actually got to talk about the project from opposite sides of the world! Woohoo!

### 1 April 2023
- Attempted to solve path issues on HPC with conda. Updated conda. Used module load for sklearn, then got tensorflow issues. Used module load for tensorflow, and found out that it does not coordinate well with other packages if there is a discrepency in package versions. After many emails back-and-forth between HPC, we realize that a workshop on how to properly use HPC and setup environments would have saved us now 14+ hours of our lives.
- Abandoned anaconda, and am using pip for environments. Created a requirements.txt and a new job file to create the env and run the first job, which is just to make the dataframes.
- Restarting work on the 2nd place team for the [SIIM-FISABIO-RSNA COVID-19 Detection](https://www.kaggle.com/competitions/siim-covid19-detection/discussion/) kaggle challenge. Their github is located [here](https://github.com/nvnnghia/siim2021).
    - Created a branch of the repo. Cloned branch locally and on the HPC in the shared "ccdd" folder.
    - On the HPC, in pipeline1, completed part 1.Installation. (Sanna will have to complete this separately, as there is no shared environment)
    - Next steps for pipeline1 are part 2:Data Preparation, and part 3:Training 


### 23 March 2023
- Added carbon tracker to the yaml file, and created the environment.
- Changed home path to data folders in the ```make_dataframe.py``` file
- Changed name of the mammograms dataset folder to "cbis-ddsm" in the ```data_paths.py``` file
- Make a job file to create the dataframes. Attempted to run job. Getting error related to ```import cv2```
- Comment out previous import, and getting error with tensorflow. running ```conda install -c conda-forge tensorflow``` in the environment. 
- We do not have access to environments that the other creates. Asked Lottie if we can share access to envs. 
- Next, need to run the job again and see if it gives the tensorflow related errors.



### 18 March 2023
- Spent ~3 hours working out how to run the yaml file to create an environment for the revisiting-transfer project. Found the bugs, pushed changes to github, and created an environment on HPC. There was one package, ```tensorflow-gpu==2.8.0``` that would only work if pip installed, and not as a dependency as it was in the original yaml file.

### 16 March 2023
 - Discussed accessing stuff on hpc as can't see what the other has done there. Is a shared folder possible?
 - Forked Dovile's repo to the project.
     + We spoke with her last Thursday and talked through the code, and she suggested some things we probably want to remove (like the mlflow tracking parts) and where might work to insert the code for the carbontracker.
     + Is all the data on HPC? (mammagrams, imagenet)
     + Started working on reproducing it on the hpc.
     + Got stuck with creating the conda env as it got upset about a conflict. Removed mlflow & boto from the .yaml as we aren't using that part of the code and the conflict seemed to be with one of them.

### March 2023
 - Downloaded covid data and uploaded to the hpc. Took ~5 hours.
 - Started looking at running the first place (private leaderboard), tried to run with a subset (10 samples) to verify code worked. 
 - Phase 1 worked.
 - Phase 2 required external datasets, some of which were no longer available. The first link in particular was to another kaggle user who had uploaded data, that looked like it was designed for this particular competition although this isn't verified as it's gone.
 - Looked at the second place version. Like the first place team, they had also done significant work offline. Their first pipeline looks workable. Their second pipeline required several github branches to be used, to which the links are broken. We need to look at this further.
 - Considering running Dovile's project and using the carbon-costs associated with that as a proxy.
 - Sorted the issue with the second pipeline, for the covid-19 challenge.
 

### February 2023
- looked at kaggle lung cancer challenge [Data Science Bowl 2017](https://www.kaggle.com/competitions/data-science-bowl-2017) private participants. Found 3 in the top ten where public githubs were available, many participants did not make their code available even if they described their process in text. 
- Spent many hours trying to work out how to reproduce their results, even with the code avaliable. Problems included:
    - Some didn't link their public github to their kaggle entry, although we could find them by google
    - Lack of requirements, non-standard formats for requirements
    - Missing data, as this challenge is no longer hosting the data due to usage restrictions
    - Missing/no longer available external data
- Eventually decided the lack of availablity of the original dataset was too great, so decided to look for other challenges.
    - Another day spent looking at various other challenges, with available code and data.
    - One competition, [Cancer detection](https://www.kaggle.com/competitions/rsna-breast-cancer-detection) is finishing soon, it's unclear how soon code will be released so maybe this won't work for our timeline.
    - Kaggle runs different kinds of challenges, we decided to focus on code challenges as more likely that code is available. Kaggle also logs how often the notebooks are run, in theory this gives us something to work on with calculating carbon costs. 
    - We also noticed that approx 8/10 of the most recent, completed challenges are code competitions.
    - Considering the [Covid challenge](https://www.kaggle.com/competitions/siim-covid19-detection/overview) from 2021. This is relativly recent so hopefully up-to-date.
  
