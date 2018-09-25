---
layout: "post"
author: "Katherine Tian (‘19)"
print_publication: true
tags: issue2
categories: Perspectives
related_image: /imgs/tian-figure1.jpg
---

*Artificial intelligence can improve doctors’ diagnostic and predictive ability, but its use in medicine faces considerable challenges.*

<!--excerpt-->

| ![](/imgs/tian-figure1.jpg) | 
|:--:| 
|Surgeons remove tissue from a patient’s breast in order to perform a biopsy to determine the nature of a tumor. Artificial intelligence algorithms can determine whether a digitized biopsy slide contains cancerous or healthy cells nearly to the level of human professionals, a 2017 study shows. (Image Credit: National Cancer Institute)|

As early as the 1950s, scientists began researching artificial intelligence or AI, starting with creating the perceptron and nearest neighbor algorithm. Suddenly, in the past few years, the field of artificial intelligence has seen meteoric progress for three main reasons: (1) the recent increase in computing power and GPU acceleration with reduced costs; (2) the availability of massive reserves of training data thanks to the rise of internet; and (3) breakthroughs in AI algorithms, in particular deep neural networks.

With these advancements, AI is poised to revolutionize many industries, including healthcare. Because of its superhuman ability to identify patterns in digital data, artificial intelligence will be able to rapidly improve patient diagnostics, health predictions, and precision medicine techniques.

In the field of cancer diagnostics, researchers from the Beth Israel Deaconess Medical Center at Harvard Medical School led by Professor Andrew Beck, now the founder and CEO of PathAI, have developed a deep learning-based method to help automate diagnoses. Traditionally, the diagnosis process requires that a slide be prepared from a biopsy so that a highly trained pathologist can examine the cells in the tissue sample under a microscope, coming to a decision about whether a diagnosis can be made. However, when these histopathological slides are scanned and digitized to create whole slide images, artificial intelligence algorithms can analyze the series of pixels in these images to determine whether the tissue sample contains cancerous cells or healthy cells.

Using millions of training image patches to train a deep convolutional neural network, Dr. Beck’s team produced an artificial intelligence framework that could discriminate tumor patches from normal patches. Their system achieved accuracy of 92% AUC (Area Under the Curve), nearly as good as the 96% accuracy AUC achieved by human pathologists at the time the research was published (Beck et al., 2017).

Since artificial intelligence algorithms are able to identify associations in data too subtle or complex for the human eye to catch, the team has since been able to improve their algorithm further to now surpass human performance in diagnostic accuracy.

Related research based on other types of data, including radiology images, molecular data, and clinical information, is also underway. Combining all the information doctors possess with a superhuman capacity for pattern recognition, artificial intelligence algorithms have the potential to make comprehensive diagnoses more quickly and accurately than a team of specialists.

At the University of Nottingham in the UK, a team of epidemiologists used machine-learning algorithms to correlate medical history with rates of heart attacks. Training their random forest, logistic regression, gradient boosting, and neural network algorithms on hospital data from 295,000 patients and then testing the algorithm predictions on data from another 82,000 patients, the scientists compared their results to predictions based on the current best practice, the American College of Cardiology / American Heart Association (ACC/AHA) guidelines, which are based on eight risk factors including the patient’s age, cholesterol level, and blood pressure.

Amazingly, the AI algorithms not only performed better than the ACC/AHA best practices in predicting the occurrence of heart attacks but also identified novel contributing factors not yet included in ACC/AHA guidelines, such as severe mental illness and taking oral corticosteroids (Weng et al., 2017). Early prediction can prevent heart attacks and save lives, and artificial intelligence can play an important role in helping doctors predict patients’ conditions more accurately using an improved set of biomarkers.

Precision medicine, as defined by National Institutes of Health, is “an emerging approach for disease treatment and prevention that takes into account individual variability in genes, environment and lifestyle for each person.” As the human genome contains around 19,000 to 20,000 coding genes and over 3 billion base pairs, the complexity of the work required to implement precision medicine is enormous and can only be realized with heavy utilization of AI to help predict which medicine will work the best for a given individual.

A team of researchers from the University of Washington has recently developed a machine learning algorithm to identify precision medicine for patients with acute myeloid leukemia. Their algorithm has identified that high SMARCA4 gene expression could be a biomarker for patient sensitivity to Mitoxantrone, a drug commonly used for treatment of AML; patients with low SMARCA4 expression should use alternative treatments (Lee et al., 2018).

However, progress towards the adoption of AI in the medical industry is hindered by challenges including the lack of accurately labeled data for training the AI algorithms, as the quality and quantity of training data will directly impact the AI algorithms’ performance. In many cases, doctors or trained professionals need to review and annotate data manually to assign proper labels. This can be a very expensive and time-consuming process, making it difficult to obtain large amounts of quality training data, which artificial intelligence algorithms depend upon.

Another challenge is lack of standardization of data. In many cases, a large data set is collected from many different organizations that use different equipment and follow different procedures to prepare the data, noise in the data may throw off AI algorithms. In addition, because deep learning algorithms may use millions of parameters to make advanced classifications, humans will not be able to fully understand how they work. Lack of interpretability may cause doctors to be hesitant to adopt AI in medicine.

As scientists surely work to overcome these challenges, AI’s impact on the healthcare industry will be major. In parts of the world that face a shortage of trained healthcare professionals, artificial intelligence algorithms can provide affordable, accessible health expertise to everyone. Furthermore, AI can assist doctors and other healthcare professionals to provide higher quality of care. AI can help physicians make more accurate diagnoses and predictions, find new personalized treatments, and organize patients’ information better such that doctors can spend more of their valuable time addressing patients’ concerns personally rather than relying on human diagnostic skills.

