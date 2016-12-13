##Basic Data Structure API
----
###Dataset
####__init__(data, label=None, max_bin=255, reference=None, weight=None, group=None, silent=False, feature_name=None, categorical_feature=None, params=None, free_raw_data=True)

    Parameters
    ----------
    data : string/numpy array/scipy.sparse
        Data source of Dataset.
        When data type is string, it represents the path of txt file
    label : list or numpy 1-D array, optional
        Label of the data
    max_bin : int, required
        Max number of discrete bin for features
    reference : Other Dataset, optional
        If this dataset validation, need to use training data as reference
    weight : list or numpy 1-D array , optional
        Weight for each instance.
    group : list or numpy 1-D array , optional
        Group/query size for dataset
    silent : boolean, optional
        Whether print messages during construction
    feature_name : list of str
        Feature names
    categorical_feature : list of str or int
        Categorical features,
        type int represents index,
        type str represents feature names (need to specify feature_name as well)
    params: dict, optional
        Other parameters
    free_raw_data: Bool
        True if need to free raw data after construct inner dataset
    

####construct()

    Lazy init
    

####create_valid(data, label=None, weight=None, group=None, silent=False, params=None)

    Create validation data align with current dataset

    Parameters
    ----------
    data : string/numpy array/scipy.sparse
        Data source of _InnerDataset.
        When data type is string, it represents the path of txt file
    label : list or numpy 1-D array, optional
        Label of the training data.
    weight : list or numpy 1-D array , optional
        Weight for each instance.
    group : list or numpy 1-D array , optional
        Group/query size for dataset
    silent : boolean, optional
        Whether print messages during construction
    params: dict, optional
        Other parameters
    

####get_group()

    Get the initial score of the Dataset.

    Returns
    -------
    init_score : array
    

####get_init_score()

    Get the initial score of the Dataset.

    Returns
    -------
    init_score : array
    

####get_label()

    Get the label of the Dataset.

    Returns
    -------
    label : array
    

####get_weight()

    Get the weight of the Dataset.

    Returns
    -------
    weight : array
    

####num_data()

    Get the number of rows in the Dataset.

    Returns
    -------
    number of rows : int
    

####num_feature()

    Get the number of columns (features) in the Dataset.

    Returns
    -------
    number of columns : int
    

####save_binary(filename)

    Save Dataset to binary file

    Parameters
    ----------
    filename : string
        Name of the output file.
    

####set_categorical_feature(categorical_feature)

    Set categorical features

    Parameters
    ----------
    categorical_feature : list of int or str
        Name/index of categorical features

    

####set_feature_name(feature_name)

    Set feature name

    Parameters
    ----------
    feature_name : list of str
        Feature names
    

####set_group(group)

    Set group size of Dataset (used for ranking).

    Parameters
    ----------
    group : numpy array or list or None
        Group size of each group
    

####set_init_score(init_score)

    Set init score of booster to start from.

    Parameters
    ----------
    init_score: numpy array or list or None
        Init score for booster
    

####set_label(label)

    Set label of Dataset

    Parameters
    ----------
    label: numpy array or list or None
        The label information to be set into Dataset
    

####set_reference(reference)

    Set reference dataset

    Parameters
    ----------
    reference : Dataset
        Will use reference as template to consturct current dataset
    

####set_weight(weight)

    Set weight of each instance.

    Parameters
    ----------
    weight : numpy array or list or None
        Weight for each data point
    

####subset(used_indices, params=None)

    Get subset of current dataset

    Parameters
    ----------
    used_indices : list of int
        Used indices of this subset
    params : dict
        Other parameters
    

###Booster
####__init__(params=None, train_set=None, model_file=None, silent=False)

    Initialize the Booster.

    Parameters
    ----------
    params : dict
        Parameters for boosters.
    train_set : Dataset
        Training dataset
    model_file : string
        Path to the model file.
    silent : boolean, optional
        Whether print messages during construction
    

####add_valid(data, name)

    Add an validation data

    Parameters
    ----------
    data : Dataset
        Validation data
    name : String
        Name of validation data
    

####attr(key)

    Get attribute string from the Booster.

    Parameters
    ----------
    key : str
        The key to get attribute from.

    Returns
    -------
    value : str
        The attribute value of the key, returns None if attribute do not exist.
    

####current_iteration()

####dump_model()

    Dump model to json format

    Returns
    -------
    Json format of model
    

####eval(data, name, feval=None)

    Evaluate for data

    Parameters
    ----------
    data : _InnerDataset object
    name :
        Name of data
    feval : function
        Custom evaluation function.
    Returns
    -------
    result: list
        Evaluation result list.
    

