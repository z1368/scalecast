# Changelog
All notable changes to this project will be documented in this file. We keep track of changes in this file since v0.1.8. The source code for all releases is available on GitHub.

## [0.6.4] - 2022-02-25
### Added
- added residuals to the function `export_fitted_vals()`. Now gives dates, actuals, fitted vals, and residuals
- added `multiseries.export_model_summaries()` function
### Changed
### Fixed
- `notebook.results_vis()` broke after last update and has now been fixed

## [0.6.2] - 2022-02-25
### Added
### Changed
- the `plot()`, `plot_test_set()`, and `plot_fitted()` functions now return figures instead of automatically plotting for you. This means more customization is now possible. Took out `to_png` and related args from these functions since that can be done now with matplotlib
### Fixed
- changed the insample metric evaluations for RNN and LSTM to be on the full training set instead of just the last few observations.

## [0.6.1] - 2022-02-23
### Added
### Changed
### Fixed
- fixed an issue when calling RNN or LSTM models after a combo model that saved attributes of the combo model illogically in history
- fixed an issue that caused test-set evaluation of ARIMA models to be inaccurate (causing severe underperformance)

## [0.6.0] - 2022-02-09
### Added
- Added drop argument to several adder functions, giving the user the option to drop the original regressors after making certain transformations on them
### Changed
- `add_ar_terms()` now accepts 0 as an argument but it doesn't do anything
### Fixed
- fixed issue with `pop_using_criterion()` function that wasn't dropping models correctly in some instances
- fixed the default parameters for the rnn model which weren't working due to mislabeling of one of the parameters in TensorFlow. updated the docstring accordingly

## [0.5.9] - 2022-02-01
### Added
- Added CurrentEstimator to `__repr__()` function.
### Changed
### Fixed
- Made it impossible to forecast without adding future dates first

