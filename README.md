# supplementary-rebuttal
Supplementary rebuttal for NDSS'24 Summer #540

## Review #540A ##
**Question:**  
*The following are some additional comments that are not necessarily the weakness of the paper:*

*If attackers incorporate the derived insights from this paper into their attack strategies, it could potentially lead to the generation of more sophisticated adversarial examples (AEs) that are harder to detect. For instance, if the attackers were to take into account the acoustic and linguistic properties that the paper's authors used to distinguish AEs from benign audios, they could potentially generate AEs that mimic these properties of benign audios more closely.*

*The authors may consider adding these properties as constraints in the optimization problem used to generate the AEs. If the attacks can still generate valid AEs under these constraints, it would demonstrate that the attackers can adapt to the proposed detection method, posing a new challenge for adversarial attack detection.*

*Furthermore, it would also be interesting to test the proposed detector on these "natural-looking" AEs. If these AEs are indeed more difficult to detect, it could highlight potential limitations of the proposed detection method and motivate the development of more advanced detection techniques.*

**Answer:**  
Thank you for the suggestion on the application of CACators in attacks. In fact, we tried to use CACators to reduce the number of iterations on generating adversarial examples, but it did not work well. We agree that using CACators to reduce the unnatural-looking adversarial noise is a promising research direction. Studies about this may improve the audibility metrics and challenge existing defense methods. We will consider it as one of our future directions for research and look forward to other researchers' studies after the paper is accepted.


## Review #540C ##
**Question 1:**  
*For instance, it seems that the authors assume rather deep background knowledge of acoustics since they do not provide much info there. Regarding the related work section, I find it rather poor: it is short, and half of it is spent on interpretability, which is nothing bad, but I do not see much on interpretability in the rest of the paper.*

**Answer:**  
We will introduce more information on acoustics in the background section. In the related work, we introduce the interpretability of the adversarial examples because we try to explain the principles of adversarial attack from the perspective of acoustic features, which we think is different from the interpretability in the previous. Thus, we review past work on interpretability.


**Question 2:**  
*Since most existing studies focus on attacking ASR models, we study this type of attack in the paper and introduce how to generate AE in this type. -> please discuss more this design choice*

**Answer:**  
In artificial intelligence, adversarial attacks generally refer to attacks against models, and this type of attack has been studied in several fields, such as audio and image. Among the adversarial attacks against speech recognition, the attacks against models are the primary studies and have various methods, so we take it as the analysis object.

**Question 3:**
*We focus on peaks because we assume the adversarial attack against speech recognition provides primary information on the speech content by the peaks of sound. -> I would assume that the attacker could make an attack such that it avoids this characteristic.*

**Answer:**  
We agree that an attacker can change the shape of the adversarial noise by adding constraints. However, we want to discuss a general situation where the attacker only constrains the audibility of the adversarial noise, as in past works [1-6].

**Question 4:**
I am not sure how to interpret Kendall's coefficient?

**Answer:**  
In statistics, the Kendall's τ coefficient is a metric used to measure the ordinal association between two measured quantities. We use it to evaluate the correlation between properties and adversarial examples/noises [7].

**Question 5:**
*For C&W, Psy, and Imp Attacks, 92%, 100%, and 77% ANs have this property, and 92%, 95%, and 36% AEs have this property. Kendall’s coefficient is 0.891 between low continuity and ANs, and 0.697 between low continuity and AEs. -> please discuss more*

**Answer:**  
The percentage denotes the proportion of adversarial examples (AEs) with adversarial properties to the total number of AEs. Kendall’s τ coefficient evaluates the correlation between properties and AEs/ANs, and a coefficient above 0.5 indicates a positive correlation. The percentages and coefficients of ANs are larger than that of AEs because adversarial attacks generate ANs directly, while the adversarial properties in the AEs may be obscured by benign audio.

**Question 6:**
*over 240Hz, 260Hz, 280Hz, and 300Hz in Fig. 6c. -> why these values?*

*To quantify it, we give the probability of audios with a period of LPC over 2, 3, 4, 5, and 6 in -> why these values?*

**Answer:**  
We chose these values because they can reflect the difference in properties between adversarial audio and benign audio.

**Question 7:**
*Therefore, we speculate the reason for the temporal discontinuity in the adversarial audio is that, given the upper bound of the noise energy, varying the energies of a few time-frequency points allows the audio to approach the optimization target along the gradient. -> requires more discussion*

*As shown in Fig. 7b, we find ANs have more formants, and their formants are lower and narrower compared with that of benign audios. -> discuss more*

**Answer:**  
The adversarial attack requires the perturbation to be as small as possible, so they only change a few values. According to past experimental results, the distribution of these values is usually discrete. For example, in images, the perturbation is several pixels. Similarly, in speech, the AN is some energy that distributes discretely in the time-frequency domain. This is why ANs are temporal discontinuity and have many formants with narrow frequency bands.

**Question 8:**
*Section D. Abnormal Linguistic Pattern of AEs does not discuss Imp Attack. Why?*

**Answer:**  
We do not discuss the Imperception attack because its targeted model Lingvo has no language model, and we do not have access to the linguistic properties of this kind of AEs.

**Question 9:**
audio frame and get a total of 22 features. -> why 22?

**Answer:**  
8 of the 22 features are CACators, selected from 208 acoustic-statistical features, and the adversarial properties represented by them pass the commonality check. The remaining 14 are derived features of 8 CACators and have similar physical meanings as them.

**Question 10:**
*We use a random forest -> why? some info on the machine learning model?*

**Answer:**  
Because random forest can give the weight of each feature, and it is a widely used model for feature ranking.

**Question 11:**
*MFCCs of audios into the classifier directly and is trained with AEs from C&W Attack and a black-box attack [9]. -> so black box? But I thought that the authors in the beginning assume white box?*

**Answer:**  
For defense, generality is a common evaluation metric. Although our study is on white-box attacks, we verify the effectiveness of our AE detector on other unseen models, including a black-box attack.

**Question 12:**
*The CNN-based detector shows poor performance on Imp and GA attacks, indicating limited transferability. -> how is CNN tuned?*

**Answer:**  
The CNN-based detector is the model used for comparison, and we directly used an open-source model trained by two adversarial attacks, which does not require fine-tuning.

[1] Carlini N, Mishra P, Vaidya T, et al. Hidden voice commands[C]//Usenix security symposium. 2016.  
[2] Cisse M M, Adi Y, Neverova N, et al. Houdini: Fooling deep structured visual and speech recognition models with adversarial examples[J]. Advances in neural information processing systems, 2017.  
[3] Iter D, Huang J, Jermann M. Generating adversarial examples for speech recognition[J]. Stanford Technical Report, 2017.  
[4] Schönherr L, Kohls K, Zeiler S, et al. Adversarial attacks against automatic speech recognition systems via psychoacoustic hiding[J]. NDSS, 2018.  
[5] Carlini N, Wagner D. Audio adversarial examples: Targeted attacks on speech-to-text[C]//2018 IEEE security and privacy workshops (SPW). IEEE, 2018.  
[6] Qin Y, Carlini N, Cottrell G, et al. Imperceptible, robust, and targeted adversarial examples for automatic speech recognition[C]//International conference on machine learning. PMLR, 2019. 
[7] Kendall M G. A new measure of rank correlation[J]. Biometrika, 1938, 30(1/2): 81-93
