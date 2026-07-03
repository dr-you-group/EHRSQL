# EHRSQL Skeleton v2 Change Summary

## Scope

- Total skeleton questions: 174
- Changed skeleton SQL: 61
- Unchanged skeleton SQL: 113
- Comparison base: `ehrsql_question_skeletons.csv:skeleton_sql`
- v2 target: `ehrsql_question_skeletons_v2.csv:skeleton_sql` and `mimiciv_cdm_query_template`

## Template Column Check

- `mimiciii_query_template` preserved from original: 174/174
- `mimiciv_cdm_query_template` equals v2 `skeleton_sql`: 174/174
- Non-empty `mimiciii_query_template` in v2: 167
- Empty in original and therefore empty in v2: ehrsql_168, ehrsql_169, ehrsql_174, ehrsql_172, ehrsql_173, ehrsql_170, ehrsql_171

## Category Counts

| Category | Count | Meaning |
|---|---:|---|
| `unchanged` | 113 | No skeleton SQL change |
| `cte_deduplication` | 26 | Index event CTE made distinct to avoid duplicate event fanout |
| `topk_late_concept_join` | 23 | Top-k concept-name query rewritten to aggregate by concept_id before joining concept |
| `current_anchor` | 12 | Current/current_date logic rewritten to fixed anchor containment |
| `unsupported_cost_empty` | 9 | Unsupported by current CDM: cost table is empty |
| `unsupported_external_event_category_mapping` | 2 | Unsupported by current CDM: intake/output category mapping is external/missing |
| `percentile_aggregate_rewrite` | 1 | Percentile query rewritten from window percent_rank to exact aggregate expression |
| `measurement_age_support_aggregate` | 1 | Age-stratified lab top-k rewritten to exact age/date support aggregate |
| `measurement_event_lateral_rewrite` | 1 | Event-after lab top-k rewritten to lateral person/date range scans |
| `normality_range_fix` | 1 | Normal lab logic rewritten to use range_low/range_high |
| `measurement_top_support_aggregate` | 1 | Frequent lab top-k rewritten to exact measurement date-count support aggregate |
| `unsupported_external_abbreviation_dictionary` | 1 | Unsupported by current CDM: abbreviation dictionary is external/missing |

## Category Details

### unchanged (113)

No skeleton SQL change

