Hands-on Lab: Variant Calling
=============================

A typical variant calling workflow consists of the following steps:


* Step 1: Extract DNA from sample (experimental)
* Step 2: Sequence DNA (experimental)
* Step 3: Align reads to reference genome (computational)
* Step 4: Identify genomic variants (computational)


For the purposes of this lab, we will focus on Step 4 and assume the first three steps have
already been performed. After Step 3, our data consists of a file of aligned reads in ``sam``
format, and a reference genome in ``fna`` format. We will be using the ``samtools`` software 
package to do Step 4.


Identify Genomic Variants
-------------------------

First, make a new directory, create a new or copy one of your old ``job.slurm`` scripts for this
exercise, and collect the following two inputs:

.. code-block:: console

    [ls6]$ cp /work/03439/wallen/public/samtools_example/ecoli_reads_aligned.sam ./
    [ls6]$ cp /work/03439/wallen/public/samtools_example/ecoli_NC_008253.fna ./


Second, find an appropriate ``samtools`` and ``bcftools`` packages in the module system and load them
into your environment.
Record the commands for this step for your ``job.slurm`` script. 

.. tip::

   This was tested with samtools v1.20 and bcftools v1.21

Then, adapt the following steps be replacing the ``[ALL_CAPS_FILENAME_PLACEHOLDERS]`` with appropriate
names for this exercise and put place them into your ``job.slurm`` script:

**Step 4a: First convert aligned reads from sam format to bam format**

.. code-block:: console

   samtools view -b -S -o [BINARY_ALIGNMENT_MAP] [ORIGINAL_SEQUENCE_ALIGNMENT]

**Step 4b: Sort the bam file**

.. code-block:: console

   samtools sort -o [SORTED_BINARY_ALIGNMENT_MAP] [BINARY_ALIGNMENT_MAP]

**Step 4c: Index the sorted bam file (sorting and indexing enables fast, efficient access)**

.. code-block:: console

   samtools index [SORTED_BINARY_ALIGNMENT_MAP]

**Step 4d: Identify genomic variants**

.. code-block:: console

   bcftools mpileup -f [REFERENCE_GENOME] -o [VARIANT_CALL_FILE] [SORTED_BINARY_ALIGNMENT_MAP]



.. note::

   Typical extensions for the file formats above are:

   * sequence alignment map = .sam
   * binary alignment map = .bam
   * variant call file = .vcf


The job should take less than 10 minutes on one node. Submit the job, monitor the job status in
the queue, and look for the results.
Make sure you understand which file was generated at each step and what it represents. Make sure
you can identify whether this job finished successfully or if ther were any errors.

BONUS
~~~~~

Visualize the genome in an idev session by performing the following:

.. code-block:: console

   samtools tview [SORTED_BINARY_ALIGNMENT_MAP] [REFERENCE_GENOME]


Additional Resources
--------------------

* Materials adapted from `SAMtools: A Primer <https://github.com/ecerami/samtools_primer>`_

