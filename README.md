# eggd_vep_CENCNV_config
Json configuration file for CEN assay CNV variant annotation using VEP.

## What does this config do?

Configuration file required to annotate a vcf using [Variant Effect Predictor](https://github.com/Ensembl/ensembl-vep) implementation [eggd_vep](https://github.com/eastgenomics/eggd_vep).

A variable level of annotation can be achieved by different combinations of custom annotation, vep plugins in addition to the required VEP resources.

## What does this config version contain?

This json file provides information about annotations, plugins, required fields and the genome version.

* Genome build: GRCh37
* VEP required files:
  * vep_v107.0.tar.gz
  * plugin_config.txt
  * homo_sapiens_refseq_vep_107_GRCh37.tar.gz
  * Homo_sapiens.GRCh37.dna.toplevel.fa.gz
  * Homo_sapiens.GRCh37.dna.toplevel.fa.gz.fai
  * Homo_sapiens.GRCh37.dna.toplevel.fa.gz.gzi
  * hs37d5.fasta-index.tar.gz
* Custom Annotation sources:
  * None for CNV analysis at the moment.


## Notes
  How to check the names of all the files included in the config:

```bash
config_file=you_file_name.json

# Get the Vep Resources filenames
for file in  $(jq -r ' .vep_resources | .[]' $config_file);
do dx describe $file --json | jq -r '.name';
done

# Get Custom Annotation filenames
for file in  $(jq -r ' .custom_annotations[]|.resource_files[]|.file_id' $config_file);
do dx describe $file --json | jq -r '.name';
done

# Get Plugin Annotation filenames
for file in  $(jq -r ' .plugins[]|.resource_files[]|.file_id' $config_file);
do dx describe $file --json | jq -r '.name';
done

```


