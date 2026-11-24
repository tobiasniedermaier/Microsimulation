COPD MARKOV-TO-MICROSIMULATION

Purpose
-------
This archive contains the R implementations and validation outputs accompanying
the study "Translating a COPD cohort Markov model into a patient-level
simulation: Technical validation and a history-dependent extension".

The archive documents the model lineage from the original COPD cohort Markov
model through its simplified R implementation to the technically validated
patient-level microsimulation and the illustrative acute-exacerbation (AE)
memory extension.

Code files
----------
1. code/Markov_model_Menn_Benchmark_Github.r
   Base-R reimplementation of the original COPD cohort Markov model by
   Menn et al. It retains GOLD grades 1-4, lung volume reduction surgery,
   lung transplantation, mild, moderate, and severe exacerbations, and death.

2. code/Markov_model_simplified_Github_incl_checks.r
   Simplified five-state Base-R cohort Markov model comprising GOLD grades
   1-4 and death. Includes deterministic calculations, internal consistency
   checks, and probabilistic sensitivity analysis.

3. code/Markov_model_simplified_heemod_with_PSA.R
   Independent implementation of the simplified cohort model using the
   heemod package, including deterministic and probabilistic analyses.
   This implementation was used only as an additional internal consistency
   check and did not generate the primary results reported in the manuscript.

4. code/Markov_microsim_validation_baseline_v3.R
   Independent technical validation of the benchmark-matched patient-level
   microsimulation against the deterministic simplified R cohort benchmark.
   Includes repeated-seed validation across 100 simulations.

5. code/COPD_Markov_microsimulation_main_baseline.R
   Clean baseline implementation containing the simplified deterministic
   cohort benchmark and the technically equivalent patient-level
   microsimulation. This file provides the validated baseline used by the
   subsequent event-level extensions.

6. code/COPD_microsimulation_AE_memory_extension.R
   Extends the validated baseline by explicitly sampling moderate and severe
   AEs at the patient level. Compares the expected-value baseline, an
   event-level model without AE memory, and an illustrative event-level model
   with a recency-based AE-memory mechanism.

7. code/COPD_AE_memory_paired_validation.R
   Repeated paired-seed validation of the event-level extension. Evaluates
   whether the no-memory event-level model reproduces the deterministic
   expected-value benchmark in expectation and quantifies the effect of
   AE memory across 20 paired simulations using common random numbers.

Recommended execution
---------------------
For reproduction of the primary analyses reported in the manuscript:

1. Run code/Markov_microsim_validation_baseline_v3.R
   to reproduce the baseline technical validation and the 100-seed analysis.

2. Run code/COPD_Markov_microsimulation_main_baseline.R
   to reproduce the cleaned benchmark and baseline microsimulation results.

3. Run code/COPD_microsimulation_AE_memory_extension.R
   to reproduce the single-run event-level analyses with and without AE memory.
   This script sources COPD_Markov_microsimulation_main_baseline.R.

4. Run code/COPD_AE_memory_paired_validation.R
   to reproduce the 20 paired repeated-seed analyses.
   This script sources COPD_microsimulation_AE_memory_extension.R.

The remaining three cohort-model scripts document the model lineage,
simplification, probabilistic analyses, and independent heemod consistency
check; they are not required to reproduce the primary microsimulation results.

Main validation findings
------------------------
- The deterministic implementation reproduced the simplified R cohort benchmark
  within predefined rounding tolerances.
- Across 100 baseline microsimulation repetitions with 100,000 patients per
  smoking-status subcohort, mean endpoint deviations were close to zero.
- Maximum cycle-specific total variation distance remained below 0.6% in all
  100 baseline repetitions.
- The event-level no-memory implementation reproduced the deterministic
  expected-value benchmark in expectation across 20 repetitions.
- The illustrative AE-memory mechanism consistently increased recurrent
  exacerbations, direct costs, and total societal costs and reduced QALYs
  across all 20 paired repetitions.

Important interpretation
------------------------
The AE-memory mechanism is illustrative and assumption-based rather than
empirically calibrated. It is recency-based and non-cumulative: after an AE,
the relative AE-risk increase is +50.0%, +33.3%, and +16.7% in the following
three quarterly cycles, respectively. A subsequent AE resets this three-cycle
decay profile; effects do not stack.

Archive organization
--------------------
code/
    R source files described above

results/baseline_validation_single_run/
    Single-run benchmark-versus-microsimulation validation outputs

results/baseline_validation_100_seeds/
    Results of the 100-replication baseline technical validation

results/main_baseline_model/
    Outputs from the cleaned baseline cohort and microsimulation implementation

results/AE_memory_single_run/
    Single-run event-level analyses with and without AE memory

results/AE_memory_paired_20_seeds/
    Results of the 20 paired repeated-seed AE-memory analyses

SHA256SUMS.txt
    SHA-256 checksums for the files in this archive
