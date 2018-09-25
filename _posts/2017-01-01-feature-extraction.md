---
layout: "post"
title: "Using Feature Extraction for Automated Scoring of HER2 Immunohistochemistry Images"
categories: Articles
issue_number: 1
tags: issue1
print_publication: true
author: "Steven Cao, Neymika Jain"
---

<!--excerpt-->

<ul class="nav nav-tabs" id="tabs" role="tablist">
  <li class="nav-item">
    <a class="nav-link active" id="home-tab" data-toggle="tab" href="#home" role="tab" aria-controls="home" aria-selected="true">Summary</a>
  </li>
  <li class="nav-item">
    <a class="nav-link" id="profile-tab" data-toggle="tab" href="#profile" role="tab" aria-controls="profile" aria-selected="false">Full Text</a>
  </li>
</ul>
<div class="tab-content" id="tabsContent">
  <div class="tab-pane fade show active" id="home" role="tabpanel" aria-labelledby="home-tab">Immunohistochemistry, which consists of using antibodies to stain tissue slides, helps pathologists determine expression of HER2 in breast cancer tumors, which is important for prognosis and treatment. Currently, most assessment of HER2 slides is done manually, with pathologists scoring slides as {0}, {1+}, {2+}, or {3+} based on the extent of staining. However, manual scoring is time-consuming and inconsistent, creating the motivation for an automated scorer. In our method, first, tissue segmentation and color separation were done on images. Next, proportion of tissue stained, mean stain intensity, Haralick texture features, and connectivity features were collected and used to train a lasso-regularized generalized linear model with a pathologist’s scoring as the gold standard. The model performed well in categorized and binarized scoring (kappa = 0.9573 and 0.9881), with higher accuracy than the existing Ariol and Chang et al. methods. It also outperformed a second pathologist in categorized scoring, suggesting that it could mimic the first pathologist’s scoring tendencies. Finally, it was tested in {0} versus {1+} scoring, a currently unexplored but clinically significant problem, and had high agreement with pathologists (kappa = 0.8074) despite potential ambiguity in separating the two groups. Thus, the model’s methods are an improvement in automated scoring.</div>
  <div class="tab-pane fade" id="profile" role="tabpanel" aria-labelledby="profile-tab" markdown="1">
  
## 1. Introduction

### 1.1 Motivation: Transition of IHC from Manual to Automated Scoring

Expression of HER2, a gene that regulates breast cancer development, is influential in breast cancer prognosis and treatment [1]. Pathologists use immunohistochemistry (IHC), the use of stains and antibodies that bind to tissue cell antigens, to determine HER2 expression level, with the blue Hematoxylin stain binding to nuclei and the brown 3,3’-Diaminobenzidine (DAB) stain binding to antibodies that bind to HER2 proteins [2]. Currently, most slides are scored manually based on the extent of DAB staining [3]. However, manual scoring is time-consuming and variable due to issues with staining and inherent human inconsistency [3, 4]. Thus, quantitative pathology in IHC is beneficial because it uses semi-automated or fully automated algorithms to reduce scoring variability as well as save time and resources [4].

### 1.2 Current Scoring Systems and Automated Implementations

Based on recommendations by the American Society of Clinical Oncology, HER2 images are categorized into four groups [5]. The negative scores, {0} and {1+}, are given to slides with no staining or weak staining, respectively [5]. The positive score, {2+}, is given to slides with either complete, weak membrane staining in greater than 10% of tumor cells, or to slides with intense membrane staining in less than 30% of tumor cells [5]. Finally, the strong positive score, {3+}, is given to slides with intense membrane staining in over 30% of tumor cells [5].

Current attempts at automated scoring use pixel-based algorithms to calculate area and intensity of staining, nuclear algorithms to find the counts of stained and unstained nuclei, and membrane algorithms to find completeness of membrane staining [4, 8-9]. However, these attempts still fall short of manual scoring. In one study, for categorized ({0, 1+} versus {2+} versus {3+}) scoring, Cohen’s kappa, a measure of true agreement with values between 0 and 1, between the Ariol automated systems and pathologists ranged from 0.698 to 0.837, falling below the inter-pathologist agreement of 0.929 [6]. Similarly, for binarized ({0, 1+} versus {3+}) scoring, the kappa of 0.898 between Ariol systems and pathologists fell below that of 1.000 between pathologists [6]. Furthermore, current automated scorers do not attempt to differentiate between {0} and {1+} scores, despite the separation’s clinical significance in gene expression and treatment [6, 8, 10-11]. Thus, given the limitations of currently available scoring methods, there was motivation to provide a more accurate automated scorer.

## 2. Materials and Methods

