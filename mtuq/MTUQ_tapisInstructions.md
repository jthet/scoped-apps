# Running MTUQ with Scoped Tapis UI

This guide will walk you through the steps to run the MTUQ application using the Scoped Tapis UI.

[Example Batch Job Submission](https://github.com/jthet/application-repository/blob/main/mtuq/job-batch.json) | [Example Interactive Job Submission](https://github.com/jthet/application-repository/blob/main/mtuq/job-interactive.json)

## Running Batch 

Running a batch job allows the user to execute one python script with MPI.

### Step 1: Log In
- Navigate to [https://seisscoped.org/tapis-ui/#/](https://seisscoped.org/tapis-ui/#/) and log in using your TACC account username and profile. Ensure you are registered under the "scoped" Tapis tenant.

### Step 2: Access the Dashboard
- Upon successful login, you will be directed to the dashboard.

### Step 3: Prepare Your Environment
- Before running the MTUQ app, you need to upload the Python script you want to execute to your `$SCRATCH` directory.

    #### Navigate to Your `$SCRATCH` Directory
    - Click on the **Files** tab located in the vertical toolbar on left side of the website.

    - You will see execution systems named `Frontera.exec` and `Stampede.exec`. Click on the `Frontera.exec` to access Frontera's file system, where your `$SCRATCH` directory is located.

    - **Note:** It's essential to know the path to your `$SCRATCH` directory. For example, mine is `/scratch1/09052/jacksont`. You can find yours by running `$echo $SCRATCH` on Frontera.

    - Enter your `$SCRATCH` directory path into the URL. For example:

        https://seisscoped.org/tapis-ui/#/files/Frontera.exec/scratch1/09052/jacksont/

    #### Upload Your Script
    - Upload the Python file you wish to execute by pressing the upload button in the file toolbar at the top of the page. Optionally, you can create a folder and place the file inside it using the folder button.
    - The script I'm using is `DetailedAnalysis.py`, available at [https://github.com/uafgeotools/mtuq/blob/master/examples/DetailedAnalysis.py](https://github.com/uafgeotools/mtuq/blob/master/examples/DetailedAnalysis.py).

### Step 4: Run the MTUQ App

- Navigate to the **Apps** tab, located below the Files tab on the vertical toolbar. Look for the `mtuq-batch v1.0` app and select it.
    - Follow the on-screen instructions, clicking **continue** until you reach the **File Inputs** section of the job launcher.
    - In the **File Inputs** section, input the **Source URL** of the Python file, preceded by `tapis://`. Do not modify the **Target Path**. 
    
        For example: 
        `tapis://Frontera.exec/scratch1/09052/jacksont/DetailedAnalysis.py`.
    
    - Press the **Skip to the end** button to proceed.

    #### Submit the Job
    - Press the `submit` button
    - **Note**: If you have more than one allocation, you may need to specify your allocation in the **Scheduler Options** section of the job launcher using `-A <your-allocation>` for the value.


### Step 5: Monitor Your Job
- To view your job and check its status, go to the **Jobs** tab on the left side of the website.

- Once the job is complete, the job status will be **FINISHED**
- You can then click on the job you ran, and the **See Files** button in the toolbar will take you to the tapis output directory associated with your job. To get to the actual MTUQ output, you need to go one directory up to the directory with the name of your job's UUID. For example, 

    `scratch1/09052/jacksont/jobs/7475cb5a-e343-4430-ba4d-7b1e553677cc-007/` 
    
    You should see relevant MTUQ output as data logs, graphs, and images.


## Running Interactive (Jupyter) 

1. To run a jupyter notebook version of MTUQ, simply select the `mtuq-interactive v1.0` app from the **Apps** tab. 

2. This application takes no input (except for the Scheduler Options to specify allocation, if applicable), so press the **Skip to End** button and then **Submit**

3. Check on your job status the same as in step 5 above, however now upon clicking the **See Files** button for your job you should see only one file: `tapisjob.out`

    - Download this file with the **Download** button in the Files toolbar. This file contains a Jupyter Notebook link.

    - This link will take you to an active Jupyter Notebook containing the MTUQ application.

    - In the Jupyter Notebook file system, the MTUQ directory should appear, however, it is possible it was bound inside a sub directory called **scoped**, so you may need to go into that directory to see the **MTUQ** directory.



## Contact Information

| Name          | Email                    | GitHub                           |
|---------------|--------------------------|----------------------------------|
| Jackson Thetford      | j.thetford @ utexas edu     | [jthet](https://github.com/jthet)
