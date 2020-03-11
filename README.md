# Text Classification
## Written to run on a CentOS server. Yum!
### cnb_dev.py is a sandbox to train and test ~~text classification models~~ multilayer Bayesian network trees that predict Harmonized Tariff Scheduling (HTS/HS) codes by analyzing containerized cargo description data. After basic natural language processing, data is passed to the root node where it is vectorized and used to train a slightly modified version of scikit-learn's implementation* of a Complement Naive Bayes** (CNB) classifier. The data is then partitioned on the predicted values and branched into the first layer of child nodes, each containing another TF-IDF vectorizer, CNB classifier pair. This branching process occurs once more before final predictions are aggregated based on residual index values. As we descend further into the tree, the CNB classifiers are predicting decreasingly general characteristics before they settle on a 4-digit HS code for each container.
##### *\*https://scikit-learn.org/stable/modules/generated/sklearn.naive_bayes.ComplementNB.html*
##### *\*\*Rennie et al. (2003) https://people.csail.mit.edu/jrennie/papers/icml03-nb.pdf*
### predict_hs.py provides a user-friendly interface for the application of an exported model from cnb_dev.py to live data through a SQL query.
### sklearn_mod.py adds a bit of extra functionality to anything that inherits from the _BaseNB() class in the sklearn.naive_bayes module.
