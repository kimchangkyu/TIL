## Python part2

## Pandas

1. merge function
    - How to combine two data frames and output the result
    - <df1>.merge(<df2>, left_on="df1's column_name", right_on="df2's column_name")
    - pd.merge(<DataFrame1>, <DataFrame2>, how="inner or outer")

2. fillna
    - Fill NaN with specific data

3. sort_values
    - sort DataFrame
    - <DataFrame>.sort_values(by, ascending=False)

4. Pandas Pivot
    - How to create a data frame by selecting index, column, and value from the column data in the data frame
    - df.pivot(index, columns, values) - groupby and run pivot
    - df.pivot_table(values, index, columns, aggfunc)

5. Pandas io
    - input, output
        - load : pd.read_csv(filepath_or_buffer, encoding="utf8")
	- save : data_name.to_csv(path_or_buf)

6. Linear Regression
    - import pickle
    - from sklearn import linear_model - linear regression model
    - from sklearn.model_selection import train_test_split - Module that divides training data and test data
    - from sklearn.metrics import mean_absolute_error - Module to evaluate the model
    - Analysis procedure
	- 1. Load Data
	    - pd.read_csv(), ...
	- 2. Data Preprocessing
    	    - Divide independent and dependent variables
    	    - Divide training data and test data
		- ex) train_x, test_x, train_y, test_y = train_test_split(df_x, df_y, test_size=0.3, random_state=1)
	- 3. Data Analysis: Linear Regression Model
	    - model = linear_model.LinearRegression() : create model
	    - model.fit(train_x, train_y) - model learning
	- 4. Performance Evaluation: MAE
	    - pred_y = model.predict(test_x) : Generate predictions
	    - mae = mean_absolute_error(test_y, pred_y) : Comparison of predicted and actual performance
	- 5. Writing Predictive Code

7. Pickle
    - Save your model with pickle
    - save 
        - with open("datas/p_model.pkl", "wb") as f:
    		pickle.dump(model, f)
    - load
        - with open("datas/p_model.pkl", "rb") as f:
    		load_model = pickle.load(f)

