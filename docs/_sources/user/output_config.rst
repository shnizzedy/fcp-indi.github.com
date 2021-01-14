:orphan:

Output Settings
----------------

.. figure:: /_images/output_gui.png

#. **Working Directory - [path]:** Directory where CPAC should store temporary and intermediate files.  *Path should not contain spaces.*

#. **Output Directory - [path]:** Directory where CPAC should place processed data.  This can also be an S3 bucket path prepended with 's3://'.  *Path should not contain spaces.*

#. **Log Directory - [path]:** Directory where CPAC should place run logs.  *Path should not contain spaces.*

#. **Crash Log Directory - [path]:** Directory where CPAC should write crash logs.  *Path should not contain spaces.*

#. **AWS Output Bucket Credentials (optional) - [path]:**  If setting the *Output Directory* to an S3  bucket, insert the path to your AWS credentials file here.,

#. **S3 Encryption - [On, Off]:** Enable server-side 256-AES encryption on data to the S3 bucket,

#. **Write Extra Functional Outputs - [On, Off]:** Include extra versions and intermediate steps of functional preprocessing in the output directory.

#. **Write Debugging Outputs - [On, Off]:** Include extra outputs in the output directory that may be of interest when more information about intermediate steps is needed.

#. **Enable logging - [On, Off]:** Whether to write log details of the pipeline. run to the logging files..

#. **Remove Working Directory [On, Off]:** Deletes the contents of the Working Directory after running.  This saves disk space, but any additional preprocessing or analysis will have to be completely re-run.)

#. **Create organized output directory - [On, Off]:** Create a simplified version of the output directory.

#. **Regenerate Outputs - [On, Off]:**  Uses the contents of the working directory to regenerate all outputs and their symbolic links.  Requires an intact working directory from a previous C-PAC run.

#. **Enable Quality Control Interface - [On, Off]:** Generate quality control pages containing preprocessing and derivative outputs.

Configuration Without the GUI
""""""""""""""""""""""""""""""

The following key/value pairs must be defined in your :doc:`pipeline configuration YAML </user/pipelines/pipeline_config>` for C-PAC to run:

