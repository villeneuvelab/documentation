## Setting up you environment

Please, follow the instructions from [this page](./Neuroimaging-softwares)

## Pipeline usage

See the [README.md][vlpp-readme] on how to launch the pipeline outside of a job scheduler. You will probably want to submit the pipeline on the guillimin scheduler, we'll see that in a few moments

## `vlpp-batch`

The tool `vlpp-batch` helps you build scripts to submit to the guillimin scheduler automatically. The tool needs to know where is your data on the cluster. In this example, we suppose that your data is organized with this structure:

```
/path
  |--freesurfer
    |--subject_00_type1
    |--subject_01_type1
/other_path
  |--pet
    |--subject_00_20170308
      |--NAV_subject_00_20170308_1435.mnc
    |--subject_01_20170315
      |--NAV_subject_01_20170315_1126.mnc
```

Create a new directory in which you will run all the commands for the processing, for example:

```
cd <your-user-directory>
mkdir pet_processing
cd pet_processing
```

#### Participants file

With this kind of structure, you have to create a `participants.tsv` file with at least 3 columns. A tsv (tabulation-separated values) file is the same as a csv file but tabulation is used to separated data.

| participant_id | fs_dir | pet_dir |
| --- | --- | --- |
| s00 | subject_00_type1 | subject_00_20170308 |
| s01 | subject_01_type1 | subject_01_20170315 |

With `participants.tsv` created, submit your jobs to the scheduler. The tool creates batch files in the `code` directory and submit them.

`vlpp-batch -f /path/freesurfer -p /other_path/pet -t participants.tsv --submit`

It is best practice to launch `vlpp-batch` without the `--submit` option and review the batch files. After review, launch the line with the `--submit` option.

You can check the status of your jobs with `qstat -u <your-username>`. See [this page][mcgillHPC-job] to know more.

#### Configuration file

If you want to change the default parameter of the pipeline, create a `config.cfg` file inside the `code` directory and edit this file with your parameters. Read the [default parameters file][vlpp-default] to understand the parameters of the pipeline.

```
mkdir code
touch code/config.cfg
```

For example, if you want to change the smoothing kernel to 8mm instead of the default 6mm, here is the content of
`code/config.cfg` you should have :

```
pet2anat {
    pet {
        fwhm = 8
    }
}
```

#### Example with PAD dataset

Content of `code/config.cfg`

```
dataset = "PAD"
```

If you are working with the PAD dataset, base freesurfer and PET directories are already known. You still need to create `participants.tsv` but launching `vlpp-batch` is much simpler.

`vlpp-batch -m pad -t participants.tsv --submit`

## `vlpp-qa`

When all the subjects are processed, launch this script from the same directory to produce Quality Assessment dashboards. Open `qa/registration_T1w.html` with firefox or chrome.

## `vlpp-extract-stats`

When all the subjects are processed, launch this script from the same directory to extract the means of all of your subjects into one convenient file. It will be located inside the `stats` directory.

For example, `group_time-4070_space-anat_ref-cerebellumCortex_suvr.tsv` contains the SUVR means (cerebellum cortex as a reference) of each freesurfer and pibindex ROIs of all your subjects in the native space.

[vlpp-readme]: https://github.com/villeneuvelab/vlpp/blob/master/README.md
[mcgillHPC-job]: http://www.hpc.mcgill.ca/index.php/starthere/81-doc-pages/91-guillimin-job-submit#h1-job-management-commands
[vlpp-default]: https://github.com/villeneuvelab/vlpp/blob/master/config/default.config
