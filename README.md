# BEAT19 public data repository

There are two sources of data:

1. Enrollment surveys
2. Daily surveys

Participant enrollment data includes demographics and environment information. 
Daily surveys include changes to environment and symptom assessment.

## Participant privacy

While these data tables have been stripped of protected health information,
by accessing these data you agree not to attempt to de-anonymize participants.

## Table descriptions

### Enrollment data table

Rows in the enrollment table represent distinct participants in the study, and
they are identified by a unique `_id` key.  Missing data are represented as
empty entries (i.e., nothing between the field delimiters. The sections below
describe the fields of this table.

#### `_id`

String variable.

Index for the participant.

#### `age`

Ordered categorical variable. 

Age bin as represented in the survey.

1. 18-20
2. 21-29
3. 30-39
4. 40-49
5. 50-59
6. 60-69
7. 70-79
8. 80-older

#### `gender`

Categorical variable.

* Female
* Male
* Other/Decline to Answer

#### `ethnicity`

Binary variable.

* 1 => Hispanic or Latino
* 0 => Not Hispanic or Latino

#### `race`

Categorical variable.

* American Indian or Alaska Native
* Asian
* Black or African American
* Native Hawaiian/Other Pacific Islander
* White or Caucasian
* Other
* Decline to answer

#### `shelter_in_place`

Binary variable.

"Are you currently in an area with a shelter-in-place recommendation?"

* 1 => Yes
* 0 => No

#### `household_size`

Ordered categorical variable.

Household size, in bins of 1, 2-3, >3

#### `state`

Categorical variable.

Two letter US state abbreviation.

#### `country`

Categorical variable.

Three letter country code.  Currently limited to the United States of America and Brazil.

#### `exposure`

Binary variable.

"Has a doctor prescribed you any medications for your symptoms?"

* True => Yes
* False => No

#### `hcw_setting`

Binary variable.

* 1 => works in any healthcare setting
* 0 => no response to any hcw setting

#### `BMI`

Positive integer variable.

Body mass index computed from height and weight.

#### `health_status`

Ordered categorical variable.

Response to question: "How would you rate your current health?"

1. Well above average
2. Above average
3. Average
3. Below average
4. Well below average

#### `smoker`

Categorical variable.

* "smoked" => "I have never smoked"
* "former" => "I used to smoke"
* "current" => "I currently smoke"
* "ecig" => "I use e-cigarettes or vape"

#### `exercise`

Binary variable.

Response to question: "Do you exercise regularly? (more than 30 min 3x/week)"

* 1 => Yes
* 0 => No

    
### Daily survey data table

Rows in the daily table represent daily survey responses unique to a given day
and individual.

The daily survey has numerous gating questions, answers to which are denoted in
the table as fields containing the substring `_prompt`.  These are always
boolean variables that can be used to obtain rows which contain non-missing
entries.

Symptom questions are typically asked as a Likert scale. Fields labeled as
`*_severity` are thus coded as

* 0 => None
* 1 => Mild
* 2 => Moderate
* 3 => Severe
* 4 => Very severe

Fields labeled as `*_frequency` are coded as

* 0 => Never
* 1 => Rarely
* 2 => Occasionally
* 3 => Frequently
* 4 => Almost constantly

#### `_id`

String variable.

Index for the participant.

#### `rel_date`

Non-negative integer variable.

Relative (to enrollment) date for the daily survey.

#### `ble_travel_prompt`

Boolean variable.

"Did you go to work or school outside the house today?"

* True => yes
* False => no

#### `ble_travel_{bike, bus, car, train, taxi, walk}`

Binary variables.

"If yes, how did you travel?"

Allowed options were

* `bike` => bicycle
* `bus` => bus
* `car` => personal vehicle
* `train` => subway/rail/train
* `taxi` => taxi/rideshare
* `walk` => walking

with values of 

* 1 => checked box for mode of transport
* 0 => did not check box for mode of transport

#### `ble_travel_time`

Ordered categorical variable

"How long were you out of the house?"

* 0 => Did not leave home
* 1 => Less than 15 mins
* 2 => 15-60 mins
* 3 => 1 - 2 hours
* 4 => 2 - 4 hours
* 5 => 4 - 8 hours
* 6 => more than 8 hours

#### `ble_travel_interactions`

Ordered categorical variable.

"With how many people outside your immediate family did you interact with today
inside 6 feet proximity for greater than 15 minutes?"

1. 0 => 0
2. 1 => 1-3
3. 2 => 4-10
4. 3 => 10-20
5. 4 => 20+

#### `ble_sip`

Binary variable.

"Are you in an area under a government mandated
shelter-in-place or stay-at-home recommendation?"

Responses of "I dont know/Not applicable" were coded as missing.

* 1 => Yes
* 0 => No

#### `ble_household_sick`

Binary variable.

"Is anyone in your household sick with known or suspected coronavirus
infection (COVID-19)?"

* 1 => Yes
* 0 => No

#### `ble_physically_feeling`

Ordered categorical variable.

"On a scale from 0 to 10, how are you physically feeling today? 0 is worse (as bad as being dead) 10 is best (perfect health)."

#### `ble_stress`

Ordered categorical variable.

"On a scale from 0 to 10, how are you physically feeling today? 0 is worse (as bad as being dead) 10 is best (perfect health)"

#### `ble_concerned`

Binary variable.

"Are you concerned that you may be getting sick?"

* 1 => Yes
* 0 => No

#### `ble_care_prompt`

Boolean variable

"Have you sought care for COVID-19 related symptoms (cough, shortness of breath and fever)?"

Gating question for care-related follow-up questions.

#### `ble_care_clinic`

Binary variable.

"Did you seek medical attention via in person visit to a clinic or hospital?"

* 1 => Yes
* 0 => No

#### `ble_care_hospitalized`

Binary variable.

"Have you been or are you currently hospitalized for COVID-19 related symptoms?"

* 1 => Yes
* 0 => No

#### `ble_care_telemedicine`

Binary variable.

"Did you seek medical attention via a phone or video call (telemedicine) service?"

#### `ble_care_flu_prompt`

Boolean variable.

"Did you have a rapid flu test?"

* True => Yes
* False => No

#### `ble_care_flu_result`

Binary variable.

"What was the result of the flu test?"

Responses of "Awaiting results" were coded as missing.

* 1 => Positive
* 0 => Negative

#### `ble_care_covid_prompt`

Boolean variable.

"Did you have a COVID-19 test?"

* True => Yes
* False => No

#### `ble_care_covid_result`

Binary variable.

"What was the result of the COVID-19 test?"

Responses of "Awaiting results" were coded as missing.

* 1 => Positive
* 0 => Negative

#### `ble_care_covid_rel_date`

Integer variable.

"When did you complete the COVID-19 Test?"

This is the day, relative to participant enrollment date, that the participant
completed the COVID test.

#### `ble_care_covid_recovered`

Binary variable.

"Have you fully recovered from your COVID-19 symptoms?"

* 1 => Yes
* 0 => No/not applicable

#### `sym_prompt`

Boolean variable.

"In the last 24 hours, have you had any changes to your SYMPTOMS?"

Gating question for fields labeled `sym_*`.

#### `sym_ent_prompt`

Boolean variable.

"In the last 24 hours, have you had any problems associated with your head,
eyes, ears, nose or throat like HEADACHE, LOSS OF TASTE OR SMELL, SORE THROAT,
RUNNY or STUFFY NOSE and/or ITCHY or GRITTY EYES?"

* True => Yes
* False => No

#### `sym_ent_headache_severity`

Likert scale variable.

"What was SEVERITY of your HEADACHE at its worst?"

#### `sym_ent_smell_severity`

Likert scale variable.

"What was the SEVERITY of your LOSS OF TASTE or SMELL?"

#### `sym_ent_sore_severity`

Likert scale variable.

"What was the SEVERITY of your SORE THROAT at its worst?"

#### `sym_ent_runny_severity`

Likert scale variable.

"What was the SEVERITY of your RUNNY NOSE at its worst?"

#### `sym_ent_stuffy_severity`

Likert scale variable.

"What was the SEVERITY of your STUFFY NOSE at its worst?"

#### `sym_ent_itchy_severity`

Likert scale variable.

"What was the SEVERITY of your ITCHY or GRITTY EYES at its worst?"

#### `sym_ent_watery_severity`

Likert scale variable.

"What was the SEVERITY of your WATERY EYES at its worst?"

#### `sym_ent_dizzy_severity`

Likert scale variable.

"What was the SEVERITY of your DIZZINESS/VERTIGO at its worst?"

#### `sym_ent_dizzy_frequency`

Likert scale variable.

"How OFTEN did you have DIZZINESS/VERTIGO?"

#### `sym_git_prompt`

Boolean variable.

"In the last 24 hours, have you had any problems with your stomach, like NAUSEA, VOMITING or DIARRHEA?"

* True => Yes
* False => No

#### `sym_git_nausea_frequency`

Likert scale variable.

"How OFTEN did you have NAUSEA?"

#### `sym_git_nausea_severity`

Likert scale variable.

"What was the SEVERITY of your NAUSEA at its worst?"

#### `sym_git_vomiting_frequency`

Likert scale variable.

"How OFTEN did you have VOMITING?"

#### `sym_git_vomiting_severity`

Likert scale variable.

"What was the SEVERITY of your VOMITING at its worst?"

#### `sym_git_diarrhea_frequency`

Likert scale variable.

"How OFTEN did you have LOOSE OR WATERY STOOLS (DIARRHEA)?"


#### `sym_resp_prompt`

Boolean variable.

"In the last 24 hours, have you had any problems with your chest or lungs like COUGH, WHEEZING, SNEEZING or SHORTNESS of BREATH?"

* True => Yes
* False => No

#### `sym_resp_wheezing_severity`

Likert scale variable.

"What was the SEVERITY of your WHEEZING at its worst?"

#### `sym_resp_sneezing_severity`

Likert scale variable.

"What was the SEVERITY of your SNEEZING at its worst?"

#### `sym_resp_coughing_severity`

Likert scale variable.

"What was the SEVERITY of your COUGH at its worst?"
#### `sym_resp_wetdry`

Binary variable.

"Was your cough WET or DRY?"

Responses of "Not applicable" were coded as missing.

#### `sym_resp_wet`

Binary variable.

Responded WET to "Was your cough WET or DRY?"

#### `sym_resp_dry`

Binary variable.

Responded DRY to "Was your cough WET or DRY?"

#### `sym_resp_bloody`

Binary variable.

"When you cough, have you noticed RED or BLOODY phlegm?"

* 1 => Yes
* 0 => No

#### `sym_resp_dyspnea_severity`

Likert scale variable.

"What was the SEVERITY of your SHORTNESS OF BREATH at its worst?"

#### `sym_fever_prompt`

Boolean variable.

"In the last 24 hours, have you had any problems like FEVER, CHILLS, BODY ACHES, FATIGUE or TIREDNESS?"

* True => Yes
* False => No

#### `sym_fever_temp_prompt`

Boolean variable.

"Have you had a fever?"

* True => Yes
* False => No

#### `sym_fever_temp`

Likert scale variable.

"What was your temperature at its highest?"

* 0 => Normal/No Fever
* 1 => Mild (38.0-38.4C)(100.4-101.1F)
* 2 => Moderate (38.5-38.9C)(101.2-102.0F)
* 3 => Severe (39.0-40C)(102.1-104F)
* 4 => Very Severe (>40C)(>104F)

#### `sym_fever_chills_frequency`

Likert scale variable.

"How OFTEN did you have CHILLS?"

#### `sym_fever_chills_severity`

Likert scale variable.

"What was the SEVERITY of your CHILLS at its worst?"

#### `sym_fever_aches_severity`

Likert scale variable.

"What was the SEVERITY of your BODY ACHES at its worst?"

#### `sym_fever_fatigue_severity`

Likert scale variable.

"What was the SEVERITY of your FATIGUE, TIREDNESS, OR LACK OF ENERGY at its worst?"

#### `sym_fever_sleeping_severity`

Likert scale variable.

"What was the SEVERITY of your PROBLEMS SLEEPING at its worst?"