.. table::
   :widths: 20,30,15

    +------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    | Key                                                                                                              | Description                                                                                                                                                                | Potential Values                                                                            |
    +==================================================================================================================+============================================================================================================================================================================+=============================================================================================+
    | FROM                                                                                                             | A pipeline configuration to base this pipeline on, for inferring unspecified configuration options.                                                                        | A path (e.g.,’/data/another_analysis/pipeline.yml’) or the name of a preconfigured pipeline |
    +----------------+-------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    | pipeline_setup | pipeline_name                                                                                   | A name that you would like to give to this pipeline.                                                                                                                       | A string.                                                                                   |
    |                +---------------------+---------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    |                | output_directory    | path                                                                      | The output directory for the pipeline.                                                                                                                                     | A path (e.g.,’/data/my_analysis/output’).                                                   |
    |                |                     +---------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    |                |                     | write_func_outputs                                                        | Include extra versions and intermediate steps of functional preprocessing in the output directory.                                                                         | On, Off, True, False                                                                        |
    |                |                     +---------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    |                |                     | write_debugging_outputs                                                   | Include extra outputs in the output directory that may be of interest when more information is needed.                                                                     | On, Off, True, False                                                                        |
    |                |                     +---------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    |                |                     | output_tree                                                               | Output directory format and structure.                                                                                                                                     | default, ndmg                                                                               |
    |                |                     +---------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    |                |                     | generate_quality_control_images                                           | Generate quality control pages containing preprocessing and derivative outputs.                                                                                            | On, Off, True, False                                                                        |
    |                +---------------------+---------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    |                | working_directory   | path                                                                      | The working directory to be used by the pipeline during the run.                                                                                                           | A path (e.g.,’/data/my_analysis/working’).                                                  |
    |                |                     +---------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    |                |                     | remove_working_dir                                                        | Deletes the contents of the Working Directory after running. This saves disk space, but any additional preprocessing or analysis will have to be completely re-run.        | On, Off, True, False                                                                        |
    |                +---------------------+---------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    |                | log_directory       | path                                                                      | Directory where CPAC should place run logs.                                                                                                                                | A path (e.g.,’/data/my_analysis/logs’).                                                     |
    |                |                     +---------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    |                |                     | run_logging                                                               | Whether to write log details of the pipeline run to the logging files.                                                                                                     | On, Off, True, False                                                                        |
    |                +---------------------+---------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    |                | crash_log_directory | path                                                                      | The directory where C-PAC will store crash logs.                                                                                                                           | A path (e.g.,’/data/my_analysis/crash’).                                                    |
    |                +---------------------+---------------------------------+-----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    |                | system_config       | on_grid                         | run                                     | Select Off if you intend to run CPAC on a single machine. If set to On, CPAC will attempt to submit jobs through the job scheduler / resource manager selected below.      | On, Off, True, False                                                                        |
    |                |                     |                                 +-----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    |                |                     |                                 | resource_manager                        | Sun Grid Engine (SGE), Portable Batch System (PBS), or Simple Linux Utility for Resource Management (SLURM). Only applies if you are running on a grid or compute cluster. | SGE, PBS, SLURM                                                                             |
    |                |                     |                                 +-----+-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    |                |                     |                                 | SGE | parallel_environment              | SGE Parallel Environment to use when running CPAC. Only applies when you are running on a grid or compute cluster using SGE.                                               | A string.                                                                                   |
    |                |                     |                                 |     +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    |                |                     |                                 |     | queue                             | SGE Queue to use when running CPAC. Only applies when you are running on a grid or compute cluster using SGE.                                                              | A string.                                                                                   |
    |                |                     +---------------------------------+-----+-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    |                |                     | maximum_memory_per_participant                                            | The maximum amount of memory each participant's workflow can allocate.                                                                                                     | A number (GB).                                                                              |
    |                |                     +---------------------------------+-----+-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    |                |                     | max_cores_per_participant                                                 | The maximum amount of cores (on a single machine) or slots on a node (on a cluster/grid) to allocate per participant.                                                      | An integer.                                                                                 |
    |                |                     +---------------------------------+-----+-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    |                |                     | num_ants_threads                                                          | The number of cores to allocate to ANTS-based anatomical registration per participant.                                                                                     | An integer.                                                                                 |
    |                |                     +---------------------------------+-----+-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    |                |                     | num_participants_at_once                                                  | The number of participant workflows to run at the same time.                                                                                                               | An integer.                                                                                 |
    |                +---------------------+---------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    |                | Amazon-AWS          | aws_output_bucket_credentials                                             | Path to a set of AWS credentials if your output directory is set to an S3 bucket.                                                                                          | A path (e.g.,’/data/my_analysis/credentials.csv’).                                          |
    |                |                     +---------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
    |                |                     | s3_encryption                                                             | Enable server-side 256-AES encryption on data to the S3 bucket.                                                                                                            | An integer.                                                                                 |
    +----------------+---------------------+---------------------------------+-----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+

The box below contains an example of what these parameters might look like when defined in the YAML

.. code-block:: YAML

   FROM: default
   pipeline_setup:
     pipeline_name: cpac-default-pipeline
     output_directory:
       path: /output
       write_func_outputs: False
       write_debugging_outputs: False
       output_tree: "default"
       generate_quality_control_images: True
     working_directory:
       path: /tmp
       remove_working_dir: True
     log_directory:
       path: /logs
       run_logging: True
     crash_log_directory:
       path: /crash
     system_config:
       on_grid:
         run: Off
         resource_manager: SGE  
         SGE:
           parallel_environment:  mpi_smp
           queue:  all.q
       maximum_memory_per_participant: 1
       max_cores_per_participant: 1
       num_ants_threads: 1
       num_participants_at_once: 1
     Amazon-AWS:
       aws_output_bucket_credentials:
       s3_encryption: False
