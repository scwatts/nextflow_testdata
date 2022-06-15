Manually generated rather - currently no process implemented to use nf-core/picard/collectwgsmetrics
```bash
REF_GENOME_FASTA_FP=/path/to/hg38.fa
for file in ../read_sets/*bam; do
  fn=${file##*/};
  sn=${fn/.bam/};
  java \
    -Dsamjdk.use_async_io_read_samtools=true \
    -Dsamjdk.use_async_io_write_samtools=true \
    -Dsamjdk.use_async_io_write_tribble=true \
    -Dsamjdk.buffer_size=4194304 \
    -jar /opt/conda/share/picard-2.27.3-0/picard.jar \
      CollectWgsMetrics \
        INPUT=${file} \
        REFERENCE_SEQUENCE=${REF_GENOME_FASTA_FP} \
        MINIMUM_MAPPING_QUALITY=20 \
        MINIMUM_BASE_QUALITY=10 \
        COVERAGE_CAP=250 \
        OUTPUT=${sn}_wgs_metrics.txt;
done
```