### 2.1 Dataset

The dataset is publicly available and was obtained using the Genetic Pathology Evaluation Centre (GPEC) TMA Viewer [6]. It includes 4,046 invasive breast carcinoma cases from the British Columbia Cancer Agency arranged into 17 tissue microarray (TMA) blocks [6]. During preparation, slides were incubated with the anti-HER2/neu antibody, stained with DAB, counterstained with Hematoxylin, and then digitized with the Ariol scoring system’s Olympus microscope at 20× magnification [6]. Manual scores for the images were taken from the paper of Turashvili et al., 2009, which assessed inter-observer HER2 scoring variability [6]. The paper excluded slides with no tissue or with tissue that was cut through [6]. The remaining slides were scored independently by two pathologists, with only the first pathologist’s scoring included in the GPEC viewer [6]. Of the remaining 3,639 images, 2,928 were scored as {0}, 245 were scored as {1+}, 130 were scored as {2+}, and the remaining 336 were scored as {3+} [6].

### 2.2 Preprocessing

#### 2.2.1 Tissue and Color Segmentation

First, masks were created to separate images into tissue and background, and then into blue (Hematoxylin) and brown (DAB) stained tissue. Tissue segmentation was done instead of nuclear segmentation because of the difficulty of accurate nuclear segmentation in histopathology due to nuclear shape irregularity [13]. Each image was first converted from RGB (red, green, blue) to grayscale using the intensity values from the image’s HSI (hue, saturation, intensity) transformation [15]. After contrast of the grayscale image was increased, two thresholds were chosen using Otsu’s method, which maximized the variance between the three classes of pixels, for hysteresis thresholding to create a tissue mask [16]. For color separation, a binary transformation with a level of 0.5 was done on the tissue’s hue values, dividing the tissue into blue and brown.

#### 2.2.2 Stain Unmixing

A second method was used to unmix the Hematoxylin and DAB stains and create a Hema&DAB color space, allowing each stain to be assessed separately. The algorithm, as described in Ruifrok and Johnston, determined the contribution of each stain to the R, G, and B values of the image based on the stains’ RGB absorption values [17]. The RGB absorption values used were [0.644, 0.717, 0.267] for Hematoxylin and [0.268, 0.570, 0.776] for DAB.

### 2.3 Feature Collection

After segmentation, three sets of quantitative features, 1) size and intensity, 2) Haralick texture features, and 3) connectivity features, were collected on images to quantify the amount of staining in each.

#### 2.3.1 First Feature Set

The first feature set, which quantified stain size and intensity, used the tissue segmentation and the value (V) color channel to find the proportion of tissue stained brown and the average intensity of staining. This feature set was included because size and intensity were included in manual HER2 scoring recommendations and also briefly described in a topic review [4, 5, 9]. To find the fraction of the tissue that was stained brown, the pixel count of the brown tissue was divided by the total tissue pixel count. To find staining intensity, the image was converted from the RGB to the HSV (hue, saturation, value) color space, and the mean of the V values of the brown tissue was calculated to represent the average intensity of each pixel. The feature set’s third feature was the product of the first two features.

#### 2.3.2 Second Feature Set

The second feature set, features 4 to 120, was comprised of the Haralick features, which quantified image texture. This feature set was included because it worked well in testing, improving categorized scoring agreement with pathologists from 0.9338 to 0.9573. Thirteen Haralick features—the Angular Second Moment, Contrast, Correlation, Sum of Squares, Inverse Difference Moment, Sum Average, Sum Variance, Sum Entropy, Entropy, Difference Variance, Difference Entropy, and 1st and 2nd Information Measures of Correlation—were collected on nine different Gray-Level Co-Occurrence Matrices (GLCMs) [18, 19, 20]. The first three GLCMs were created from the grayscale images for the total tissue, blue tissue, and brown tissue.

The next four matrices were created from the hue and saturation color channels for the total tissue and brown tissue. The last two matrices were created from the unmixed Hematoxylin and DAB stains.

The Haralick features were collected on multiple color channels because each channel contained unique information about the image. The features from the color channels were not highly correlated with each other, and each color channel was represented in the features selected by the model (Table 1).

#### 2.3.3 Third Feature Set

The last feature set, features 121 to 124, quantified the connectivity of the brown tissue. This set was included because completeness of staining was another characteristic described in manual scoring guidelines [5]. First, to transform the brown tissue mask to skeleton, pixels were removed from the edges of objects while keeping the objects intact until they were each one pixel wide [21]. Using this transformation, the mean and maximum pixel counts and the mean and minimum Euler numbers were collected on each skeleton object. The Euler number, the number of objects in a region minus the number of holes, was collected on each object separately, so it counted the number of holes in each [22]. These features were used to quantify connectivity because membranes that were more connected tended to be large and have many holes.

