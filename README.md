# rma-tabuliser

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.5018140.svg)](https://doi.org/10.5281/zenodo.5018140) [![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0) ![GitHub release (latest by date)](https://img.shields.io/github/v/release/jfy133/rma-tabuliser) ![GitHub issues](https://img.shields.io/github/issues/jfy133/rma-tabuliser)



## Description

Bash script to generate count/taxon/OTU tables from RMA6 files (wrapper to
MEGAN6 rma2info).
## Requirements

**Mandatory**

  * MEGAN (>= v6.21.7)
    *  ⚠️ contents of `tools/` must be in `$PATH`, 
    *  (bio)conda install recommended
  * awk
  * sed
  * grep
  * cat
  * sort

**Optional**

  * GNU parallel 
    * For in-parallel processing of multiple input files

## Usage

```bash
$ rma-tabuliser -h

  RMA-TABULISER

  NAME
      
      rma-tabuliser - convert multiple MEGAN RMA6 files to count tables

  SYNOPSIS
      
      rma-tabuliser -d <input_directory> [OPTIONS]...

  DESCRIPTION
      
      rma-tabuliser is a bash script that takes multiple RMA6 files from MEGAN, extracts nodes and counts, and merges 
      this information into a table of samples as columns, and nodes as rows, aligned reads in cells. It also allows 
      some optional filtering functionality for Taxonomy-based tables based on taxonomic levels.
      
      Requires: MEGAN (>= v6.21.7) to be installed on your system, and the contents of the tools/ directory (in the 
      MEGAN installation path) to be in your $PATH. (Tip: the bioconda version of MEGAN puts these tools already in 
      your path).

      The resulting table, count_table.tsv, will be saved alongside the RMA6 files.

  OPTIONS
    
    MANDATORY

      -d [PATH]

      Input directory containing RMA6 files (RMA6  files should not be in in daughter-directories!)

    OPTIONAL

      -c [CLASS]      Type of count table to create. Options are: EC EGGNOG GTDB INTERPRO2GO KEGG SEED Taxonomy. Default: Taxonomy

      -h              Display this help message.

      -k              Specify to keep intermediate files.

      -n              Specify to print names of each feature, instead of ID numbers.

      -r [RANK]

        For Taxonomy class tables, specify which major taxonomic rank to filter from. Use first letter of the rank in 
        captials. Specify 'A' for no filtering (i.e. all ranks). Options are: A D K P C O F G S. Default A

      -s              Specify to summarise node counts, i.e. all

      -t [N_THREADS]
      
        Specify the number of threads to parallelise processing of files. Note: this requires GNU parallel to be 
        installed and avaliable on your $PATH. Default: 1

      -u              Specify to include unassigned reads in output table.



      -v              Print version to terminal.

      -V              Print verbose information during processing.



  EXAMPLES

      rma-tabuliser -d /path/to/files/
          Will generate a Taxonomy table, with node ID numbers at all taxonomic levels.

      rma-tabuliser -d /path/to/files/ -c Taxonomy -n -t 2 -r 'S'
          Will generate a Taxonomy table, with node names and filtered to S(pecies) level, processing 2 files at a time.

      rma-tabuliser -d /path/to/files/ -c Taxonomy -n -r 'G' -s
          Will generate a Taxonomy table, with node names and filtered to G(enus) level with counts on daughter nodes included in genus count.

  AUTHOR
      
      James A. Fellows Yates (jfy133@gmail.com)

  VERSION

    0.0.1


```
