# [FeTrIL: Feature Translation for Exemplar-Free Class-Incremental Learning](https://openaccess.thecvf.com/content/WACV2023/html/Petit_FeTrIL_Feature_Translation_for_Exemplar-Free_Class-Incremental_Learning_WACV_2023_paper.html)
*Grégoire Petit, Adrian Popescu, Hugo Schindler, David Picard, Bertrand Delezoide*. *WACV 2023*.

**TL;DR:** FeTrIL represent new classes by their features obtained from feature extractor. Past classes are however represented by pseudo-features that are derived from the new classes by geometric translation.
Hence, it is able to do exemplar free classs incremental learning by constraining the space by both features of new classes and pseudo features of the old classes.


FeTrIL introduces a novel technique that aims to strike a better stability-plasticity balance by incorporating both a fixed feature extractor and a pseudo-features generator. 
This generator employs a simple yet effective geometric translation method to produce representations of past classes in the form of pseudo-features. 
This translation process only requires storing the centroid representations of previous classes. 
By combining the actual features of new classes with the pseudo-features of past classes, FeTrIL creates a comprehensive dataset that is fed into an incremental linear classifier. 
The linear classifier is then trained to progressively discriminate between all classes, leading to improved performance.
This also led to much faster method compared to mainstream ones which update the entire deep model.

FeTrIL first trains the feature extractor with an initial task which is usually larger than the rest of the incremental tasks and then freeze it.
This ensures the stable space representation through the entire CL process.
Before moving to the next task, it saves the centroids of learned classes.
Then, in the following tasks, it extacts the features of new classes.
To generate Pseudo-features of past classes, FeTrIL projects the feature distribution of the new classes to the centroids of the old classes:

$$
f(c_p)=f(c_n)+\mu(C_p)-\mu(C_n)
$$

where $μ(C_p)$, $μ(C_n)$ are the mean features of classes $C_p$ and $C_n$ extracted with $F$ and $f(c_n)$ is features of a sample $c_n$ of class $C_n$.

Finally, it trains the incremental linear classifier.
Note that, when CIL tasks include more than one classes, FeTrIL uses cosine similarity between class centroids to decide which feature distribution should be projected to the old classes. 

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/fetril.png?raw=true" width=800>
</p>