### 2.4 Machine Learning

Using R’s glmnet package [23], a lasso-regularized generalized linear model (GLM) was trained to classify images using manual scoring as the gold standard. In binary classification, the model used gradient descent to find the coefficients for a decision value function consisting of a linear combination of features [23]. The decision value for an image represented where it fell between the two categories, and 0 was used as the separating threshold, making negative values one category and positive values the other [23]. Because not all the features would be useful for the model, lasso regularization was used to limit the size of the coefficients of features and set some to 0, reducing overfitting [24]. Lasso’s penalty parameter, lambda, which determines the extent of coefficient limitation, was chosen through 10-fold cross-validation on the training set [23, 24]. A one-versus-all approach was used for multi-class problems, so separate models were created for each class, and the class with the highest decision value was chosen [23].

### 2.5 Assessment of the Model

#### 2.5.1 The Three Scoring Tasks

The model was tested with Turashvili et al.’s dataset described in Section 2.1. Turashvili et al.’s paper used this dataset to assess agreement between two Ariol automated scoring systems and two pathologists’ manual scoring, allowing our model to be compared to the Ariol systems and the second pathologist [6]. Because only the first pathologist’s scores were included in the GPEC viewer, we used the better Ariol system’s agreement with the first pathologist for comparison.

Turashvili et al. assessed inter-observer variability on two problems, categorized scoring ({0, 1+} versus {2+} versus {3+}) and binarized scoring ({0, 1+} versus {3+}) [6]. However, the paper did not explore the {0} versus {1+} scoring task, which is a problem that is generally unexplored despite being clinically important [6, 8, 10, 11]. This paper assesses our model’s accuracy for the three aforementioned scoring tasks.

Similarly to Turashvili et al.’s paper, weighted kappa with squared weights was used as the measure of agreement, and 95% confidence intervals were created through bootstrapping with 1000 repetitions using the bias-corrected and accelerated method [6, 25, 26]. To determine whether the model’s predictions were significantly better than random guessing, one-sided, one-proportion z-tests were done for the null hypothesis that the accuracy was equal to the no information rate, and an alpha of 0.01 was used to determine significance [27].

#### 2.5.2 Dividing the dataset

The dataset was divided into training and test sets using R’s random sampling and a seed of 123, with 75% of the data put into the training set and the other 25% into the test set. For testing on {0} versus {1+} scoring, because the dataset had about ten times as many score {0} as score {1+} images [6], random sampling was done again with the same seed in order to include only 10% of the score {0} images, evening out the prevalences of each score. Because this process was not done in Turashvili et al.’s paper [6], uneven data were used for comparisons with Ariol in categorized and binarized scoring. However, to test the hypothesis that evening out data would lead to better scoring results, a second set of testing for categorized scoring with evened-out data was done as well.

#### 2.5.3 Replicating Chang et al.’s Method

Another existing method, Chang et al., 2012 [28], was replicated using the paper’s descriptions so that it could be tested on Turashvili et al.’s dataset and also provide a point of reference in the otherwise unexplored {0} versus {1+} scoring task. Chang et al.’s method was chosen for replication because it was presented in a paper and thus had descriptions of methods. Most existing automated scorers were commercial, meaning that they did not have detailed descriptions available and thus could not be replicated. The actual code from Chang et al.’s paper could not be obtained, so its methods were replicated to the best of our abilities.

Chang et al.’s method collected the Haralick texture features for the R, G, and B color channels, the grayscale color channel, and the H, S, and I color channels [28]. It then trained a tree-based multiclass Support Vector Machine (SVM) with features selected by Sequential Forward Floating Selection (SFFS) [28]. To classify test images, it used a tile voting system in which it divided images into square tiles, classified each tile, and then chose the score that had the most votes [28].

However, because Turashvili et al.’s dataset contained TMAs, as opposed to the paper’s dataset, which contained homogeneous regions of interest selected by pathologists, modifications needed to be made to accommodate the tiling method (Figures 1 and 6) [6, 28]. Many of the TMAs scored as {3+} had intense staining in around 40% of tissue and no staining in the other 60%, causing them to be incorrectly scored as {0} using tiling. Thus, to modify Chang et al.’s method for Turashvili et al.’s dataset, features were collected on only the brown-stained areas of images or on the blue-stained areas of images without brown staining, creating regions that could be used for tiling. Images were segmented into stain and non-stain using disk-shaped dilation on the brown tissue mask (Figure 8). To replicate the article’s feature selection, the dprep package’s “sffs” method was modified to use SVM classifiers [29]. The accuracy for fully split scoring ({0} versus {1+} versus {2+} versus {3+}) was compared to the accuracy reported in the paper, 0.9069, to assess the closeness of the replication [28]. Chang et al.’s method was tested on blocks A-D of Turashvili et al.’s dataset.

