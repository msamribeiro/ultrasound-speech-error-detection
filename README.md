# Automatic detection of speech articulation errors using ultrasound tongue imaging


#### Speech Error Detection

This repository provides a demo for the set of experiments described in the paper:

Ribeiro, M.S., Cleland, J., Eshky, A., Richmond, K., and Renals. S. (Under Revision)
**Automatic detection of speech articulation errors using ultrasound tongue imaging**
Submitted to Speech Communication.


#### Requirements

Please make sure the following Python libraries and their dependencies are available.

- numpy (1.16.0)
- scikit-image (0.17.2)
- pytorch (1.3.1)

#### Usage

There is some sample data available in `sample_data`. To run the demo, simply type:

`python run_demo.py`

This will run the demo with all default parameters. You can optionally configure them. The example below will evaluate the segment at 4.07 seconds (an alveolar) for velar substitution.

`python run_demo.py --timestamp 4.07 --expected_class alveolar --competing_class velar`

Alternatively, you can test the same segment for velar fronting, which should be identifier as an error.

`python run_demo.py --timestamp 4.07 --expected_class velar --competing_class alveolar`

You can test more utterances using ultrasound and audio. There are plenty available from the [Ultrasuite Repository](https://ultrasuite.github.io/). If you use different, utterances, you will need to generate MFFCs for them.

#### Audio feature extraction 

The audio stream inputs MFCCs. These can be computed using any of the available libraries. We have used Kaldi to generate these features. For the sample utterance in `sample_data`, we provide a set of MFFCs. In the directory `make_mfccs_demo`, there is a example of the steps we used to extract those features. If you wish to run `make_mfccs.sh`, you will need Kaldi installed on your system.

#### Pre-trained model

The pre-trained model parameters available in `models` is the system using both ultrasound and audio and trained on the joint [TaL corpus](https://ultrasuite.github.io/data/tal_corpus/) and [UXTD dataset](https://ultrasuite.github.io/data/uxtd/). This model has 86.90% accuracy when evaluated on Typically Developing Data. See Section 5 of the paper for more details.

#### Accepted classes

The classes that the models allows are the following: 

*alveolar, dental, labial, labiovelar, lateral, palatal, postalveolar, rhotic, velar*. 

You can obtain generic scores for productions of these classes or test for any substitution between them.