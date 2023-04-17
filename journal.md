# Journal to track what we have been up to.
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


### 17 April 2023
- For Dovile's Project:
    - Results (in `job.122952.out`) of running training on the isic data:
    Only Ran training once.
    ```
    CarbonTracker:
    Actual consumption for 1 epoch(s):
            Time:   1:37:40
            Energy: 0.338987 kWh
            CO2eq:  32.058499 g
            This is equivalent to:
            0.298219 km travelled by car
    CarbonTracker:
    Predicted consumption for 200 epoch(s):
            Time:   325:31:49
            Energy: 67.797429 kWh
            CO2eq:  5665.096228 g
            This is equivalent to:
            52.698570 km travelled by car
    CarbonTracker: Finished monitoring.
    ```      
    - Results for the kimia dataset (in `job.123577.out`)
    ```
    CarbonTracker:
    Actual consumption for 1 epoch(s):
            Time:   0:08:34
            Energy: 0.007341 kWh
            CO2eq:  0.521238 g
            This is equivalent to:
            0.004849 km travelled by car
    CarbonTracker:
    Predicted consumption for 200 epoch(s):
            Time:   28:32:35
            Energy: 1.468276 kWh
            CO2eq:  101.336366 g
            This is equivalent to:
            0.942664 km travelled by car
    CarbonTracker: Finished monitoring.
    ```
    - Need to get chest, knee, mammograms, pcam-small, and thyroid datasplits working
    - Ran pips.job for thyroid data. Attempting to debug with 1 dataset at a time. Job failed (`job.123703.out`) due to `AttributeError: module 'pandas' has no attribute 'read_xml'`. Wth? Need to get help from HPC about this Tuesday (tomorrow) between 9-11.
    - Submitted pips.job for making chest dataframe (123721).
 - For Kaggle project:
    - Re-ran pretraining with correct number of epochs (4 folds, 15 epochs each). Gave limit of 3 days, but requested more from HPC. 
    - Need to get these results. (in `job.123717.out`?)
    - Training ran successfully, just ran out of time. (in `job.122954.out`)
    - Ran training with actual training commented out to see number of epochs (in `job.123717.out`)
    - Added CarbonTracker to training script. Need to re-run with correct epochs, more time, and comments removed.

### 16 April 2023
- For Dovile's Project:
    - The job submitted for the breast datset showed a typo in the fix in the CarbonTracker code. It has now been fixed and re-run. 
    - The results prior to re-running (in `job.122945.out`) are as follows:
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
  
