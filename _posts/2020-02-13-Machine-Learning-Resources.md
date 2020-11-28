*I am currently working on audio/speech processing, TTS etc., so...*

### Deep Learning in Speech resources:
* Understanding sound/audio:
	* @[radekosmulski](https://twitter.com/radekosmulski) - [A great starting point](https://github.com/earthspecies/from_zero_to_DSP/), also usable in Google Colab.
	* [Very good intro to audio](https://github.com/mogwai/fastai_audio/blob/master/tutorials/01_Intro_to_Audio.ipynb/).
	* [Progress tracker](https://github.com/sebastianruder/NLP-progress) in NLP by @[seb_ruder](https://twitter.com/seb_ruder)
	* [Everything you should know about sound](https://waitbutwhy.com/2016/03/sound.html)

* Generation/Synthesis of new sounds based on training set (**[copied from](https://github.com/drscotthawley/drscotthawley.github.io/blob/master/_posts/2017-2-6-Machine-Learning-Reference-List.md)**):

    * Jake Fiala: "Deep Learning and Sound" <http://fiala.uk/notes/deep-learning-and-sound-01-intro>
    * GRUV: <https://github.com/MattVitelli/GRUV>.  Btw, found that LSTM worked better than GRU.
    * John Glover: <http://www.johnglover.net/blog/generating-sound-with-rnns.html>  Glover used LSTM fed by phase vocoder (really just STFT).
    * Google Magenta for MIDI: <https://magenta.tensorflow.org/welcome-to-magenta>
    * Google WaveNet for Audio... <https://deepmind.com/blog/wavenet-generative-model-raw-audio/>
        * WaveNet is slow.   "Fast Wavenet": <https://github.com/tomlepaine/fast-wavenet>
        * WaveNet in Keras: <https://github.com/basveeling/wavenet>

* Neural voice cloning with few samples implementations (to be added):
	* Transfer Learning from Speaker Verification to Multispeaker Text-To-Speech Synthesis - [paper](https://arxiv.org/abs/1806.04558)
		* [Github implementation](https://github.com/CorentinJ/Real-Time-Voice-Cloning)
	* Neural Voice Cloning with a Few Samples - [paper](https://arxiv.org/abs/1802.06006)
		* [Github implementation](https://github.com/Sharad24/Neural-Voice-Cloning-with-Few-Samples)
	* DeepVoice3 - [paper](https://arxiv.org/abs/1710.07654)
	* Wavenet - [blog](https://deepmind.com/blog/article/wavenet-generative-model-raw-audio)

* Text-to-speech implementations (to be added):
	* Tacotron2 - [paper](https://arxiv.org/abs/1712.05884)
	* DCTTS - [paper](https://arxiv.org/pdf/1901.04276.pdf)

### [**Deep Learning cheatsheet**](https://github.com/rusty1s/deep-learning-cheatsheet) by @[rusty1s](https://twitter.com/rusty1s).

### Resources by @[thom_wolf](https://twitter.com/Thom_Wolf).

*My self-educational approach is usually to get a few rather exhaustive books and read them for cover to cover.*
* Here is my reading list to join the NLP/AI/ML field.
	* [The "Deep Learning" Book](https://www.deeplearningbook.org/) by Ian Goodfellow, Yoshua Bengio and Aaron Courville is a good ressource to get a quick overview of the current tools.
	* ["Artificial Intelligence: A Modern Approach"](http://aima.cs.berkeley.edu/) by Stuart Russell and Peter Norvig is a great ressource for all pre-neural-network tools and methods.
	* ["Machine Learning: A Probabilistic Perspective"](https://www.cs.ubc.ca/~murphyk/MLbook/) by Kevin P. Murphy is a great ressource to go deeper in the probabilistic approach and get a good exposure to Bayesian tools.
	* ["Information Theory, Inference and Learning Algorithms"](http://www.inference.org.uk/mackay/itila/book.html) by David MacKay is a little gem that explain propabilities and Information theory so clearly it's almost unbelievable.
	* **"The Book of Why: The New Science of Cause and Effect"** by Pearl, Judea is a good introduction to Causality (more accessible than the big "Causality: Models, Reasoning and Inference")
	* ["Reinforcement Learning: An Introduction"](http://incompleteideas.net/book/the-book.html) by Richard S. Sutton and Andrew G. Barto is a great ressource to get an introductory exposure to Reinforcement Learning
* Natural Language Processing: three great ressources I've read with interest:
	* [Kyunghyun Cho's lecture notes](https://github.com/nyu-dl/NLP_DL_Lecture_Note/blob/master/lecture_note.pdf) on "Natural Language Processing with Representation Learning" are great.
	* [Yoav Goldberg's book on "Neural Network Methods in Natural Language Processing"](https://www.amazon.com/Language-Processing-Synthesis-Lectures-Technologies/dp/1627052984) is nice too (see also an older free version [here](https://arxiv.org/abs/1510.00726)).
	* [Jacob Eisenstein's textbook on "Natural Language Processing"](https://github.com/jacobeisenstein/gt-nlp-class/blob/master/notes/eisenstein-nlp-notes.pdf) is also a very exhaustive read.

* It's also good to complement this with a few online courses depending on what field you feel you should be diving deeper into.
I took the following classes:
	* [Computational Probability and Inference (6.008.1x)](https://courses.edx.org/courses/course-v1:MITx+6.008.1x+3T2016/course/) from edx.
	* [Probabilistic Graphical Models Specialization](https://www.coursera.org/specializations/probabilistic-graphical-models) from coursera.
