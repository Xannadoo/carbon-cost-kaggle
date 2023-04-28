# Dee and Sanna's Weekly Meeting Notes
* [1st May 2023](#1st-may-2023)
* [28th April 2023](#28th-april-2023)
* [20th April 2023](#20th-april-2023)
* [10th April 2023](#10th-april-2023)
* [4th April 2023](#4th-april-2023)
* [23th March 2023](#23rd-march-2023)
* [20th March 2023](#20th-march-2023)
* [2nd March 2023](#2nd-march-2023)
* [26th February 2023](#26th-february-2023)
* [23rd February 2023](#23rd-february-2023)
* [13th February 2023](#13th-february-2023)
* [Template](#day-month-year)

### 1st May 2023

#### Who did you help this week?
-

#### Who helped you this week?
-

#### What did you achieve?
* 

#### What did you struggle with?
* 

#### What would you like to work on next week?
* 

#### Where do you need help from Veronika?
* 

#### Any other topics
This space is yours to add to as needed.



### 28th April 2023

#### Who did you help this week?
- Sanna helped Dee remember that we don't have to re-run all the code, but we can comment out the files that ran (there are 7) for training and pretraining, and the job will finish in less time without requiring more than 3 days.

#### Who helped you this week?
- Joachim helped me figure out how to specify a desktop when submitting jobs.

#### What did you achieve?
* Made dataframes of all but 1 dataset (pcam-small)
* Ran training with CarbonTracker on all but 1 dataset with freeze=False for RevisitingTransfer (waiting on a few results to finish still)
* Rain training with freeze=True for RevisitingTransfer
* Have half of the results for pipeline1, both pretraining and training.

#### What did you struggle with?
* Package version issues on the HPC

#### What would you like to work on next week?
* Finish training on all datasets with freeze=True
* Enterpreting the results
* Writing

#### Where do you need help from Dovile?
* Is it expected that training only runs for 5-7/200 epochs? Seems to be correct. When freeze=false, the first chunk of epochs is training on the classification layer, and the second chunk is training the weights. 
* Verify that how we ran the training is correct
* Kimia dataset - she used it very little in the beginning. The pcam dataset is similar, but the kimia dataset is smaller. So she didn't run many experiments on it before dropping it completely. 
* Pcam data - we are skipping for now
* mamms data - we are skipping for now

#### Any other topics
-



### 20th April 2023

#### Who did you help this week?
* Sanna helped Dee try to debug an issue with making the dataframes on the mammograms dataset in Dovile's project.
* Lottie helped us debug issue in the CarbonTracker package.

#### Who helped you this week?
* Each other. We discussed how to handle data that is now coming in.

#### What did you achieve?
* For Dovile's project
	* We now have results for training on 3 out of 8 of the datasets. (isic, kimia, and breast)
	* Found that mammograms data has different structure on data_shares. Attempting to make dataframes work.
* We have results from pretraining in the Kaggle team's pipeline1.
* Fixed error in CarbonTracker
* Downloaded meta data from Kaggle and begun trying to work out what is useful (and what the various datasets actually include; there are no descriptions)

#### What did you struggle with?
* We still have error's making some of the dataframes for Dovile's project. We cannot train until the dataframes are made.

#### What would you like to work on next week?
* For kaggle project
	*  Run training job for pipeline1 to see carbon footprint
	*  Start looking into pipeline1
* Dovile's project:
	* Finish debugging for mammograms dataset and make dataframes
	* Make dataframes work for knee, chest, pcam-small, and thyroid

#### Where do you need help from Veronika?
* Requesting red queue for running the training for the kaggle team.

#### Any other topics




### 10th April 2023

#### Who did you help this week?
--

#### Who helped you this week?
--

#### What did you achieve?
* Continued working on the 2nd place team's code for the kaggle challenge
	* Solved package and installation issues.
	* Used the kaggle API to download a large dataset to the HPC
	* Finished Step 2, data preparation for pipeline1
	* Started Step 3, Training.

#### What did you struggle with?
* Package/installation issues on the kaggle project

#### What would you like to work on next week?
* Finish stage 3 Training for pipeline1 in the kaggle repo, shown [here](https://github.com/nvnnghia/siim2021/tree/main/pipeline1).
* Run training for Dovile's project

#### Where do you need help from Veronika?
* Help solving the Cuda/pytorch issues on HPC

#### Any other topics
--



### 4th April 2023

#### Who did you help this week?
- 

#### Who helped you this week?
- Spent 14+ hours trying to problem solve environment issues on the HPC. Lottie helped solving problems. Solution was using pip and not anaconda, with module load for sklearn and tensorflow.

#### What did you achieve?
* Got a working environment for Dovile's project.
* Re-ran the code for Dovile's project to make the dataframes.
* Restarted work on the 2nd place team for the [SIIM-FISABIO-RSNA COVID-19 Detection](https://www.kaggle.com/competitions/siim-covid19-detection/discussion/) kaggle challenge. Their github is located [here](https://github.com/nvnnghia/siim2021).
    - Created a branch of the repo. Cloned branch locally and on the HPC in the shared "ccdd" folder.
    - On the HPC, in pipeline1, completed part 1.Installation.
    - In pipeline1, for part 2.Data Preparation, downloaded the first dataset (resized SIIM2021) to the HPC

#### What did you struggle with?
* Getting working environments on the HPC. A workshop on setting up environments on HPC would have been amazing. Why does ITU not do this?

#### What would you like to work on next week?
* For the second place team, pipeline1, finishing step 2 Data Preparation, and start step 3 Training.

#### Where do you need help from Veronika?
- 

#### Any other topics
-



### 23rd March 2023

#### Who did you help this week?

Each other.

#### Who helped you this week?

* Dovile helped us find the mammograms data, which had been named "cbis-ddsm" on the HPC, not "mammograms" as it was in her code.
* Lottie explained how to make a shared environment, and how to make a batch file to create an environment and install packages

#### What did you achieve?

* Added carbon tracker to the yaml file, and created the environment.
* Changed home path to data folders in the ```make_dataframe.py``` file
* Changed name of the mammograms dataset folder to "cbis-ddsm" in the ```data_paths.py``` file
* Make a job file to create the dataframes. Attempted to run job. Getting error related to ```import cv2```
* Comment out ```import cv2```, as it doesn't seem needed to make the data splits. Getting error with tensorflow. running ```conda install -c conda-forge tensorflow``` in the environment. It has taken >1hour

#### What did you struggle with?

* Conda installing packages on the HPC is taking >1hour each. It is excrutiating. Lottie says HPC is just slow today.
* We do not have access to conda envs that the other creates. This is inconvenient. We are running a batch file to create a shared env
* Can't get the environment to work with sklearn.

#### What would you like to work on next week?

* We need to run the revi.job again and see if it gives the tensorflow related errors, or if it creates the dataframes
* Ideally we would make the data splits and train the model with carbontracker
* Work on getting 1 kaggle challenge participant's code to run

#### Where do you need help from Veronika?

* Understanding HPC. For example, loading multiple modules. Can we load an environment and load tensorflow as shown on the HPC.itu.dk site?

#### Any other topics

*



### 20th March 2023

#### Who did you help this week?

--

#### Who helped you this week?

* Dovile - talked us through her code from her [Revisiting Hidden Representations in Transfer Learning for Medical Imaging](https://github.com/DovileDo/revisiting-transfer) project

#### What did you achieve?

--

#### What did you struggle with?

* The real world. We already had delays due to my getting sick, then Dee had a family tragedy.
* Matching up datasets in the hpc. We haven't used the hpc much for a while and navigating can be interesting.

#### What would you like to work on next week?

* Actually getting some code to run properly.
	- if so, getting the carbontracker working.

#### Where do you need help from Veronika?

--

#### Any other topics

--


### 2nd March 2023

#### Who did you help this week?
--

#### Who helped you this week?
--

#### What did you achieve?

* Uploaded COVID competition data to HPC
* Began working through the instructions for running team 1's code (their [github](https://github.com/dungnb1333/SIIM-COVID19-Detection/tree/982a6b12955e8f53ec3f8af46754251b1678e08c)). Got through stage 2.1.

#### What did you struggle with?

* I tried running some teams' submission notebooks. While teams submit *just one notebook*, if often requires a larger repository to run. It doesn't seem sufficient to run their submission notebook alone.

#### What would you like to work on next week?

* Download the rest of the external data for team one.
* Finish working on getting their code running (with a small sample of data)

#### Where do you need help from Veronika?

* 

#### Any other topics
--


### 26th February 2023

#### Who did you help this week?

Each other

#### Who helped you this week?

Each other

#### What did you achieve?

* We learned that there are competitions on kaggle tagged as "code competitions". In these, the participants submit code, which kaggle will then run on their machines. We further noticed that code competitions tend to have a higher submission rate per team, with some teams up to 300 submissions, compared to competitions where a team submits an already trained model. It seems that this method of submission allows for a better tracking of the amount of times code is run, since the model-submission format does not indicate the amount of times a team trained a model for parameter tuning. Therefore, we believe we will get a more accurate result of the carbon footprint by looking into a code compeitions.
* Furthermore, code competitions are run by teams submitting code. Therefore the code is often publically available.
* The first competition we will be looking into is [SIIM-FISABIO-RSNA COVID-19 Detection](https://www.kaggle.com/competitions/siim-covid19-detection/)

#### What did you struggle with?

* We are moving on from the Data Science Bowl 2017 due to issues finding runable publically available code (much of the code we found used legacy languages and packages that are no longer supported), and issues finding a trustworthy source of data.

#### What would you like to work on next week?

* Working on a notebook to submit to the competition and run carbon-tracker on.

#### Where do you need help from Veronika?

* Finding value in what we have done (or not done) so far

#### Any other topics

--



### 23rd February 2023

#### Who did you help this week?

Sanna helped Dee find the kaggle datasets.

#### Who helped you this week?

See above. 

#### What did you achieve?

* Found the kaggle datasets (not so straightforward as expected)
	* https://academictorrents.com/details/015f31a94c600256868be155358dc114157507fc	
* Found supplementary data
	* [1st](https://github.com/lfz/DSB2017)
		* [Luna 16 Grand Challenge](https://luna16.grand-challenge.org/Download/)
	* [2nd](https://github.com/juliandewit/kaggle_ndsb2017)
		* None needed
	* [7th](https://github.com/NDKoehler/DataScienceBowl2017_7th_place)
		* [Luna 16 Grand Challenge](https://luna16.grand-challenge.org/Download/)
* We found competitions that are complete, have publically available code, and have publically available data:
	* [RSNA 2022 Cervical Spine Fracture Detection](https://www.kaggle.com/competitions/rsna-2022-cervical-spine-fracture-detection)
	* [RSNA Breast Cancer Detection](https://www.kaggle.com/competitions/rsna-breast-cancer-detection)
		* Might not have publically available code in time
		* Is it too similar to the Cervical Spine Competition (<9hr run time restriction on code?)
* We learned that the category "code competition" on kaggle means teams submit code vs a trained model. Therefore competitions with this tag are more likely to have publically available code. We are thinking to narrow our investigation to competitions with the tag **code competition**. Furthermore, these types of competitions have restrictions regarding resources and environments, as well as maximum runtime. This might reduce the amount of confounding factors as well as make it easier to extrapolate on our findings. 

#### What did you struggle with?

* Finding the data for the competition.

#### What would you like to work on next week?

* The following items are needed for each project to work:
	* [1st](https://github.com/lfz/DSB2017)
		* nothing is apparently missing
	* [2nd](https://github.com/juliandewit/kaggle_ndsb2017)
		* nothing is apparently missing
	* [7th](https://github.com/NDKoehler/DataScienceBowl2017_7th_place)
		* Checkpoint folder is required to run the project, but it has been removed from dropbox

* We are moving on from the lung cancer competition for now.
* Download data for cervical spine fracture detection
* Attempt running code for the cervical spine fracture detection competition

#### Where do you need help from Veronika?

* Guidance on problem solving finding the data/missing elements
* Is it safe to download the data to the HPC from the sources we found?
* Next week... can we meet Thursday since the PURRlab event is also Thursday, and we will be at ITU?


### 13th February 2023

#### Who did you help this week?

Each other.

#### Who helped you this week?

Google.

#### What did you achieve?

* Found 3 github repos for high ranking teams for the Kaggle lung cancer challenge:
	* 1st https://github.com/lfz/DSB2017
	* 2nd https://github.com/juliandewit/kaggle_ndsb2017
	* 7th https://github.com/NDKoehler/DataScienceBowl2017_7th_place

* Started working on how to actually run the first one.

#### What did you struggle with?

* Working out how to handle requirements for each repo, and looking at how to make the code run.

#### What would you like to work on next week?

* Continue with how to run the first project
* Test the requirements.txt file on Sanna's computer
* Finish setting up a requirements.txt file for HPC
* Start looking at the next submission where code is available

#### Where do you need help from Veronika?

* It seems some packages used are outdated. Is it ok if we use different versions of packages for the environment? 



### day month year Template

#### Who did you help this week?

Replace this text with a one/two sentence description of who you helped this week and how.

#### Who helped you this week?

Replace this text with a one/two sentence description of who helped you this week and how.

#### What did you achieve?

* Replace this text with a bullet point list of what you achieved this week.
* It's ok if your list is only one bullet point long!

#### What did you struggle with?

* Replace this text with a bullet point list of where you struggled this week.
* It's ok if your list is only one bullet point long!

#### What would you like to work on next week?

* Replace this text with a bullet point list of what you would like to work on next week.
* It's ok if your list is only one bullet point long!
* Try to estimate how long each task will take.

#### Where do you need help from Veronika?

* Replace this text with a bullet point list of what you need help from Veronika on.
* It's ok if your list is only one bullet point long!
* Try to estimate how long each task will take.

#### Any other topics

This space is yours to add to as needed.