## [0.5.8] - 2022-01-27
### Added
### Changed
- Made it impossible to pass tune argument to `manual_forecast()`
### Fixed
- Fixed results_vis in notebook (wasn't displaying one of the widgets)

## [0.5.7] - 2022-01-26
### Added
### Changed
- Cleaned up a lot of documentation
### Fixed
- Fixed links in readme

## [0.5.6] - 2022-01-25
### Added
- Added documentation on Read the Docs
- Added cilvel information to export functions
### Changed
### Fixed

## [0.5.5] - 2022-01-20
### Added
- Added CILevel info to export model_summaries function
### Changed
### Fixed
- Fixed an issue where plots were diplaying incorrect confidence levels if `cilevel` had been changed since training it

## [0.5.4] - 2022-01-20
### Added
- Added the rnn estimator
### Changed
- plot_loss argument no longer considered a hyperparameter value for LSTM and RNN models
### Fixed
- Fixed an issue where "==" wasn't being accepted in the `evaluated_as` argument in the `pop_using_criterion()` function
- Scaler in history saved as 'minmax' instead of None for LSTM and RNN models

## [0.5.3] - 2022-01-18
### Added
- EvaluatedModels to `__repr__()`
### Changed
- Does not call `infer_freq()` as often, making code more efficient
### Fixed
- sometimes the attribute `ci_bootstrap_samples` was being called `bootstrap_samples`, changed everything to `bootstrap_samples` only

## [0.5.2] - 2022-01-12
### Added
### Changed
### Fixed
- Fixed an error that occured when calling the `__repr__()` method if no models had been evaluated first

## [0.5.1] - 2022-01-12
### Added
- Added `export_fitted_vals()` function
- Added ci option to the `results_vis()` function in notebook
- Added the `get_funcs()` function
### Changed
- No `Xvars` in LSTM model, changed to lags (now model will only look at its own history)
- No `normalizer` in LSTM model (always uses a minmax scaler now)
- LSTM model can no longer be tuned
- Got rid of all lstm model grids
- changed `__str__()` and `__repr__()` so that they now offer better info
### Fixed
- Fixed the LSTM model by scaling the dependent variable and unscaling it (minmax) when it comes out and getting rid of other Xvars

## [0.5.0] - 2022-01-10
### Added
- Added confidence intervals using bootstrapping
  - `set_cilvel()` function (default .95)
  - `set_bootstrap_samples()` function (default 100)
- Added `ci` parameter to `plot()` and `plot_test_set()` function 
- Added UpperCI, LowerCI, TestSetUpperCI, TestSetLowerCI keys to history dict
- Added `export_forecasts_with_cis()` and `export_test_set_preds_with_cis()` functions
- Added source code (commented out) to get level confidence intervals -- when I tested, the intervals were too large to implement but maybe in the future this will be revisited
### Changed
### Fixed

## [0.4.4] - 2022-01-07
### Added
- added lstm grid in example grids
- added EarlyStopping callback functionality for the LSTM model
- added `get_expanded_lstm_grid()` to GridGenerator module which gives an example of a grid with early stopping
### Changed
- changed default paramaters for the lstm model
- added `**kwargs` to the lstm model forecast function that are passed to the `fit()` function in TensorFlow, got rid of `epochs` and `batch_size` args consequently
### Fixed

## [0.4.25] - (quick fix) 2022-01-06
### Added
### Changed
### Fixed
- source code was using `f` instead of `self` when when calling `pop_using_criterion()`

## [0.4.2] - 2022-01-06
### Added
- lstm estimator
- added `pop_using_criterion()` function
### Changed
- Fixed an issue where sklearn models were being fit on the same data twice -- does not change outcomes but the models run faster now
- Output from `_scale()` function is now always a numpy matrix (could have been either that or pandas dataframe before)
- sorted `_estimators_` list
- changed the error message for when importing a grid fails to account for one other possible reason the failure occured
### Fixed

## [0.4.1] - 2021-12-30
### Added
- Can now sort by metric value in `export_all_validation_grids_to_excel()`
### Changed
### Fixed
- Fixed an issue where sometimes the incorrect AR terms were being propogated for test-set evaluation only

## [0.4.0] - 2021-12-30
### Added
### Changed
- deleted the 'scale' normalizer from the mlp grid
### Fixed
- Fixed an issue with the PowerTransformer normalizer that failed because of a DivideByZero error, now defaults to a StandardScaler when this issue is encountered and logs a warning

## [0.3.9] - 2021-12-30
### Added
- Added `init_dates` and `levely` attributes
- Added `'Observations'` info to history and `export()`
- Added `'lvl_test_set_predictions'` to export dataframes
### Changed
- Got rid of `first_obs` and `first_dates` attributes and wrote more efficient code to do what they were there for
- More information available when `__str__()` is called
### Fixed
- Fixed what became an issue with the last update in which when calling `add_diffed_terms()` or `add_lagged_terms()`, the level series wasn't accurate due to how undifferencing was being executed. After examining this issue, it became evident that the previous way to undifference forecasts was less efficient than it should have been, this update fixed the issues from the last update and made the code more efficient
- Fixed an issue where AR terms were manipulating the underlying xreg structures so that each forecast were using its own test-set propogated AR values instead of the correct AR values
- Fixed the `export_Xvars_df()` method which wasn't working correctly if at least one forecast hadn't been called first

## [0.3.8] - 2021-12-29
### Added
- added the following functions that can each add additional Xvars to forecast with:
	- `add_exp_terms()` - for non polynomial exponential transformations
	- `add_logged_terms()` - for log of any base transformations
	- `add_pt_terms()` - for individual variable power transformations (box cox and yeo johnson available)
	- `add_diffed_terms()` - to difference non-y terms
	- `add_lagged_terms()` - to lag non-y terms
- added the 'pt' normalizer for yeo-johnson normalization (in addition to 'minmax', 'normalize', and 'scale')
- added the `drop_Xvars()` function that is identical to the `drop_regressors()` function
### Changed
- imports all sklearn models as soon as scalecast is imported
- src code cleanup with better coding practices when it comes to forecasting sklearn models (no more copying and pasting new functions)
- changed several set data types to lists in src code
- changed the names of some hidden functions
- other src code cleanup for readability and minor efficiency gains
- better in-line comments and docstring documentation
- got rid of quiet paramater in `save_summary_stats()` and `save_feature_importance()` and now these simply log any problems as warnings
- time trends now start at 1 instead of 0 (makes log transformations possible)
- observation dropping for AR terms in sklearn models now based on the number of N/A values in each AR term instead of just the AR number
- changed some example grids to include the pt normalizer
### Fixed
- now logs all warnings

## [0.3.7] - 2021-12-27
### Added
- `dynamic_testing` argument to `manual_forecast()` and `auto_forecast()` functions -- this is `True` by default (makes all testing comparable between sklearn/non-sklearn models)
- `dynamic_tuning` argument to `tune()` function -- this is `False` by default to majorly improve speed in some applications
### Changed
- native Forecaster warnings will be logged
### Fixed

## [0.3.6] - 2021-12-14
### Added
- added `tune_test_forecast()` function to notebook module to create a progress bar when using a notebook
### Changed
### Fixed
- fixed an issue with `Forecaster.ingest_Xvars_df()` when `use_future_dates=False` causing an error to be raised

## [0.3.5] - 2021-12-07
### Added
- added `include_traing` parameter to `notebook.results_vis()` function
### Changed
### Fixed
- fixed `print_attr` parameter default in `notebook.results_vis()`

## [0.3.4] - 2021-12-07
### Added
- added `results_vis()` notebook function (requires ipywidgets)
- added `Forecaster.export_Xvars_df()` function
- added `max_integration` argument to the `Forecaster.integrate()` function
### Changed
### Fixed

## [0.3.3] - 2021-11-26
### Added
### Changed
- Now reloads Grids file each time `ingest_grid()` is called so that notebooks do not have to be rerun when a grid cannot be found
### Fixed
- Fixed an issue with some sklearn estimators that occurs when passing a subset of regressors in a list to the forecast function

## [0.3.2] - 2021-11-01
#### Added
#### Changed
#### Fixed
- Found an issue when using `floor` in Prophet

## [0.3.1] - 2021-10-29
#### Added
- Added the eCommerce example
- In `limit_grid_size()`, users can now set random_seed parameter for consistent results
#### Changed
#### Fixed
- Scikit-learn models were not accepting `Xvars='all'` as an arguments
- Fixed an issue causing models run at different levels to error out sometimes when plotted
- Fixed a plotting error that occured sometimes when setting models parameter to `None`

## [0.3.0] - 2021-10-15
#### Added
- Added an option to save to png in plot(), plot_test_set(), and plot_fitted() methods using plt.savefig() from matplotlib and calling with `to_png = True`
#### Changed
- Made errors more descriptive, stripping out AssertionError types 
#### Fixed
- fixed typos in doc strings

## [0.2.9] - 2021-09-27
#### Added
#### Changed
- In plot() method, `models=None` is now accepted and will plot only actual values
- Example grids are modified to prevent overfitting in some models
#### Fixed
- Fixed the add_time_trend() method to not skip a time step in the first observation

## [0.2.8] - 2021-08-27
#### Added
- Added a descriptive error when all_feature_info_to_excel() or all_validation_grids_to_excel() fails
#### Changed
- Using pd.shift() instead of np.roll() to create AR terms to avoid further issues with AR terms
- Prophet, silverkite, and ARIMA have better Xvar validation mechanisms to ensure that autoregressive terms aren't fed to them, which could cause errors and doesn't add anything to the models that isn't already built into them. Now, even if a user tries to feed AR terms only, it will pass no Xvars to these models
#### Fixed
- AR terms were not dropping the correct first observations before being estimated with SKLEARN models, so we fixed that but it didn't seem to make a noticeable difference in any of the examples 

## [0.2.7] - 2021-08-20
#### Added
- added reset() function that deletes all regressors and resets the object to how it was initiated
- added documentation and hints in the source code
#### Changed
- changed readme documentation to be more concise
#### Fixed
- in the documentation, it was stated that the 'scale' value passed to the 'normalize' parameter when calling manual_forecast() or auto_forecast() would use a StandardScaler from sklearn, but a Normalizer was actually being applied. Now, you can pass 'scale' to get the StandardScaler, 'normalize' to get the Normalizer, or 'minmax' to get the MinMaxScaler (unchanged from previous distributions). 'minmax' is still the default for all estimators that accept this argument

## [0.2.6] - 2021-08-12
#### Added
- added train_only argument to following functions to reduce data leakage in eda/preprocessing steps: integrate, adf_test, plot_acf, plot_pacf, plot_periodogram, seasonal_decompose -- default argument is still False for these. Now it is suggested to set a test length before running any one of these methods and only examine the training set correlations to prevent data leakage
#### Changed
#### Fixed

## [0.2.5] - 2021-08-09
#### Added
- added integrate() method that can be used to automatically find the series appropriate level to achieve stationarity, according to augmented dickey fuller test
#### Changed
#### Fixed

## [0.2.4] - 2021-08-03
#### Added
- added tune_test_forecast() function that allows what used to take four lines to be aggregated into one, also allows more easy saving of feature information by setting feature_importance or summary_stats parameters to True
- added all_feature_info_to_excel() function
- added all_validation_grids_to_excel() function
#### Changed
#### Fixed
- removed a duplicate column from the dataframe created when calling the export() method

## [0.2.3] - 2021-07-19
#### Added
#### Changed
- changed removed pandas-datareader from imports in setup.py since it is not a package dependency (change having to do with installation only and should not affect anything when applying the library)
#### Fixed

## [0.2.2] - 2021-07-16
#### Added
- added GridGenerator module so user can more easily create grids in working directory
#### Changed
- changed all functions with diffy parameter (plot_acf, plot_pacf, seasonal_decompose) now accept True, False, 0, 1, or 2 as possible values
#### Fixed
- fixed issues with two-level undifferencing where it was adding values exponentially because the level was being added to the first and second-level differences
- fixed issues with two-level undifferencing where dates were being mixed up
- fixed issues with one-level test-set evaluation where the incorrect initial value was set to undifference values in the test-set only, causing miscalculation of metrics, although the bias was in both directions so when rerunning avocados.ipynb, for example, the results were virtually the same with different models now outperforming others but metrics remaining more or less the same on average; forecasted values did not change

## [0.1.9] - 2021-07-09
#### Added
- added lightgbm and silverkite as estimators
#### Changed
- changed 'which' parameter in set_valiation_metric() to 'metric' for clarity
- changed 'which' parameter in set_estimator() to 'estimator' for clarity
#### Fixed

## [0.1.8] - 2021-07-05
#### Added
#### Changed
#### Fixed
- fixed an error in combo modeling that was causing incorrect applications of weights in weighted averaging -- the weights were generating correctly but not being applied to the best-performing models in the correct order