####eval_train(feval=None)

    Evaluate for training data

    Parameters
    ----------
    feval : function
        Custom evaluation function.

    Returns
    -------
    result: str
        Evaluation result list.
    

####eval_valid(feval=None)

    Evaluate for validation data

    Parameters
    ----------
    feval : function
        Custom evaluation function.

    Returns
    -------
    result: str
        Evaluation result list.
    

####feature_importance(importance_type=split)

    Feature importances

    Returns
    -------
    Array of feature importances
    

####predict(data, num_iteration=-1, raw_score=False, pred_leaf=False, data_has_header=False, is_reshape=True)

    Predict logic

    Parameters
    ----------
    data : string/numpy array/scipy.sparse
        Data source for prediction
        When data type is string, it represents the path of txt file
    num_iteration : int
        Used iteration for prediction
    raw_score : bool
        True for predict raw score
    pred_leaf : bool
        True for predict leaf index
    data_has_header : bool
        Used for txt data
    is_reshape : bool
        Reshape to (nrow, ncol) if true

    Returns
    -------
    Prediction result
    

####reset_parameter(params)

    Reset parameters for booster

    Parameters
    ----------
    params : dict
        New parameters for boosters
    silent : boolean, optional
        Whether print messages during construction
    

####rollback_one_iter()

    Rollback one iteration
    

####save_model(filename, num_iteration=-1)

    Save model of booster to file

    Parameters
    ----------
    filename : str
        Filename to save
    num_iteration: int
        Number of iteration that want to save. < 0 means save all
    

####set_attr(kwargs)

    Set the attribute of the Booster.

    Parameters
    ----------
    **kwargs
        The attributes to set. Setting a value to None deletes an attribute.
    

####set_train_data_name(name)

####update(train_set=None, fobj=None)

    Update for one iteration
    Note: for multi-class task, the score is group by class_id first, then group by row_id
          if you want to get i-th row score in j-th class, the access way is score[j*num_data+i]
          and you should group grad and hess in this way as well

    Parameters
    ----------
    train_set :
        Training data, None means use last training data
    fobj : function
        Customized objective function.

    Returns
    -------
    is_finished, bool
    

##Training API
----
####train(params, train_set, num_boost_round=100, valid_sets=None, valid_names=None, fobj=None, feval=None, init_model=None, feature_name=None, categorical_feature=None, early_stopping_rounds=None, evals_result=None, verbose_eval=True, learning_rates=None, callbacks=None)

    Train with given parameters.

    Parameters
    ----------
    params : dict
        Parameters for training.
    train_set : Dataset
        Data to be trained.
    num_boost_round: int
        Number of boosting iterations.
    valid_sets: list of Datasets
        List of data to be evaluated during training
    valid_names: list of string
        Names of valid_sets
    fobj : function
        Customized objective function.
    feval : function
        Customized evaluation function.
        Note: should return (eval_name, eval_result, is_higher_better) of list of this
    init_model : file name of lightgbm model or 'Booster' instance
        model used for continued train
    feature_name : list of str
        Feature names
    categorical_feature : list of str or int
        Categorical features,
        type int represents index,
        type str represents feature names (need to specify feature_name as well)
    early_stopping_rounds: int
        Activates early stopping.
        Requires at least one validation data and one metric
        If there's more than one, will check all of them
        Returns the model with (best_iter + early_stopping_rounds)
        If early stopping occurs, the model will add 'best_iteration' field
    evals_result: dict or None
        This dictionary used to store all evaluation results of all the items in valid_sets.
        Example: with a valid_sets containing [valid_set, train_set]
                 and valid_names containing ['eval', 'train']
                 and a paramater containing ('metric':'logloss')
        Returns: {'train': {'logloss': ['0.48253', '0.35953', ...]},
                  'eval': {'logloss': ['0.480385', '0.357756', ...]}}
        passed with None means no using this function
    verbose_eval : bool or int
        Requires at least one item in evals.
        If `verbose_eval` is True,
            the eval metric on the valid set is printed at each boosting stage.
        If `verbose_eval` is int,
            the eval metric on the valid set is printed at every `verbose_eval` boosting stage.
        The last boosting stage
            or the boosting stage found by using `early_stopping_rounds` is also printed.
        Example: with verbose_eval=4 and at least one item in evals,
            an evaluation metric is printed every 4 (instead of 1) boosting stages.
    learning_rates: list or function
        List of learning rate for each boosting round
        or a customized function that calculates learning_rate in terms of
        current number of round (and the total number of boosting round)
        (e.g. yields learning rate decay)
        - list l: learning_rate = l[current_round]
        - function f: learning_rate = f(current_round, total_boost_round)
                   or learning_rate = f(current_round)
    callbacks : list of callback functions
        List of callback functions that are applied at end of each iteration.

    Returns
    -------
    booster : a trained booster model
    

