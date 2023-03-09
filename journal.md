# Feb 2023 
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
  
 # March 2023
 - Downloaded covid data and uploaded to the hpc. Took ~5 hours.
 - Started looking at running the first place (private leaderboard), tried to run with a subset (10 samples) to verify code worked. 
 - Phase 1 worked.
 - Phase 2 required external datasets, some of which were no longer available. The first link in particular was to another kaggle user who had uploaded data, that looked like it was designed for this particular competition although this isn't verified as it's gone.
 - Looked at the second place version. Like the first place team, they had also done significant work offline. Their first pipeline looks workable. Their seond pipeline required several github branches to be used, to which the links are broken. We need to look at this further.
 - Considering running Dovile's project and using the carbon-costs associated with that as a proxy.

