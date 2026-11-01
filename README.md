# Stock price forecast

Forecasts the Alphabet (`GOOGL`) daily close. Each notebook downloads prices from Yahoo Finance for 2015-11-01 through late 2023. Nothing is stored as a CSV.

Prices are scaled with `MinMaxScaler` to the range 0–1. The first 80% of the series is the training set. Each model looks at 60 days and predicts the next close, then forecasts 365 days ahead. The score is root mean squared error.

## Notebooks

| File | Model |
| --- | --- |
| `01-lstm.ipynb` | Two LSTM layers, dropout, two dense layers |
| `02-gru.ipynb` | Two GRU layers, dropout, two dense layers |
| `03-bilstm.ipynb` | Two bidirectional LSTM layers, dropout 0.2 |
| `04-cnn.ipynb` | Conv1D, max pooling, flatten, dense |
| `05-xgboost.ipynb` | XGBoost regressor |
| `06-gradient-boosting.ipynb` | Gradient boosting |
| `07-svm.ipynb` | Support vector regression, RBF kernel |
| `08-random-forest.ipynb` | Random forest |

The notebooks do not depend on each other.

## Results

Test RMSE, lowest first:

| Model | Train RMSE | Test RMSE |
| --- | ---: | ---: |
| LSTM | 78.254 | 5.730 |
| GRU | 78.917 | 5.848 |
| Gradient boosting | 0.807 | 7.991 |
| Random forest | 76.207 | 8.444 |
| Bi-LSTM | 76.869 | 9.488 |
| XGBoost | 76.616 | 9.643 |
| CNN | 77.825 | 9.945 |
| SVM | 5.683 | 10.268 |

LSTM and GRU fit this series best. Random forest and gradient boosting are next. Bi-LSTM, XGBoost, the CNN, and SVM are weaker here. The gradient-boosting and SVM training errors are far below the other training errors, so treat those two training numbers carefully if you re-run the notebooks.

## Run

```bash
pip install -r requirements.txt
```

Open any notebook from this folder.
