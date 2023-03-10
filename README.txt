README

BEASTNET file include the functions for using the BEAST-Net model, from the paper "BEAST-Net: A neural network adaptation of a behavioral model":

preprocess:
The function receives dataset in the original CPC dataset structure and produce a Processed data set for
the BEAST-net model: it creates pickle files (a file for each 100 games) with all of the possible delta ST values and the probabilities to recieve them.
the delta  ST values and probabilities are stored in a vector for each sampling tool combination, with different values when trial=0 and trial=1,...4.
for each 100 choice tasks there is a seperate pickle file. first 100 choice tasks file is ended with _100 etc.
run preprocessing only *once*!, *on the whole dataset. then you can train many models as you wish, per subgroup or for all of the data.
you will receive  pickles files of the processed dataset.

preproccsing is using functions from the code of Plonsky et al., 2017 for a technical interpetation of the original dataset

trainBEASTNet:
The function trains a network the learns the parameters of the sampling tool probabilities, the BEV weight (w in the paper), and the sigmoid curvature (b in the paper)
it prints the parameters values  every 10 games in the log file and here (so the final values will be at the end of the log file)
and at the end creates a csv file (named by the param csvNameFinal) with the prediction of the tuned BEAST in a column named 'BEASTNET'
if you want to run a subgroup model. please train the model first on non dominant problems, and then take the parameters it learned from the log file, and  put them in probs0,...probs4 and run the model on the subgroup.
when you run a model on a subgroup/non_dom/dom choice tasks, the csv must include only those choice tasks. while the preprocessed pickle file will include all the dataset
for getting a clustered model please run deep_clustering_kmeans.py which produced a clustered dataset (with column 'cluster') and then run a different BEASTNet model per cluster, you will need to create a seperate csv file per cluster as any other subgroup

deep_clustering_kmeans,DCN,kmeans and autoencoder are using for clusering the dataset.
you need to run deep_clustering_kmeans.py and specify there the name of the csv to run on, and number of clusters. and the name of the clustered  dataset. after that you can split the dataset according to the clusters and run a separate BEAST-Net model for every cluster.
the clustered dataset will have a column name 'cluster' with the cluster number.


