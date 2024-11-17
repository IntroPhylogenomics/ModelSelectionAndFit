# Model Selection and Model Fit

This repository contains tutorials that explore ways to select phylogenetic models for your data and then analyze how well those models fit the data.

First, we'll use RevBayes to select among substitution models using Bayes factors. The tutorial is available [here](https://revbayes.github.io/tutorials/model_selection_bayes_factors/bf_subst_model.html).

We can use Bayes factors to select models in many contexts beyond only substitution models. We might use them to select between concatenated and multispecies coalescent models or alternative clock models in a divergence time analysis. Here we'll use them to select a partition model. A tutorial that demonstrates how to do this is posted [here](https://revbayes.github.io/tutorials/partition/).

As we have seen in the lecture slides, the number of possible partition models grows rapidly as the size of a dataset grows. For large datasets, it can be impractical to use Bayes factors to investigate many possible partition models. We can use alternative and faster strategies to accomplish something similar. IQTree will allow you to do this, selecting both a reasonable partition model and substitution models for each partition. You can easily run this analysis in IQTree for the example files using the command:

```
 iqtree -s concat.nex -spp partition.nex -m MFP+MERGE
```
The ```concat.nex``` files contains the same four simulated loci that we just estimated Bayes Factors for, and the ```partition.nex``` file simply specifies where the locus boundaries in the concatenated alignment. After running this command, open the ```partition.nex.best_scheme.nex``` file, which contains the optimal partitioning scheme that IQtree found. You can read more about this functionality [here](http://www.iqtree.org/doc/Advanced-Tutorial#choosing-the-right-partitioning-scheme).

The above exercises demonstrate how to measure relative model fit, which asks 'What model, among a set of candidates, fits my data the best?' It is of course possible that all of the models in our set of candidates fit the data poorly. In this case, we would simply be choosing the best of a bad bunch without necessarily realizing it. To avoid this, we often want to measure how well the model describes the data in an absolute sense. To do this in a Bayesian framework, we can use posterior prediction. A tutorial introducing posterior prediction in RevBayes for a non-phylogenetic example is available [here](https://revbayes.github.io/tutorials/intro_posterior_prediction/). Once you understand the fundamentals of posterior prediction in a general sense, these tutorials will show you how to do this for phylogenetic analyses using the P<sup>3</sup> pipeline in RevBayes for both [data based](https://revbayes.github.io/tutorials/model_testing_pps/pps_data.html) and [inference based](https://revbayes.github.io/tutorials/model_testing_pps/pps_inference.html) test statistics.

As a final exercise, we can bring together many of the things that we have been working on to assess the fit of our partition model. We'll use the model identified by IQtree (1:GTR, 2:HKY+G, 3,4:JC). You'll need to set up a revscript that:

- reads in the four loci
- sets up an appropriate partitioning scheme
- assigns the correct substitution model to each gene
- run a P<sup>3</sup> analysis for this model

Does the model seem to be an adequate description of the data?