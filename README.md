# crack

NAMING CONVENTION
within crack/data, there are 56 .mat files. Each file contains processed calcium imaging data for one session from one animal. example: cc029L-3.mat. cc029 is the animal name, 3 is the behavior session number. note: the presence of the 'L' indicates if one or two areas were recorded simultaneously and can be disregarded.

DATA STRUCTURE
within each .mat file, you will see the following variables saved: CaA0*, CaA1*, licks, summary, trials
*CaA0 or CaA1 may not be present in sessions without 'L' in name

CaA0/CaA1
    these contain the calcium data for each of the areas (A0 or A1).
    important fields:
    CaA#.F_dF: the fluorescence traces.  an N by 1 cell where N is the number of trials session. each cell contains an M x P double array where M is the number of ROIs and P is     the number of timepoints in the nth trial. 
    CaA#.deconv: the deconvolved calcium events.  an 1 by N cell where N is the number of trials session. each cell contains an M x P double array where M is the number of ROIs     and P is the number of timepoints in the Nth trial. 
    CaA#.celltype: the decoded celltypes of the recorded ROIs.  an M x 1 double array where the number indicates the decoded cell type of the ROI.
        CELL TYPE KEY: 
        0: undecoded; 
        1: Agmat; 
        2: Baz1a;
        3: Adamts2; 
        4: Pvalb;
        5: Sst; 
        6: Vip;
    CaA#.trial_info: contains trial info necessary to link calcium recording with behavior data. 1 x N cell where N is the number of trials. CaA0.trial_info{n}.mat_file tells       you the name of the nth trial which can be used to reference the correct trial in summary table (see summary table below)


trials
    contains behavior task information. each row is trial. relevant columns:
    time_stamp: start time of trial. used to match trial to correct 2P recording (see summary table below). 
    direction_1: rotation direction of sample stimulus (CW or CCW)
    direction_2: rotation direction of test stimulus (CW or CCW)
    decision: animal's decision for that trial (Hit, Miss, FA, or CR)
    task: whether the trial was performed during task or passive conditions (task = 1; passive = 0);

summary
    summary.table contains information necessary to link calcium recording from CaA0/CaA1 to the trial data. relevant columns:
    Bhv_Start_Time: corresponds with "time_stamp" columns of "trials"
    'A0_name': corresponds with CaA0.trial_info{n}.mat_file
    'A1_name': corresponds with CaA1.trial_info{n}.mat_file
    in other words, use A0_name to find correct calcium recording and Bhv_Start_time to find correct behavior data for the same trial. 

