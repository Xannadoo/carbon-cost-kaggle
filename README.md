# Carbon Footprint of Machine Learning Competitions With Medical Images
Investigating the carbon cost of kaggle competitions

This project contains the data produced in our investigation of the carbon footprint of ML competitions, and our subsequent analysis.
For further information on our motivations behind this research, and our analysis, please check out the final report [here](https://github.com/carbonCostKaggle/carbon-cost-kaggle/blob/main/report/final_report.pdf).

# Repo Structure
[img](https://github.com/carbonCostKaggle/carbon-cost-kaggle/tree/main/img): Images from analysis, some of which are used in the report.<br>
[meta_data/meta](https://github.com/carbonCostKaggle/carbon-cost-kaggle/tree/main/meta_data/meta): Contains all of the metadata files from Kaggle used in our analysis. <br>
[Report](https://github.com/carbonCostKaggle/carbon-cost-kaggle/tree/main/report): Contains the final report.<br>
[Results](https://github.com/carbonCostKaggle/carbon-cost-kaggle/tree/main/results): Contains the final results from the carbon footprint analysis of the models. The markdown files are raw, unformatted output from CarbonTracker, including data on the job out file so we could internally locate the original source on the HPC, as well as the stage of training being analyzed and hardware used. The csv files are the more tidy version of the markdown files, for use in the notebooks.

# How to Install and Run this Project

```
pip install requirements.txt
```

# Acknowledgements
