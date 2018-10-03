# DSX Local Workshop V1.2.1
In this workshop you will learn how to develop and deploy applications in DSX Local. The workshop has been divided into several stand-alone parts for those who are interested in a specific development tool or deployment task.

This lab is meant to be instructor-led.  That is, the instructor will explain the objectives of the DSX capabilities covered in each lab, and demonstrate some of those capabilities at the beginning of each lab.


## About this repository
This repository contains several lab subfolders. Some labs include notebooks and data, while others have additional instructions that are located in the *Lab Instructions* folder. 

## Prerequisites
1. Knowledge of analytics. These labs do not teach you the basics of analytics or how to implement analytics in R, Python and SPSS. The purpose of this workshop is to provide hands-on experience with analytics tools and deployment functions in DSX Local. 
2. To run this workshop you need an instance of DSX Local V1.2.1. 
3. Download the [DSX_Local_V121_Workshop.zip](https://github.com/SidneyPhoon/DSX_Local_Workshop_V12/blob/master/DSX%20Local%20Projects/DSX_Local_V12_Workshop.zip?raw=true).

### Setting up lab projects in DSX Local
1. Rename the downloaded **DSX_Local_V121_Workshop.zip** file and give it a unique name.  For example, add your initials.    *Note: Project names in DSX Local cluster must be unique. When we create a project "from file", the project name is inherited from the file name*.
2. Log in to DSX Local.
3. Select "New Project" and select "From File".
4. Browse to the .zip file and click **Create**.
![ProjectFromFile](/img/CreateProjectFromFile.png?raw=true).

### Lab 1: Build, Save and Test SparkML Models (Jupyter/Python)
1. Open the project you just created. 
2. Navigate to **Assets** view, in the **Notebooks** section open **TelcoChurn_SparkML** *Jupyter* notebook. This notebook has been implemented for the Python 2.7 runtime. The version of the runtime is displayed on the top right corner of the notebook. You can verify the runtime by running the first cell in the notebook. 
3. Follow instructions in the notebook.

### Lab 2: Create Batch Script and Test Batch Scoring (Python)
1. You must have completed "Lab 1: Build, Save and Test SparkML Models" before working through this lab.
2. Navigate the to the **Models** section of the project and click into the saved **Telco_Churn_ML_model**.
3. Click the **Batch score** tab.
4. For **Input data set**, select *new_customer_churn_data.csv*.
5. For **Output data set**, check **"Local file"** and specify *new_customers_scores.csv*.
6. On the top right, click **Advanced Settings**.
7. Scroll through the Advanced Setting to see the various options.  Click **Save** to save the default settings.
8. Click **Generate Batch Script**.  (Note: the batch script can be edited. For example, to perform pre/post processing tasks)

![batchscoring](/img/batch_scoring.png?raw=true)

9. Click **Run now**. Wait till the status changes to Success or refresh the browser to see the job status (Scroll to the bottom of page to see the job status).
10. Verify that the *new_customers_scores.csv* is in the data section of the project.
<br/>

### Lab 3: Create Model Evaluation Script and Test Evaluation (Python)
1. You must have completed "Lab 1: Build, Save and Test SparkML Models" before working through this lab.
2. Navigate the to the **Models** section of the project and click into the saved **Telco_Churn_ML_model**.
3. Click the **Evaluate** tab.
4. For the scripts inputs, specify these values.<br/>
![model_eval](/img/model_eval.png?raw=true)

5. Click **Advanced Settings** and change the name of the script. For example, you can name it ChurnModelEvalScript. Click Save.
6. Click **Generate evaluation Script**.
7. Click **Run now**. Wait till the status changes to Success or refresh the browser to see the job status (Scroll to the bottom of page to see the job status).
8. To see the results of the model evaluation, navigate the to the **Models** section of the project and click into the model  **Telco_Churn_ML_model**.  Scroll down to the **Evaluation results** section.<br/>
![model_eval_results](/img/model_eval_results.png?raw=true)

<br/>

### Lab 4: Build R models in Jupyter and deploy R model.  Test and evaluate R model, run Shiny App with embedded model.
1. Navigate to **Assets** view, in the **Notebooks** section open **DriverClassification** notebook.  
2. Execute the code cells in the notebook, making sure to save the model into the RStudio directory and the ML Repository
3. Navigate the to the **Models** section and click into the saved **BrakeEventClassifier**.
4. Click the **Real-time score** tab.  
   * Enter these values and click Submit to test the model, brake_time_sec=5, brake_distance_ft=15, road_type=highway, braking_score=100, brake_pressure20pct=1, brake_pressure40pct=1, brake_pressure60pct=1, brake_pressure80pct=0, brake_pressure100pct=0, abs_event=0, travel_speed=65
5. Click the **Batch score** tab.
   - For **Input data set**, select *new_brake_events.csv*.
   - For **Output data set**, specify *new_brake_events_scores.csv*.
   - On the top right, click **Advanced Settings**.
   - Scroll through the Advanced Setting to see the various options.  Click **Save** to save the default settings.
   - Click **Generate Batch Script**.  
   - Click Click **Run now**.  Refresh the browser to see the job status (Scroll to the bottom of page to see the job status).
   - Verify that the *new_brake_events_scores.csv* is in the data section of the project.
   <br/>
6.  Navigate the to the **Models** section and click into the saved **BrakeEventClassifier**.
7.  Click the **Evaluate** tab. 
    - For **Input data set**, select *brake_events_eval.csv*.  For **Threshold metric** select **Accuracy Score**.
    - Click **Advanced Settings** to review the default settings. Click Save.
    - Click **Generate evaluation Script**.
    - Click **Run now**. Refresh the browser to see the job status (Scroll to the bottom of page to see the job status).
    - To see the results of the model evaluation, navigate the to the **Models** section of the project and click into the model **BrakeEventClassifier**.  Scorll down to the **Evaluation results** section.
<br/>
8. Navigate the to the **RStudio** section and click **Open RStudio**
9. The "demoBrakeEvents" Shiny App is already included in this project.  Open demoBrakeEvents\server.R and run it.

### Lab 5: Deploy Project into Production
1. You must have completed Lab 1, Lab 2, Lab 3 and Lab 4 before working through this lab.
2. Data scientists have to commit changes to the project. You can commit assets by clicking on the 
Git action icon in the top right corner.  Select **Commit**, then **Push**. Specify the commit message about the changes you are committing, e.g. "deploy generated scripts".<br/>
![commit_push](/img/project_commit_push.png?raw=true)
3.  At this time, do not specify the version tag.<br/>
![commit_push](/img/project_push.png?raw=true)
4. Now we are assuming that a different person, a deployment admin, is taking over deployment. Click on the Git icon and select Commit History. Notice that we can add a tag to the project. <br/><br/>
A tag is used to identify a specific version of the project. There may be many versions of the assets in the project, but only specific versions should be used in production.<br/>
![commit_history](/img/commit_history.png?raw=true)
5.  Provide a tag, for example, WorkshopRelease, and click **Save**.
![commit_history tagged](/img/commit_history_tagged.png?raw=true)
6. Navigate to the **Deployment Manager**.  <br/>
![deployment_manager](/img/deployment_manager.png?raw=true)
7. Click **+ Add Project Release** to create a project release.
8. Specify the following inputs
  * **Name**: WorkshopRelease1-<your initials>
  * **Route**: release1 (this string will be used in all URLs that are generated by deployment, that’s why it can’t have spaces, upper case characters, and special characters). Important: if you’re sharing a cluster, make the route unique, for example, add initials to release1. 
  * **Source project**: the project that you want to deploy (e.g. "DSX_Local_V121_Workshop_<your initial>"
  * Tag: tag that you specified in the earlier steps. 

9. Click **Create**. This will take a few minutes because DSX is making a copy of all assets in the project.
10. The default view shows all assets that are a part of the project. Notice that you can filter them by type if you select the drop down. 
11.  Filter the assets by **Models**.
12. Click **Web service** to define an **Online Deployment** for the model.
13. Specify the name *telco-churn-online*.  Notice that the name gets appended to the URL (REST endpoint), that’s why it has to be lowercase with no special characters. 
14. Click **Create**
15. The **REST endpoint** is displayed in the model details. This endpoint won’t be live until we launch the project.<br/>
![mmd_rest_endpoint](/img/mmd_rest_endpoint.png?raw=true)<br/>
16. Filter the assets by **Scripts** and configure jobs for the batch scoring and model evaluation scripts.
17. Click the **Deployments** tab to list all the deployments you have created. <br/>
![mmd_deployments](/img/mmd_deployments.png?raw=true)<br/>
18. The deployments are in a disabled state because the project has not been launch.  Click the **Launch** button at the top right corner.<br/>
Launching the release will:
* Start all environments that will be used for deployment
* Enable the REST endpoints
* Enable URLs for “applications” (notebooks and Shiny)
* Enable schedules (if they are configured)
* Enable on-demand invocation of jobs. 

19. When all the deployments are enabled, click on any of the deployments and test them either with an API call or run a batch job on demand.






