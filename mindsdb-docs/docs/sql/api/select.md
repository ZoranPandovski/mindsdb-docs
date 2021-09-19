# SELECT statement

The `SELECT` statement is used to get a predictons from the model table. The data is not persistent and is returned on the fly as a result-set.

```sql
SELECT column_name, column_name2 FROM model_table;
```

The below list contains the column names of the model table. Note that `target_varaiable_` will be the name of the target variable column.

* target_variable_original - The original value of the target variable.
* target_variable_min - Lower bound of the predicted value.
* target_variable_max - Upper bound of the predicted value.
* target_variable_confidence - Model confidence score.
* target_variable_explain - JSON object that contains additional information as `confidence_lower_bound`, `confidence_upper_bound`, `anomaly`, `truth`.
* when_data - The data to make the predictions from(WHERE clause params).
* select_data_query - SQL select query to create the datasource.
* external_datasource - Name of the pre-existing datasource that the model was built from.



## SELECT example

The following SQL statement selects all information from the `home_rentals_model`:


```sql
SELECT * FROM mindsdb.home_rentals 
WHERE when_data='{"sqft": 800, "number_of_rooms": 4, "number_of_bathrooms": 2,
				  "location": "good", "days_on_market" : 12, 
                  "neighborhood": "downtown", "initial_price": "2222"}';

```

![SELECT model_name](/assets/sql/select_hr.png)

{{ read_csv('https://raw.githubusercontent.com/mindsdb/mindsdb-examples/master/classics/home_rentals/home_rentals_model.csv') }}


The following SQL statement selects only the target variable `rental_price` and accuracy from the `home_rentals_model` and adds alias names:


```sql
SELECT rental_price as price, 
rental_price_confidence as accuracy 
FROM mindsdb.home_rentals WHERE when_data='{"sqft": 800, "number_of_rooms": 4, "number_of_bathrooms": 2, 
                                            "location": "good", "days_on_market" : 12,  
                                            "neighborhood": "downtown", "initial_price": "2222"}';
```

![SELECT model_name](/assets/sql/select_hra.png)