## 3. Results

### 3.1 Statistical Tests for Accuracy and No Information Rate

In all three scoring tasks, tests for our method and Chang et al.’s method produced p-values smaller than the alpha of 0.01, with the largest p-value being 0.00145, indicating that both models’ predictions were significantly better than random guessing.

### 3.2 Categorized Scoring ({0, 1+} versus {2+} versus {3+})

Both the Ariol method and Chang et al.’s method had high agreement with the first pathologist (kappa = 0.835, 95% CI: 0.81-0.862; kappa = 0.8058, 95% CI: 0.6546-0.9028), and the second pathologist had very high agreement with the first (kappa = 0.929, 95% CI: 0.909-0.949) [6]. In comparison to all three, our method had significantly higher agreement (kappa = 0.9573, 95% CI: 0.9323-0.9728), falling above all three 95% confidence intervals.


The first confusion matrix, which displays how our predictions compared with manual scoring, shows high agreement for {0, 1+} images and {3+} images (balanced accuracy = 0.9676, 0.9540) but lower agreement for {2+} images (balanced accuracy = 0.7756).

Because the original dataset had more {0, 1+} images than {2+} or {3+} images, our method was also tested after score prevalences had been evened out using random sampling, and it achieved higher balanced accuracy for score {2+} images, increasing from 0.7756 to 0.9431. A one-sided, two-proportion z-test with the null hypothesis that sensitivity for {2+} images was equal for both even and uneven datasets yielded a p-value of 0.00144, which is below the alpha of 0.01, meaning that the change in scoring accuracy for {2+} images was significant.

### 3.3 Binary Scoring ({0, 1+} versus {3+})

The Ariol method had high agreement with the first pathologist (kappa = 0.898, 95% CI: 0.775-0.979) [6], while Chang et al.’s method had very high agreement (kappa = 0.9260, 95% CI: 0.7937-0.9787). In comparison with both methods, our method had significantly higher agreement with the first pathologist (kappa= 0.9881, 95% CI: 0.9485-1), falling above both confidence intervals. However, it fell below the perfect inter-pathologist agreement (kappa = 1.000, 95% CI: 1.000-1.000).

Our method’s confusion matrix shows only two images scored incorrectly by our method, both {0, 1+} images predicted as {3+}. The two images are shown below (Figure 12).

The first image had close to no tissue on the slide but was not discarded, and the second image included part of the brown-stained neighboring tissue in the frame (Figure 12). These anomalies are possible reasons why the method scored them incorrectly. The empty core should have been discarded in Turashvili et al.’s paper like the other unsatisfactory cores were, but it was scored as 0 instead X [6].

## 3.4 {0} versus {1+} Scoring

Chang et al.’s method had low agreement with the first pathologist (kappa = 0.3416, 95% CI: 0.1922-0.5178), while our method had high agreement (kappa= 0.8074, 95% CI: 0.6884-0.8957), falling above Chang et al.’s method’s 95% confidence interval.

Our method’s confusion matrix shows similar accuracy for {0} and {1+} images, with six {0} images and seven {1+} images scored incorrectly (Figure 14). Examples of the incorrectly scored images are shown below (Figure 15).

Figure 15 shows examples of images that were scored incorrectly by our method. The incorrectly scored images for both scores had light staining and were similar to each other. In addition, the model outputted decision values closer to the threshold, 0, for incorrectly scored images than for correctly scored images, with the mean of the absolute values of the decision values being 0.422 for incorrectly scored images compared to 1.750 for correctly scored images (Figure 16). These images and their small decision values suggest some ambiguity in separating the two categories.

## 3.5 Assessing the Replication

Chang et al.’s method achieved 0.7308 accuracy for {0} versus {1+} versus {2+} versus {3+} scoring, which fell short of the paper’s reported 0.9069 for the same scoring task [28].

## 4. Discussion

### 4.1 Categorized and Binarized Scoring

#### 4.1.1 Agreement with Pathologists