| benchmark_id | changed | q_tag | summary |
|---|---|---|---|
| `ehrsql_007` | NO | what is the gender of patient {patient_id}? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_008` | NO | what is the date of birth of patient {patient_id}? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_015` | NO | what is_verb the age of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_017` | NO | what is_verb the marital status of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_016` | NO | what is_verb the name of insurance of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_125` | NO | count the number of patients who were admitted to the hospital [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_126` | NO | count the number of patients who were discharged from the hospital [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_060` | NO | what was the [time_filter_exact1] length of icu stay of patient {patient_id}? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_009` | NO | what was the [time_filter_exact1] length of hospital stay of patient {patient_id}? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_079` | NO | has_verb patient {patient_id} been admitted to the hospital [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_105` | NO | count the number of icu visits of patient {patient_id} [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_080` | NO | has_verb patient {patient_id} been to an emergency room [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_098` | NO | list the hospital admission time of patient {patient_id} [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_104` | NO | count the number of hospital visits of patient {patient_id} [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_127` | NO | count the number of patients who stayed in ward {ward_id} [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_128` | NO | count the number of patients who stayed in careunit {careunit} [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_057` | NO | when was the [time_filter_exact1] hospital admission time of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_028` | NO | what was the [time_filter_exact1] ward of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_029` | NO | what was the [time_filter_exact1] careunit of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_027` | NO | what was the [time_filter_exact1] hospital admission type of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_059` | NO | when was the [time_filter_exact1] hospital discharge time of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_058` | NO | when was the [time_filter_exact1] hospital admission time that patient {patient_id} was admitted via {admission_route} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_130` | NO | count the number of patients who were diagnosed with {diagnosis_name} [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_084` | NO | has_verb patient {patient_id} received any diagnosis [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_121` | NO | list the ids of patients diagnosed with {diagnosis_name} [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_085` | NO | has_verb patient {patient_id} been diagnosed with {diagnosis_name} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_032` | NO | what was the name of the diagnosis that patient {patient_id} [time_filter_exact1] received [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_061` | NO | when was the [time_filter_exact1] time that patient {patient_id} was diagnosed with {diagnosis_name} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_129` | NO | count the number of patients who were diagnosed with {diagnosis_name2} [time_filter_within] after having been diagnosed with {diagnosis_name1} [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_122` | NO | what is the [agg_function] [unit_average] number of patient records diagnosed with {diagnosis_name} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_001` | NO | what is the intake method of {drug_name}? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_137` | NO | count the number of {drug_name} prescription cases [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_136` | NO | count the number of patients who were prescribed {drug_name} [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_087` | NO | has_verb patient {patient_id} been prescribed any medication [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_107` | NO | count the number of drugs patient {patient_id} were prescribed [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_088` | NO | has_verb patient {patient_id} been prescribed {drug_name} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_108` | NO | count the number of times that patient {patient_id} were prescribed {drug_name} [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_039` | NO | what was the total amount of dose of {drug_name} that patient {patient_id} were prescribed [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_086` | NO | has_verb patient {patient_id} been prescribed {drug_name1}, {drug_name2}, or {drug_name3} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_064` | NO | when was the [time_filter_exact1] prescription time of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_035` | NO | what was the name of the drug that patient {patient_id} was [time_filter_exact1] prescribed [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_065` | NO | when was the [time_filter_exact1] time that patient {patient_id} was prescribed {drug_name} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_038` | NO | what was the dose of {drug_name} that patient {patient_id} was [time_filter_exact1] prescribed [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_034` | NO | what was the name of the drug that patient {patient_id} was [time_filter_exact1] prescribed via {drug_route} route [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_067` | NO | when was the [time_filter_exact1] time that patient {patient_id} was prescribed a medication via {drug_route} route [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_040` | NO | what was the name of the drug that patient {patient_id} were prescribed [n_times] [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_066` | NO | when was the [time_filter_exact1] time that patient {patient_id} was prescribed {drug_name1} and {drug_name2} [time_filter_within] [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_041` | NO | what is the new prescription of patient {patient_id} [time_filter_global2] compared to the prescription [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_081` | NO | has_verb patient {patient_id} received any procedure [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_135` | NO | count the number of {procedure_name} procedure cases [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_131` | NO | count the number of patients who received a {procedure_name} procedure [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_172` | NO | has_verb patient {patient_id} received a {procedure_name} procedure in other than the current hospital [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_082` | NO | has_verb patient {patient_id} received a {procedure_name} procedure [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_106` | NO | count the number of times that patient {patient_id} received a {procedure_name} procedure [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_062` | NO | when was the [time_filter_exact1] procedure time of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_033` | NO | what was the name of the procedure that patient {patient_id} [time_filter_exact1] received [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_063` | NO | when was the [time_filter_exact1] time that patient {patient_id} received a {procedure_name} procedure [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_132` | NO | count the number of patients who received a {procedure_name} procedure [n_times] [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_083` | NO | what was the name of the procedure that patient {patient_id} received [n_times] [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_142` | NO | count the number of patients who had a {intake_name} intake [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_140` | NO | count the number of patients who received a {lab_name} lab test [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_141` | NO | count the number of patients who received a {culture_name} microbiology test [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_089` | NO | has_verb patient {patient_id} received any lab test [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_091` | NO | has_verb patient {patient_id} had any microbiology test result [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_052` | NO | what was the total volume of output that patient {patient_id} had [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_049` | NO | what was the total volume of intake that patient {patient_id} received [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_053` | NO | what is the difference between the total volume of intake and output of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_094` | NO | has_verb patient {patient_id} had any {intake_name} intake [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_095` | NO | has_verb patient {patient_id} had any {output_name} output [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_090` | NO | has_verb patient {patient_id} received a {lab_name} lab test [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_092` | NO | has_verb patient {patient_id} had any {culture_name} microbiology test result [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_110` | NO | count the number of times that patient {patient_id} had a {intake_name} intake [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_111` | NO | count the number of times that patient {patient_id} had a {output_name} output [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_051` | NO | what was the total volume of {output_name} output that patient {patient_id} had [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_109` | NO | count the number of times that patient {patient_id} received a {lab_name} lab test [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_048` | NO | what was the total volume of {intake_name} intake that patient {patient_id} received [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_068` | NO | when was the [time_filter_exact1] lab test of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_074` | NO | when was the [time_filter_exact1] intake time of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_030` | NO | what was the [time_filter_exact1] measured height of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_031` | NO | what was the [time_filter_exact1] measured weight of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_071` | NO | when was the [time_filter_exact1] microbiology test of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_047` | NO | what was the name of the intake that patient {patient_id} [time_filter_exact1] had [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_050` | NO | what was the name of the output that patient {patient_id} [time_filter_exact1] had [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_043` | NO | what was the name of the lab test that patient {patient_id} [time_filter_exact1] received [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_046` | NO | what was the name of the specimen that patient {patient_id} was [time_filter_exact1] tested [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_054` | NO | what was the [time_filter_exact1] measured {vital_name} of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_072` | NO | when was patient {patient_id}'s [time_filter_exact1] {culture_name} microbiology test [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_073` | NO | when was the [time_filter_exact1] time that patient {patient_id} had a {intake_name} intake [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_075` | NO | when was the [time_filter_exact1] time that patient {patient_id} had a {output_name} output [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_076` | NO | when was the [time_filter_exact1] time that patient {patient_id} had a {vital_name} measured [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_069` | NO | when was the [time_filter_exact1] time that patient {patient_id} received a {lab_name} lab test [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_042` | NO | what was the [time_filter_exact1] measured value of a {lab_name} lab test of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_045` | NO | what was the organism name found in the [time_filter_exact1] {culture_name} microbiology test of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_093` | NO | has_verb there been any organism found in the [time_filter_exact1] {culture_name} microbiology test of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_078` | NO | when was the [time_filter_exact1] time that patient {patient_id} had the [sort] {vital_name} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_070` | NO | when was the [time_filter_exact1] time that patient {patient_id} had the [sort] value of {lab_name} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_055` | NO | what was the [agg_function] {vital_name} of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_044` | NO | what was the [agg_function] {lab_name} value of patient {patient_id} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_096` | NO | has_verb the {vital_name} of patient {patient_id} been ever [comparison] than {vital_value} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_077` | NO | when was the [time_filter_exact1] time that the {vital_name} of patient {patient_id} was [comparison] than {vital_value} [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_100` | NO | list the [unit_average] [agg_function] weight of patient {patient_id} [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_103` | NO | list the [unit_average] [agg_function] {vital_name} of patient {patient_id} [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_099` | NO | list the [unit_average] [agg_function] {lab_name} lab value of patient {patient_id} [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_102` | NO | list the [unit_average] [agg_function] volume of {output_name} output that patient {patient_id} had [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_101` | NO | list the [unit_average] [agg_function] volume of {intake_name} intake that patient {patient_id} received [time_filter_global1]. | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_014` | NO | is the {vital_name} of patient {patient_id} [time_filter_exact2] measured [time_filter_global2] [comparison] than the [time_filter_exact1] value measured [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_013` | NO | is the value of {lab_name} of patient {patient_id} [time_filter_exact2] measured [time_filter_global2] [comparison] than the [time_filter_exact1] value measured [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_010` | NO | what is the change in the weight of patient {patient_id} from the [time_filter_exact2] value measured [time_filter_global2] compared to the [time_filter_exact1] value measured [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_012` | NO | what is the change in the {vital_name} of patient {patient_id} from the [time_filter_exact2] value measured [time_filter_global2] compared to the [time_filter_exact1] value measured [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_011` | NO | what is the change in the value of {lab_name} of patient {patient_id} from the [time_filter_exact2] value measured [time_filter_global2] compared to the [time_filter_exact1] value measured [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_173` | NO | has_verb patient {patient_id} had any allergy [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_170` | NO | what was the name of the allergy that patient {patient_id} had [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |
| `ehrsql_171` | NO | what was the name of the substance that patient {patient_id} was allergic to [time_filter_global1]? | skeleton_sql is unchanged after whitespace normalization |

### cte_deduplication (26)

Index event CTE made distinct to avoid duplicate event fanout

| benchmark_id | changed | q_tag | summary |
|---|---|---|---|
| `ehrsql_157` | YES | what are_verb the top [n_rank] frequently prescribed drugs that patients aged [age_group] were prescribed [time_filter_within] after having been diagnosed with {diagnosis_name} [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_158` | YES | what are_verb the top [n_rank] frequently prescribed drugs that {gender} patients aged [age_group] were prescribed [time_filter_within] after having been diagnosed with {diagnosis_name} [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_124` | YES | count the number of patients who did not come back to the hospital [time_filter_within] after diagnosed with {diagnosis_name} [time_filter_global1]. | index event CTE now selects distinct person/date pairs |
| `ehrsql_114` | YES | what is the [n_survival_period] survival rate of patients diagnosed with {diagnosis_name}? | index event CTE now selects distinct person/date pairs |
| `ehrsql_123` | YES | count the number of patients who were dead after having been diagnosed with {diagnosis_name} [time_filter_within] [time_filter_global1]. | index event CTE now selects distinct person/date pairs |
| `ehrsql_116` | YES | what are the top [n_rank] diagnoses that have the highest [n_survival_period] mortality rate? | index event CTE now selects distinct person/date pairs |
| `ehrsql_146` | YES | what are_verb the top [n_rank] frequent diagnoses that patients were diagnosed [time_filter_within] after having been diagnosed with {diagnosis_name} [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_139` | YES | count the number of patients who were prescribed {drug_name} [time_filter_within] after having been diagnosed with {diagnosis_name} [time_filter_global1]. | index event CTE now selects distinct person/date pairs |
| `ehrsql_036` | YES | what was the name of the drug that patient {patient_id} was prescribed [time_filter_within] after having been diagnosed with {diagnosis_name} [time_filter_global1]? | index event CTE now selects distinct person/date pairs |
| `ehrsql_115` | YES | what is the [n_survival_period] survival rate of patients who were prescribed {drug_name} after having been diagnosed with {diagnosis_name}? | index event CTE now selects distinct person/date pairs |
| `ehrsql_156` | YES | what are_verb the top [n_rank] frequently prescribed drugs that patients were prescribed [time_filter_within] after having been diagnosed with {diagnosis_name} [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_174` | YES | count the number of patients who were diagnosed with {diagnosis_name} [time_filter_within] after having received a {procedure_name} procedure [time_filter_global1]. | index event CTE now selects distinct person/date pairs |
| `ehrsql_134` | YES | count the number of patients who received a {procedure_name} procedure [time_filter_within] after having been diagnosed with {diagnosis_name} [time_filter_global1]. | index event CTE now selects distinct person/date pairs |
| `ehrsql_145` | YES | what are_verb the top [n_rank] frequent diagnoses that patients were diagnosed [time_filter_within] after having received a {procedure_name} procedure [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_150` | YES | what are_verb the top [n_rank] frequent procedures that patients received [time_filter_within] after having been diagnosed with {diagnosis_name} [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_161` | YES | what are_verb the top [n_rank] frequent lab tests that patients had [time_filter_within] after having been diagnosed with {diagnosis_name} [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_164` | YES | what are_verb the top [n_rank] frequent specimens that patients were tested [time_filter_within] after having been diagnosed with {diagnosis_name} [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_153` | YES | what are_verb the top [n_rank] frequent prescribed drugs for patients who were also prescribed {drug_name} [time_filter_within] [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_154` | YES | what are_verb the top [n_rank] frequent drugs that patients were prescribed [time_filter_within] after having been prescribed with {drug_name} [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_138` | YES | count the number of patients who were prescribed {drug_name} [time_filter_within] after having received a {procedure_name} procedure [time_filter_global1]. | index event CTE now selects distinct person/date pairs |
| `ehrsql_037` | YES | what was the name of the drug that patient {patient_id} was prescribed [time_filter_within] after having received a {procedure_name} procedure [time_filter_global1]? | index event CTE now selects distinct person/date pairs |
| `ehrsql_155` | YES | what are_verb the top [n_rank] frequently prescribed drugs that patients were prescribed [time_filter_within] after having received a {procedure_name} procedure [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_133` | YES | count the number of patients who received a {procedure_name2} procedure [time_filter_within] after having received a {procedure_name1} procedure [time_filter_global1]. | index event CTE now selects distinct person/date pairs |
| `ehrsql_149` | YES | what are_verb the top [n_rank] frequent procedures that patients received [time_filter_within] after having received a {procedure_name} procedure [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_162` | YES | what are_verb the top [n_rank] frequent lab tests that patients had [time_filter_within] after having received a {procedure_name} procedure [time_filter_global1]? | procedure-after lab top-k uses lateral person/date range scan over measurement ; concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_165` | YES | what are_verb the top [n_rank] frequent specimens that patients were tested [time_filter_within] after having received a {procedure_name} procedure [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |

### topk_late_concept_join (23)

Top-k concept-name query rewritten to aggregate by concept_id before joining concept

| benchmark_id | changed | q_tag | summary |
|---|---|---|---|
| `ehrsql_144` | YES | what are_verb the top [n_rank] frequent diagnoses of patients aged [age_group] [time_filter_global1]? | concept table join moved after top-k aggregation |
| `ehrsql_152` | YES | what are_verb the top [n_rank] frequently prescribed drugs of patients aged [age_group] [time_filter_global1]? | concept table join moved after top-k aggregation |
| `ehrsql_148` | YES | what are_verb the top [n_rank] frequent procedures of patients aged [age_group] [time_filter_global1]? | concept table join moved after top-k aggregation |
| `ehrsql_160` | YES | what are_verb the top [n_rank] frequent lab tests of patients aged [age_group] [time_filter_global1]? | age-stratified top lab tests use mimiciv.schera_measurement_concept_date_age_counts ; concept table join moved after top-k aggregation |
| `ehrsql_157` | YES | what are_verb the top [n_rank] frequently prescribed drugs that patients aged [age_group] were prescribed [time_filter_within] after having been diagnosed with {diagnosis_name} [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_158` | YES | what are_verb the top [n_rank] frequently prescribed drugs that {gender} patients aged [age_group] were prescribed [time_filter_within] after having been diagnosed with {diagnosis_name} [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_143` | YES | what are_verb the top [n_rank] frequent diagnoses [time_filter_global1]? | concept table join moved after top-k aggregation |
| `ehrsql_146` | YES | what are_verb the top [n_rank] frequent diagnoses that patients were diagnosed [time_filter_within] after having been diagnosed with {diagnosis_name} [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_156` | YES | what are_verb the top [n_rank] frequently prescribed drugs that patients were prescribed [time_filter_within] after having been diagnosed with {diagnosis_name} [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_145` | YES | what are_verb the top [n_rank] frequent diagnoses that patients were diagnosed [time_filter_within] after having received a {procedure_name} procedure [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_150` | YES | what are_verb the top [n_rank] frequent procedures that patients received [time_filter_within] after having been diagnosed with {diagnosis_name} [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_161` | YES | what are_verb the top [n_rank] frequent lab tests that patients had [time_filter_within] after having been diagnosed with {diagnosis_name} [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_164` | YES | what are_verb the top [n_rank] frequent specimens that patients were tested [time_filter_within] after having been diagnosed with {diagnosis_name} [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_151` | YES | what are_verb the top [n_rank] frequently prescribed drugs [time_filter_global1]? | concept table join moved after top-k aggregation |
| `ehrsql_153` | YES | what are_verb the top [n_rank] frequent prescribed drugs for patients who were also prescribed {drug_name} [time_filter_within] [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_154` | YES | what are_verb the top [n_rank] frequent drugs that patients were prescribed [time_filter_within] after having been prescribed with {drug_name} [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_155` | YES | what are_verb the top [n_rank] frequently prescribed drugs that patients were prescribed [time_filter_within] after having received a {procedure_name} procedure [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_147` | YES | what are_verb the top [n_rank] frequent procedures [time_filter_global1]? | concept table join moved after top-k aggregation |
| `ehrsql_149` | YES | what are_verb the top [n_rank] frequent procedures that patients received [time_filter_within] after having received a {procedure_name} procedure [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_162` | YES | what are_verb the top [n_rank] frequent lab tests that patients had [time_filter_within] after having received a {procedure_name} procedure [time_filter_global1]? | procedure-after lab top-k uses lateral person/date range scan over measurement ; concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_165` | YES | what are_verb the top [n_rank] frequent specimens that patients were tested [time_filter_within] after having received a {procedure_name} procedure [time_filter_global1]? | concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |
| `ehrsql_159` | YES | what are_verb the top [n_rank] frequent lab tests [time_filter_global1]? | top frequent lab tests use mimiciv.schera_measurement_concept_date_counts ; concept table join moved after top-k aggregation |
| `ehrsql_163` | YES | what are_verb the top [n_rank] frequent specimens tested [time_filter_global1]? | concept table join moved after top-k aggregation |

### current_anchor (12)

Current/current_date logic rewritten to fixed anchor containment

| benchmark_id | changed | q_tag | summary |
|---|---|---|---|
| `ehrsql_112` | YES | count the number of current patients. | current visit/date logic is evaluated against anchor_date 2215-01-16 instead of open-ended NULL/current_date semantics |
| `ehrsql_113` | YES | count the number of current patients aged [age_group]. | current visit/date logic is evaluated against anchor_date 2215-01-16 instead of open-ended NULL/current_date semantics |
| `ehrsql_020` | YES | how many [unit_count] have passed since patient {patient_id} was admitted to the icu currently? | current visit/date logic is evaluated against anchor_date 2215-01-16 instead of open-ended NULL/current_date semantics |
| `ehrsql_019` | YES | how many [unit_count] have passed since patient {patient_id} was admitted to the hospital currently? | current visit/date logic is evaluated against anchor_date 2215-01-16 instead of open-ended NULL/current_date semantics |
| `ehrsql_022` | YES | how many [unit_count] have passed since the [time_filter_exact1] time patient {patient_id} stayed in ward {ward_id} on the current hospital visit? | current visit/date logic is evaluated against anchor_date 2215-01-16 instead of open-ended NULL/current_date semantics |
| `ehrsql_021` | YES | how many [unit_count] have passed since the [time_filter_exact1] time patient {patient_id} stayed in careunit {careunit} on the current hospital visit? | current visit/date logic is evaluated against anchor_date 2215-01-16 instead of open-ended NULL/current_date semantics |
| `ehrsql_023` | YES | how many [unit_count] have passed since the [time_filter_exact1] time patient {patient_id} was diagnosed with {diagnosis_name} on the current hospital visit? | current visit/date logic is evaluated against anchor_date 2215-01-16 instead of open-ended NULL/current_date semantics |
| `ehrsql_024` | YES | how many [unit_count] have passed since the [time_filter_exact1] time patient {patient_id} was prescribed {drug_name} on the current hospital visit? | current visit/date logic is evaluated against anchor_date 2215-01-16 instead of open-ended NULL/current_date semantics |
| `ehrsql_168` | YES | how many [unit_count] have passed since the [time_filter_exact1] time patient {patient_id} received a procedure on the current hospital visit? | current visit/date logic is evaluated against anchor_date 2215-01-16 instead of open-ended NULL/current_date semantics |
| `ehrsql_169` | YES | how many [unit_count] have passed since the [time_filter_exact1] time patient {patient_id} received a {procedure_name} procedure on the current hospital visit? | current visit/date logic is evaluated against anchor_date 2215-01-16 instead of open-ended NULL/current_date semantics |
| `ehrsql_026` | YES | how many [unit_count] have passed since the [time_filter_exact1] time patient {patient_id} had a {intake_name} intake on the current icu visit? | current visit/date logic is evaluated against anchor_date 2215-01-16 instead of open-ended NULL/current_date semantics |
| `ehrsql_025` | YES | how many [unit_count] have passed since the [time_filter_exact1] time patient {patient_id} received a {lab_name} lab test on the current hospital visit? | current visit/date logic is evaluated against anchor_date 2215-01-16 instead of open-ended NULL/current_date semantics |

### unsupported_cost_empty (9)

Unsupported by current CDM: cost table is empty

| benchmark_id | changed | q_tag | summary |
|---|---|---|---|
| `ehrsql_005` | YES | what is the cost of diagnosing {diagnosis_name}? | rewritten to stub because mimiciv.cost has zero rows in the current CDM |
| `ehrsql_120` | YES | what is_verb the [agg_function] total hospital cost that involves a diagnosis named {diagnosis_name} [time_filter_global1]? | rewritten to stub because mimiciv.cost has zero rows in the current CDM |
| `ehrsql_004` | YES | what is the cost of a drug named {drug_name}? | rewritten to stub because mimiciv.cost has zero rows in the current CDM |
| `ehrsql_119` | YES | what is_verb the [agg_function] total hospital cost that involves a drug named {drug_name} [time_filter_global1]? | rewritten to stub because mimiciv.cost has zero rows in the current CDM |
| `ehrsql_002` | YES | what is the cost of a procedure named {procedure_name}? | rewritten to stub because mimiciv.cost has zero rows in the current CDM |
| `ehrsql_117` | YES | what is_verb the [agg_function] total hospital cost that involves a procedure named {procedure_name} [time_filter_global1]? | rewritten to stub because mimiciv.cost has zero rows in the current CDM |
| `ehrsql_003` | YES | what is the cost of a {lab_name} lab test? | rewritten to stub because mimiciv.cost has zero rows in the current CDM |
| `ehrsql_118` | YES | what is_verb the [agg_function] total hospital cost that involves a {lab_name} lab test [time_filter_global1]? | rewritten to stub because mimiciv.cost has zero rows in the current CDM |
| `ehrsql_056` | YES | what is_verb the total hospital cost of patient {patient_id} [time_filter_global1]? | rewritten to stub because mimiciv.cost has zero rows in the current CDM |

### unsupported_external_event_category_mapping (2)

Unsupported by current CDM: intake/output category mapping is external/missing

| benchmark_id | changed | q_tag | summary |
|---|---|---|---|
| `ehrsql_166` | YES | what are_verb the top [n_rank] frequent intake events [time_filter_global1]? | rewritten to stub because MIMIC-IV CDM does not provide a reviewed intake/output category mapping for these EHRSQL item groups |
| `ehrsql_167` | YES | what are_verb the top [n_rank] frequent output events [time_filter_global1]? | rewritten to stub because MIMIC-IV CDM does not provide a reviewed intake/output category mapping for these EHRSQL item groups |

### measurement_age_support_aggregate (1)

Age-stratified lab top-k rewritten to exact age/date support aggregate

| benchmark_id | changed | q_tag | summary |
|---|---|---|---|
| `ehrsql_160` | YES | what are_verb the top [n_rank] frequent lab tests of patients aged [age_group] [time_filter_global1]? | age-stratified top lab tests use mimiciv.schera_measurement_concept_date_age_counts ; concept table join moved after top-k aggregation |

### measurement_event_lateral_rewrite (1)

Event-after lab top-k rewritten to lateral person/date range scans

| benchmark_id | changed | q_tag | summary |
|---|---|---|---|
| `ehrsql_162` | YES | what are_verb the top [n_rank] frequent lab tests that patients had [time_filter_within] after having received a {procedure_name} procedure [time_filter_global1]? | procedure-after lab top-k uses lateral person/date range scan over measurement ; concept table join moved after top-k aggregation ; index event CTE now selects distinct person/date pairs |

### measurement_top_support_aggregate (1)

Frequent lab top-k rewritten to exact measurement date-count support aggregate

| benchmark_id | changed | q_tag | summary |
|---|---|---|---|
| `ehrsql_159` | YES | what are_verb the top [n_rank] frequent lab tests [time_filter_global1]? | top frequent lab tests use mimiciv.schera_measurement_concept_date_counts ; concept table join moved after top-k aggregation |

### normality_range_fix (1)

Normal lab logic rewritten to use range_low/range_high

| benchmark_id | changed | q_tag | summary |
|---|---|---|---|
| `ehrsql_097` | YES | has_verb the {vital_name} of patient {patient_id} been normal [time_filter_global1]? | normal abnormal lab predicate now uses numeric range_low/range_high, avoiding non-portable normal concept id logic |

### percentile_aggregate_rewrite (1)

Percentile query rewritten from window percent_rank to exact aggregate expression

| benchmark_id | changed | q_tag | summary |
|---|---|---|---|
| `ehrsql_018` | YES | what percentile is the value of {lab_value} in a {lab_name} lab test among patients of the same age as patient {patient_id} [time_filter_global1]? | percent_rank window sort was replaced with count(value < target) / nullif(count(*) - 1, 0) |

### unsupported_external_abbreviation_dictionary (1)

Unsupported by current CDM: abbreviation dictionary is external/missing

| benchmark_id | changed | q_tag | summary |
|---|---|---|---|
| `ehrsql_006` | YES | what does {abbreviation} stand for? | rewritten to stub because abbreviation expansion requires an external dictionary |
