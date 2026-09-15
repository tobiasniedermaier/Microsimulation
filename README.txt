COPD MARKOV-TO-MICROSIMULATION VALIDATION ARCHIVE

Purpose
-------
This archive contains the frozen baseline validation, the cleaned baseline model,
the illustrative acute-exacerbation memory extension, and the corresponding
single-run and repeated-seed validation outputs.

Code execution order
--------------------
1. code/Markov_microsim_validation_baseline_v3.R
   Independent technical validation of the baseline microsimulation against the
   deterministic simplified Markov benchmark (100 repeated seeds).

2. code/COPD_Markov_microsimulation_main_baseline.R
   Cleaned main baseline implementation.

3. code/COPD_microsimulation_AE_memory_extension.R
   Sources the cleaned main baseline file and adds explicit AE-event simulation
   with and without the illustrative recency-based memory assumption.

4. code/COPD_AE_memory_paired_validation.R
   Sources the memory extension and performs 20 paired repeated-seed runs using
   common random numbers.

Main validation findings
------------------------
- The deterministic implementation reproduced the frozen simplified Markov
  benchmark within predefined rounding tolerances.
- Across 100 baseline microsimulation repetitions (100,000 patients per
  smoking-status subcohort), mean endpoint deviations were close to zero.
- Maximum cycle-specific total variation distance was below 0.6% in all 100
  baseline repetitions.
- The event-level no-memory implementation reproduced the deterministic
  expected-value benchmark in expectation across 20 repetitions.
- The illustrative AE-memory assumption consistently increased direct and total
  societal costs, reduced QALYs, and increased recurrent exacerbation counts in
  all 20 paired repetitions.

Important interpretation
------------------------
The AE-memory assumption is illustrative and not empirically calibrated. It is
recency-based and non-cumulative: an AE resets a three-quarter decay profile with
a maximum relative AE-risk increase of 50%; effects do not stack.

Archive organization
--------------------
code/
results/baseline_validation_single_run/
results/baseline_validation_100_seeds/
results/main_baseline_model/
results/AE_memory_single_run/
results/AE_memory_paired_20_seeds/