####cv(params, train_set, num_boost_round=10, nfold=5, stratified=False, metrics=None, fobj=None, feval=None, init_model=None, feature_name=None, categorical_feature=None, early_stopping_rounds=None, fpreproc=None, verbose_eval=None, show_stdv=True, seed=0, callbacks=None)

    Cross-validation with given paramaters.

    Parameters
    ----------
    params : dict
        Booster params.
    train_set : Dataset
        Data to be trained.
    num_boost_round : int
        Number of boosting iterations.
    nfold : int
        Number of folds in CV.
    stratified : bool
        Perform stratified sampling.
    folds : a KFold or StratifiedKFold instance
        Sklearn KFolds or StratifiedKFolds.
    metrics : string or list of strings
        Evaluation metrics to be watched in CV.
    fobj : function
        Custom objective function.
    feval : function
        Custom evaluation function.
    init_model : file name of lightgbm model or 'Booster' instance
        model used for continued train
    feature_name : list of str
        Feature names
    categorical_feature : list of str or int
        Categorical features, type int represents index,
        type str represents feature names (need to specify feature_name as well)
    early_stopping_rounds: int
        Activates early stopping. CV error needs to decrease at least
        every <early_stopping_rounds> round(s) to continue.
        Last entry in evaluation history is the one from best iteration.
    fpreproc : function
        Preprocessing function that takes (dtrain, dtest, param)
        and returns transformed versions of those.
    verbose_eval : bool, int, or None, default None
        Whether to display the progress.
        If None, progress will be displayed when np.ndarray is returned.
        If True, progress will be displayed at boosting stage.
        If an integer is given,
            progress will be displayed at every given `verbose_eval` boosting stage.
    show_stdv : bool, default True
        Whether to display the standard deviation in progress.
        Results are not affected, and always contains std.
    seed : int
        Seed used to generate the folds (passed to numpy.random.seed).
    callbacks : list of callback functions
        List of callback functions that are applied at end of each iteration.

    Returns
    -------
    evaluation history : list(string)
    

##Scikit-learn API
----
###Common Methods
####__init__(num_leaves=31, max_depth=-1, learning_rate=0.1, n_estimators=10, max_bin=255, silent=True, objective=regression, nthread=-1, min_split_gain=0, min_child_weight=5, min_child_samples=10, subsample=1, subsample_freq=1, colsample_bytree=1, reg_alpha=0, reg_lambda=0, scale_pos_weight=1, is_unbalance=False, seed=0)

    Implementation of the Scikit-Learn API for LightGBM.

    Parameters
    ----------
    num_leaves : int
        Maximum tree leaves for base learners.
    max_depth : int
        Maximum tree depth for base learners, -1 means no limit.
    learning_rate : float
        Boosting learning rate
    n_estimators : int
        Number of boosted trees to fit.
    silent : boolean
        Whether to print messages while running boosting.
    objective : string or callable
        Specify the learning task and the corresponding learning objective or
        a custom objective function to be used (see note below).
        default: binary for LGBMClassifier, lambdarank for LGBMRanker
    nthread : int
        Number of parallel threads
    min_split_gain : float
        Minimum loss reduction required to make a further partition on a leaf node of the tree.
    min_child_weight : int
        Minimum sum of instance weight(hessian) needed in a child(leaf)
    min_child_samples : int
        Minimum number of data need in a child(leaf)
    subsample : float
        Subsample ratio of the training instance.
    subsample_freq : int
        frequence of subsample, <=0 means no enable
    colsample_bytree : float
        Subsample ratio of columns when constructing each tree.
    reg_alpha : float
        L1 regularization term on weights
    reg_lambda : float
        L2 regularization term on weights
    scale_pos_weight : float
        Balancing of positive and negative weights.
    is_unbalance : bool
        Is unbalance for binary classification
    seed : int
        Random number seed.

    Note
    ----
    A custom objective function can be provided for the ``objective``
    parameter. In this case, it should have the signature
    ``objective(y_true, y_pred) -> grad, hess`` 
        or ``objective(y_true, y_pred, group) -> grad, hess``:

        y_true: array_like of shape [n_samples]
            The target values
        y_pred: array_like of shape [n_samples] or shape[n_samples* n_class]
            The predicted values
        group: array_like
            group/query data, used for ranking task
        grad: array_like of shape [n_samples] or shape[n_samples* n_class]
            The value of the gradient for each sample point.
        hess: array_like of shape [n_samples] or shape[n_samples* n_class]
            The value of the second derivative for each sample point

    for multi-class task, the y_pred is group by class_id first, then group by row_id
        if you want to get i-th row y_pred in j-th class, the access way is y_pred[j*num_data+i]
        and you should group grad and hess in this way as well
    