For categorized scoring, while both Ariol and Chang et al.’s method fell short of manual scoring, our method outperformed the second pathologist with its higher agreement with the first pathologist, falling above the second pathologist’s 95% CI (0.909-0.946) with a kappa of 0.9573 (Figure 8). The fact that it outperformed the second pathologist suggests that the features collected by the model can describe an image well enough that it can imitate the first pathologist’s scoring tendencies. This high agreement also suggests a large improvement from current automated methods. However, our model also had a lower balanced accuracy for {2+} images, 0.7756, than for {0, 1+} or {3+} images (Figure 9) [6]. This difference was likely due to the lower prevalence of {2+} scores compared to the other two categories, as balanced accuracy increased to 0.9431 when score prevalences were evened out (Figure 9).

For binarized scoring, our method outperformed both automated methods but fell short of the perfect agreement between the two pathologists (Figure 10). However, although our method incorrectly scored two images, both images had been prepared imperfectly, and the first image had been left in the dataset despite its lack of tissue (Figure 12) [6]. Although problems of unsatisfactory images would not be issues for human scorers, the time saved in actual slide scoring would likely be greater than the time spent in slide preparation if automated scorers were to be used.

#### 4.1.2 Comparison of Methods

Direct comparisons between our method and Ariol are difficult because of the lack of material detailing its exact methods. As for Chang et al.’s method, Chang et al.’s dataset seemed to contain only homogeneous regions, and its tiling method did not translate well to TMAs (Figure 6) [28]. In comparison to descriptions of current methods in topic reviews, our method collected a wider variety of features and also used a lasso-regularized GLM to limit overfitting from this larger feature set, allowing it to more comprehensively quantify images’ staining [4, 8-9]. Another difference was the use of tissue segmentation and stain unmixing rather than nuclear and membrane segmentation, making our method less susceptible to the irregularity of nuclear structures in slides [4, 8-9, 13].

### 4.2 {0} versus {1+} Scoring

{0} versus {1+} scoring had been unexplored by other papers assessing inter-observer agreement despite its clinical significance [6, 8, 10-11, 32-33], but our method attempted the problem and achieved high agreement with manual scoring (Figure 13). This high agreement, especially in comparison to Chang et al.’s method’s low agreement (Figure 13), demonstrates that the model’s features can capture small differences in staining. It also suggests that the two scores are separable with reasonable consistency with automated methods.

However, the incorrectly-scored images’ small decision values and their similarities suggest ambiguity in {0} versus {1+} scoring (Figures 15 and 16). No studies were found that explored inter-pathologist agreement for this scoring task, but the fact that most studies group the two categories together supports this conjecture [6, 8, 32-33]. Part of this ambiguity may stem from the use of categories to score images, as scoring could be inconsistent for images that fall between two categories. This problem could be alleviated through automated scorers, as they

would be able to supply consistent continuous values instead of categories to assess the amount of staining in a slide, like our method’s decision values. In addition, automated scorers could catch small variations in staining that might be difficult to catch with the human eye. Thus, automated scoring could increase the viability of separating {0} and {1+} images.

### 4.3 Replication of Chang et al.’s Method

The accuracy of Chang et al.’s method for {0} versus {1+} versus {2+} versus {3+} scoring, 0.7308, was much lower than the reported accuracy, 0.9069 [28]. This discrepancy could be explained by the fact that Turashvili et al.’s dataset contained heterogeneous TMAs, while Chang et al.’s dataset included homogeneous regions of interest selected by pathologists, making its tiling method ineffective (Figure 6) [28]. However, this discrepancy could also be evidence of flaws in the replication code. Thus, the results obtained would be better substantiated with Chang et al.’s actual code, rather than a replication.

### 4.4 Other Limitations and Future Work

Because of the restriction of using publicly available data, only one dataset was used in assessing the model. Furthermore, many current methods, being commercial, were not available for replication or comparison [4, 8-9]. Because of this, one alternative explanation for the model’s high accuracy could be ease of the dataset, though the comparisons to existing methods make this explanation less likely. For future work, testing with more data, using survival data to test the model’s usefulness in prognosis, and comparing with more existing methods could further support or disprove our results. Also, {0} versus {1+} scoring ambiguity could be explored through finding inter-pathologist agreement for the problem, which would determine whether errors made by the model were due to ambiguity or flaws in the method. Finally, the method could be expanded to and tested on other IHC biomarkers that are problematic for automated scorers.

## Conclusion

This paper presented a more accurate, comprehensive method for HER2 scoring to improve upon the currently time-consuming and inconsistent manual HER2 scoring as well as the inaccurate existing automated methods. Furthermore, it assessed the overlooked but important problem of {0} versus {1+} scoring, finding potential scoring ambiguity but also the ability for reasonably consistent separation of the scores by automated systems. This paper’s tests and its comparisons with other papers’ results support the conclusion that its methods are an improvement in automated scoring. However, due to limitations in access to data and existing methods, further testing would be useful to further support or disprove the results.
  
  </div>
</div>
