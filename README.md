# eggd_vep_CENCNV_config

Json configuration file for CEN assay CNV variant annotation using VEP.

## What does this config do?

Configuration file required to annotate a vcf using [Variant Effect Predictor](https://github.com/Ensembl/ensembl-vep) implementation [eggd_vep](https://github.com/eastgenomics/eggd_vep).

A variable level of annotation can be achieved by different combinations of custom annotation, vep plugins in addition to the required VEP resources.

## What does this config version contain?

This config repo contains two json files for the genome builds GRCh38 and GRCh37.
These json files provide information about annotations, plugins, required fields and the genome version.

| Key | GRCh37 | GRCh38 |
|--------------|--------------|--------------|
| **vep_docker** | vep_v107.0.tar.gz | vep_v107.0.tar.gz |
| **plugin_config** | plugin_config.txt | plugin_config.txt |
| **vep_cache** | homo_sapiens_refseq_vep_107_GRCh37.tar.gz | homo_sapiens_refseq_vep_107_GRCh38.tar.gz |
| **reference_fasta** | Homo_sapiens.GRCh37.dna.toplevel.fa.gz | Homo_sapiens.GRCh38.dna.toplevel.fa.gz |
| **reference_fai** | Homo_sapiens.GRCh37.dna.toplevel.fa.gz.fai | Homo_sapiens.GRCh38.dna.toplevel.fa.gz.fai |
| **reference_gzi** | Homo_sapiens.GRCh37.dna.toplevel.fa.gz.gzi | Homo_sapiens.GRCh38.dna.toplevel.fa.gz.gzi |
| **ref_bcftools** | hs37d5.fasta-index.tar.gz | GRCh38_GIABv3_no_alt_analysis_set_maskedGRC_decoys_MAP2K3_KMT2C_KCNJ18_noChr.fasta-index.tar.gz |
| **Custom Annotation sources** | No custom annotation for CNV analysis currently | No custom annotation for CNV analysis currently |

## Notes

  How to check the names of all the files included in the config:

```bash
config_file=<config_filename>.json

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