####apply(X, num_iteration=0)

    Return the predicted leaf every tree for each sample.

    Parameters
    ----------
    X : array_like, shape=[n_samples, n_features]
        Input features matrix.

    num_iteration : int
        Limit number of iterations in the prediction; defaults to 0 (use all trees).

    Returns
    -------
    X_leaves : array_like, shape=[n_samples, n_trees]
    

####booster()

    Get the underlying lightgbm Booster of this model.
    This will raise an exception when fit was not called

    Returns
    -------
    booster : a lightgbm booster of underlying model
    

####evals_result()

    Return the evaluation results.

    Returns
    -------
    evals_result : dictionary
    

####feature_importance()

    Feature importances

    Returns
    -------
    Array of normailized feature importances
    

####fit(X, y, sample_weight=None, init_score=None, group=None, eval_set=None, eval_sample_weight=None, eval_init_score=None, eval_group=None, eval_metric=None, early_stopping_rounds=None, verbose=True, feature_name=None, categorical_feature=None, other_params=None)

    Fit the gradient boosting model

    Parameters
    ----------
    X : array_like
        Feature matrix
    y : array_like
        Labels
    sample_weight : array_like
        weight of training data
    init_score : array_like
        init score of training data
    group : array_like
        group data of training data
    eval_set : list, optional
        A list of (X, y) tuple pairs to use as a validation set for early-stopping
    eval_sample_weight : List of array
        weight of eval data
    eval_init_score : List of array
        init score of eval data
    eval_group : List of array
        group data of eval data
    eval_metric : str, list of str, callable, optional
        If a str, should be a built-in evaluation metric to use.
        If callable, a custom evaluation metric, see note for more details.
    early_stopping_rounds : int
    verbose : bool
        If `verbose` and an evaluation set is used, writes the evaluation
    feature_name : list of str
        Feature names
    categorical_feature : list of str or int
        Categorical features,
        type int represents index,
        type str represents feature names (need to specify feature_name as well)
    other_params: dict
        Other parameters

    Note
    ----
    Custom eval function expects a callable with following functions:
        ``func(y_true, y_pred)``, ``func(y_true, y_pred, weight)``
            or ``func(y_true, y_pred, weight, group)``.
        return (eval_name, eval_result, is_bigger_better)
            or list of (eval_name, eval_result, is_bigger_better)

        y_true: array_like of shape [n_samples]
            The target values
        y_pred: array_like of shape [n_samples] or shape[n_samples * n_class] (for multi-class)
            The predicted values
        weight: array_like of shape [n_samples]
            The weight of samples
        group: array_like
            group/query data, used for ranking task
        eval_name: str
            name of evaluation
        eval_result: float
            eval result
        is_bigger_better: bool
            is eval result bigger better, e.g. AUC is bigger_better.
    for multi-class task, the y_pred is group by class_id first, then group by row_id
      if you want to get i-th row y_pred in j-th class, the access way is y_pred[j*num_data+i]
    

####get_params(deep=False)

    Get parameters
    

####predict(data, raw_score=False, num_iteration=0)

    Return the predicted value for each sample.

    Parameters
    ----------
    X : array_like, shape=[n_samples, n_features]
        Input features matrix.

    num_iteration : int
        Limit number of iterations in the prediction; defaults to 0 (use all trees).

    Returns
    -------
    predicted_result : array_like, shape=[n_samples] or [n_samples, n_classes]
    

###LGBMClassifier

####predict_proba(data, raw_score=False, num_iteration=0)

    Return the predicted probability for each class for each sample.

    Parameters
    ----------
    X : array_like, shape=[n_samples, n_features]
        Input features matrix.

    num_iteration : int
        Limit number of iterations in the prediction; defaults to 0 (use all trees).

    Returns
    -------
    predicted_probability : array_like, shape=[n_samples, n_classes]
    

###LGBMRegressor

###LGBMRanker

####fit(X, y, sample_weight=None, init_score=None, group=None, eval_set=None, eval_sample_weight=None, eval_init_score=None, eval_group=None, eval_metric=None, eval_at=None, early_stopping_rounds=None, verbose=True, feature_name=None, categorical_feature=None, other_params=None)

    Most arguments like common methods except following:

    eval_at : list of int
        The evaulation positions of NDCG
    
