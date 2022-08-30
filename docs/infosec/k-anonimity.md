# K-anonimity

*K-anonimity* is a property of datasets containing information about some unique entities (e.g., databases with personal records), such that for every entity whose information is contained in the dataset, it is impossible to distinguish its information from at least k-1 other unique entities in that same dataset. That is, for any entry in the dataset, there are at least *k* different entities it can belong to. K-anonimity is usually achieved using two methods:

    * Suppression: removing some of the features from the dataset, e.g., erasing some column from the database.
    * Binning/Generalization: replacing certain compnonents of the data with a coarse grained bin or category for that data. For example, if the dataset contains age as a column, we can replace the exact age entries with an age range ("45 yo" -> "between 40 and 50").

#infosec