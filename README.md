Infant Preference for Sounds: Speech and Laughter

An undergraduate honors thesis project that studies whether young infants prefer to listen to sounds made by other infants, and whether that preference extends from speech-like sounds (babbling) to laughter. The study is built for Children Helping Science (formerly Lookit), an online platform for running developmental research with families from home.

Thesis Information
	
Author	Kendyl Bray

Advisor  Melanie J. Spence, PhD

University of Texas at Dallas

Year	2026

Thesis Paper	Extending the Infant-Talker Bias to Naturalistic Vocalizations: Protophones and Laughter 


Project Overview
Purpose

This project examines how babies pay attention to different voices and sounds during their first year, while they are learning language. Past research has found that babies tend to prefer listening to speech from other infants (sometimes called the Infant Talker Bias). This project tests whether that preference also applies to another form of social communication: laughter.

Understanding which voices and sounds capture an infant's attention can help explain how children learn language in the earliest months of life. Parents also complete short surveys about their child's language development and laughter, which allow us to explore whether more experience producing certain sounds (such as babbling or laughing) relates to the sounds infants prefer to hear.

Study Design
Participants: Infants approximately 6 to 10 months old, participating from home with a parent.
Method: Preferential looking / looking-time paradigm. The parent sits with their back to the screen and holds the baby against their chest, over their shoulder, so the baby can see the screen but the parent cannot. The webcam records the baby's eye movements during the study.
Conditions (between subjects): Each infant is randomly assigned to hear one of two sound types:
Speech sounds (neutral vocalizations such as coos and babbles)
Laughter
Trials (within subjects): Each infant hears 12 short audio recordings (about 10 seconds each), alternating between adult female and infant speakers (6 of each). Which speaker type comes first is counterbalanced across participants.
Main measure: How long the infant looks at the screen during each recording. Longer looking is treated as an indicator of preference. Trained research assistants code the recorded videos.
What the Code Does

This repository contains the study protocol, a JSON file that Children Helping Science uses to build and run the study. It is not a standalone app. The JSON defines a sequence of frames (screens), and the platform handles rendering, recording, and data storage.

Study flow

The sequence in the protocol runs in this order:

#	Frame	Type	What it does
1	study-intro	Text	Welcomes the parent and outlines what will happen.
2	video-config	Webcam setup	Helps the parent set up their webcam and microphone.
3	video-consent	Video consent	Records the parent reading a consent statement (study purpose, procedures, benefits, data use, and rights).
4	questionnaire-instructions	Text	Introduces the three questionnaires.
5	development-survey	Survey	Asks about home language, birth weight, screen exposure, and confirms the parent is 18+.
6	survey-select	Frame selector	Chooses the age-appropriate language survey (see below).
7	laughter-survey	Survey	Asks how often the child laughs, when laughing began, and what makes them laugh.
8	stimuli-preview	Stimuli preview	Optionally lets the parent preview an example audio (without the baby).
9	instructions	Instructions	Study overview, plus an audio test and video test.
10	video-quality	Webcam quality check	Checklist for webcam centering, lighting, and distractions, plus a test recording.
11	baby-webcam-check	Webcam display	Shows the parent how to hold the baby over their shoulder.
12	final-instructions	Text	Final reminders before test trials begin.
13	calibration-video	Calibration	Attention-getter appears center, left, and right to calibrate looking direction.
14	test-trials	Trials (choice frame)	The 12 audio test trials, recorded on webcam.
15	final-calibration-video	Calibration	Repeats the calibration sequence.
16	image-3	Images + audio	Plays the "all done" audio so the parent knows they can turn around.
17	exit-survey	Exit survey	Debriefing, certificate of participation, and data privacy options.
Key logic

Age-based language survey (survey-select). The frame uses a generateProperties function that calculates the child's age in months from their birthday on the platform. Children under 8 months receive the 6 to 8 month language survey; children 8 months and older receive the 9 to 11 month survey. The calculated age is also saved as ageInMonthsAtSurvey.

Random condition assignment and counterbalancing (test-trials). This frame uses the random-parameter-set sampler with four parameter sets:

Parameter set	Odd trials	Even trials	Sound type
1	Adult female	Infant	Laughter
2	Infant	Adult female	Laughter
3	Adult female	Infant	Speech (neutral)
4	Infant	Adult female	Speech (neutral)

Each set contains six audio files per speaker type. The #UNIQ suffix on the placeholders (ODD_TRIAL_SOUNDS#UNIQ, EVEN_TRIAL_SOUNDS#UNIQ) tells the platform to use each file once, so no recording repeats within a participant. Trials alternate odd, even, odd, even for 12 total.

Trial presentation (commonFrameProperties). Every trial shows a looping attention-getter video in the center of the screen while one audio file plays. Trials auto-advance when the audio ends, and webcam recording is on for the entire trial.

Repository Contents
.
├── README.md
└── [your-protocol-file].json    # Study protocol (frames + sequence)

Update the file name above to match your repository. No participant data is stored in this repository.

Stimuli

Audio files and the attention-getter video are hosted in a separate repository from the Infant Learning Project and loaded at runtime through baseDir:

https://github.com/infantlearningproject/Infant-Preference-for-Sounds

File naming follows the pattern Adultfemale_laugh##, Baby_laugh##, Adultfemale_neutral##, and Baby_neutral##.

How to Run the Study
Create or sign in to a researcher account on Children Helping Science and join or create a lab. (Lookit's researcher documentation is at lookit.readthedocs.io.)
Create a new study in your lab.
Under the study's Edit study details / Study type settings, open the Protocol configuration editor.
Copy the contents of the JSON protocol file in this repository into the protocol editor and save.
Preview the study from the researcher interface to test it, including the audio and webcam steps.
Set the age range (approximately 6 to 10 months), submit for approval if required by your lab, and start the study.
Requirements
A Children Helping Science researcher account with permission to create studies
IRB approval for your own use of the study design
An internet connection so stimuli can load from the hosted repository
Data and Privacy
This repository contains no participant data.
All data collected through the platform (survey responses, webcam video, consent video) is stored by Children Helping Science, subject to its privacy policy, and is only accessible to authorized researchers.
The study includes a parent video consent and a data privacy selection at the end of the session.
Anyone reusing this protocol must obtain their own ethics (IRB) approval and update the consent text, PI, institution, and contact information.
Customizing the Protocol

If you adapt this study, the most common edits are:

Consent and contact info: video-consent frame (PIName, institution, PIContact, research_rights_statement)
Support email: video-config frame (troubleshootingIntro)
Stimuli: parameterSets in test-trials and baseDir in commonFrameProperties
Age cutoff for the language survey: the generateProperties function in survey-select
Debriefing text and certificate link: exit-survey frame
Acknowledgments

This study was developed in collaboration with the Infant Learning Project at The University of Texas at Dallas (PI: Melanie J. Spence).

Built on the Lookit / Children Helping Science platform and its experiment-runner frames.


Contact

Kendyl Bray, kendyl.bray@gmail.com
