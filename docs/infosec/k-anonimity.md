# K-anonimity

*K-anonimity* is a property of datasets containing information about some unique entities (e.g., databases with personal records), such that for every entity whose information is contained in the dataset, it is impossible to distinguish its information from at least *k-1* other unique entities in that same dataset. That is, for any entry in the dataset, there are at least *k* different entities it can belong to. K-anonimity is usually achieved using two methods:
   * Suppression: removing some of the features from the dataset, e.g., erasing some column from the database.
   * Binning/Generalization: replacing certain compnonents of the data with a coarse grained bin or category for that data. For example, if the dataset contains age as a column, we can replace the exact age entries with an age range ("45 yo" -> "between 40 and 50"). Such binned attributes are called *quasi-identifiers* because while they are not sufficient to identify an individual on their own, they can be used for unique identification when combined.

There are two common types of attacks against k-anonimity:
   * Homogeneity attack: if the sensitive values for a particular k-anonymious equivalence class are not diverse enough, e.g., if they are the same among all or most of the members of said class, the attacker can still infer the data for the particular individual with high probaability.
   * Background knowledge attack: the attacker utilizes some association between the pseudo-identifiers and the sensitive attibutes in order to infer the value of a sensitive attribute for an individual, or at least narrow it down.

K-anonimity can be strenghtened against homogeneity attacks by introducing l-diversity to the data. **L-diversity** is a property of a k-anonimized dataset such that in every equivalence class of tuples that share quasi-identifiers, the set of corresponding sensitive attributes includes at least *l* different values.

#infosec