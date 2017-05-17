
# Beer Reviews:

For this part of the experiment, we have decided to create a recommendation system using the beer dataset. Let’s say the online alcohol seller wants to prompt people buying beer on the site with some recommendations before checkout. Using the beer dataset we will test different recommendation models and ultimately choose the best one for the ‘website’.

- brewery_id: All breweries are assigned a unique identifier, over 5230 different breweries observed	
- brewery_name: The name of the brewery, again over 5230 different breweries  	
- review_time: The time the review was made
- review_overall: The overall score of the beer between 1-5
- review_aroma: The smell of the beer ranked between 1-5
- review_appearance: The appearance of the beer between 1-5
- review_profilename: The reviewers profile name, there are over 32908 different reviewers
- beer_style: The type of beer, there are 104 different types in this dataset	
- review_palate:	palate is a scoring between 1-5. I think it represents the initial taste when the beer enters your mouth
- review_taste: Taste is also ranked between 1-5 and it represents the overall taste form entering the mouth to swallowing 
- beer_name: The name of the beer, there are over 44000 unique beers reviewed	
- beer_abv: This variable gives the ABV range of all 44000 beers, the range is between .01 - 57	
- beer_beerid: A numeric value is assigned to all of the beer names 


```python
import graphlab as gl #import graphlab
```


```python
data = gl.SFrame.read_csv('beer_reviews.csv')#read dataset
```


<pre>Finished parsing file C:\Users\Green\Downloads\beer_reviews.csv</pre>



<pre>Parsing completed. Parsed 100 lines in 0.708144 secs.</pre>


    ------------------------------------------------------
    Inferred types from first 100 line(s) of file as 
    column_type_hints=[long,str,long,float,float,float,str,str,float,float,str,float,long]
    If parsing fails due to incorrect types, you can correct
    the inferred type list above and pass it to read_csv in
    the column_type_hints argument
    ------------------------------------------------------
    


<pre>Read 453422 lines. Lines per second: 666949</pre>



<pre>Finished parsing file C:\Users\Green\Downloads\beer_reviews.csv</pre>



<pre>Parsing completed. Parsed 1586614 lines in 1.67751 secs.</pre>



```python
data#view data
```




<div style="max-height:1000px;max-width:1500px;overflow:auto;"><table frame="box" rules="cols">
    <tr>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">brewery_id</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">brewery_name</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">review_time</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">review_overall</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">review_aroma</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">review_appearance</th>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">10325</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Vecchio Birraio</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1234817823</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1.5</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2.5</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">10325</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Vecchio Birraio</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1235915097</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2.5</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.0</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">10325</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Vecchio Birraio</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1235916604</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2.5</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.0</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">10325</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Vecchio Birraio</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1234725145</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.5</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1075</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Caldera Brewing Company</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1293735206</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">4.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">4.5</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">4.0</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1075</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Caldera Brewing Company</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1325524659</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.5</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.5</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1075</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Caldera Brewing Company</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1318991115</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.5</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.5</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.5</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1075</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Caldera Brewing Company</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1306276018</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2.5</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.5</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1075</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Caldera Brewing Company</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1290454503</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">4.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.5</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1075</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Caldera Brewing Company</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1285632924</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">4.5</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.5</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">5.0</td>
    </tr>
</table>
<table frame="box" rules="cols">
    <tr>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">review_profilename</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">beer_style</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">review_palate</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">review_taste</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">beer_name</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">beer_abv</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">beer_beerid</th>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">stcules</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Hefeweizen</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1.5</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1.5</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Sausa Weizen</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">5.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">47986</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">stcules</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">English Strong Ale</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Red Moon</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">6.2</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">48213</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">stcules</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Foreign / Export Stout</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Black Horse Black Beer</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">6.5</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">48215</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">stcules</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">German Pilsener</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2.5</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Sausa Pils</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">5.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">47969</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">johnmichaelsen</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">American Double /<br>Imperial IPA ...</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">4.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">4.5</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Cauldron DIPA</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">7.7</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">64883</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">oline73</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Herbed / Spiced Beer</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.5</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Caldera Ginger Beer</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">4.7</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">52159</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Reidrover</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Herbed / Spiced Beer</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">4.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">4.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Caldera Ginger Beer</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">4.7</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">52159</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">alpinebryant</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Herbed / Spiced Beer</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.5</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Caldera Ginger Beer</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">4.7</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">52159</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">LordAdmNelson</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Herbed / Spiced Beer</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3.5</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">4.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Caldera Ginger Beer</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">4.7</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">52159</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">augustgarage</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Herbed / Spiced Beer</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">4.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">4.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Caldera Ginger Beer</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">4.7</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">52159</td>
    </tr>
</table>
[1586614 rows x 13 columns]<br/>Note: Only the head of the SFrame is printed.<br/>You can use print_rows(num_rows=m, num_columns=n) to print more rows and columns.
</div>




```python
data = data.dropna()#remove all NA's which drops about 8,000 entires
```


```python
train, test = gl.recommender.util.random_split_by_user(data, user_id = 'review_profilename', item_id='beer_name',
                                                        item_test_proportion=.2 ) #create train and test set 

```

### Base Model

- First we tried the base recommender model using the recommender() function with no parameter tuning. The model preformed ok, with the RMSE ranged from .0007 to 3.4 where the precision and recall were around .03 to .05. This performance really isn’t that great. For this project we are going to use precision and recall or check the performance of the model before RMSE is somewhat misleading.Specifically, I am more interested in precision, because I want to know to what degree this model can predict user's sentiment.  From what I read on graph lab, the recommender() method chooses a model for you based on the data you provide it.


```python
model = gl.recommender.create(train, user_id = 'review_profilename', item_id='beer_name', target='review_overall')
results = model.recommend(users = None, k = 5)
rmse_results = model.evaluate(test)
model.save('model_1')
```


<pre>Recsys training: model = ranking_factorization_recommender</pre>



<pre>Preparing data set.</pre>



<pre>    Data has 1509514 observations with 32830 users and 44032 items.</pre>



<pre>    Data prepared in: 3.07417s</pre>



<pre>Training ranking_factorization_recommender for recommendations.</pre>



<pre>+--------------------------------+--------------------------------------------------+----------+</pre>



<pre>| Parameter                      | Description                                      | Value    |</pre>



<pre>+--------------------------------+--------------------------------------------------+----------+</pre>



<pre>| num_factors                    | Factor Dimension                                 | 32       |</pre>



<pre>| regularization                 | L2 Regularization on Factors                     | 1e-009   |</pre>



<pre>| solver                         | Solver used for training                         | adagrad  |</pre>



<pre>| linear_regularization          | L2 Regularization on Linear Coefficients         | 1e-009   |</pre>



<pre>| ranking_regularization         | Rank-based Regularization Weight                 | 0.25     |</pre>



<pre>| max_iterations                 | Maximum Number of Iterations                     | 25       |</pre>



<pre>+--------------------------------+--------------------------------------------------+----------+</pre>



<pre>  Optimizing model using SGD; tuning step size.</pre>



<pre>  Using 188689 / 1509514 points for tuning the step size.</pre>



<pre>+---------+-------------------+------------------------------------------+</pre>



<pre>| Attempt | Initial Step Size | Estimated Objective Value                |</pre>



<pre>+---------+-------------------+------------------------------------------+</pre>



<pre>| 0       | 4.16667           | Not Viable                               |</pre>



<pre>| 1       | 1.04167           | Not Viable                               |</pre>



<pre>| 2       | 0.260417          | Not Viable                               |</pre>



<pre>| 3       | 0.0651042         | Not Viable                               |</pre>



<pre>| 4       | 0.016276          | Not Viable                               |</pre>



<pre>| 5       | 0.00406901        | Not Viable                               |</pre>



<pre>| 6       | 0.00101725        | Not Viable                               |</pre>



<pre>| 7       | 0.000254313       | No Decrease (3.74262 >= 1.00741)         |</pre>



<pre>| 8       | 6.35783e-005      | No Decrease (1.33345 >= 1.00741)         |</pre>



<pre>| 9       | 1.58946e-005      | 1.00435                                  |</pre>



<pre>| 10      | 7.94729e-006      | 0.998232                                 |</pre>



<pre>| 11      | 3.97364e-006      | 1.00097                                  |</pre>



<pre>| 12      | 1.98682e-006      | 1.00382                                  |</pre>



<pre>| 13      | 9.93411e-007      | 1.00548                                  |</pre>



<pre>+---------+-------------------+------------------------------------------+</pre>



<pre>| Final   | 7.94729e-006      | 0.998232                                 |</pre>



<pre>+---------+-------------------+------------------------------------------+</pre>



<pre>Starting Optimization.</pre>



<pre>+---------+--------------+-------------------+-----------------------+-------------+</pre>



<pre>| Iter.   | Elapsed Time | Approx. Objective | Approx. Training RMSE | Step Size   |</pre>



<pre>+---------+--------------+-------------------+-----------------------+-------------+</pre>



<pre>| Initial | 0us          | 1.00969           | 0.71772               |             |</pre>



<pre>+---------+--------------+-------------------+-----------------------+-------------+</pre>



<pre>| 1       | 2.88s        | 1.00123           | 0.710508              |             |</pre>



<pre>| 2       | 5.77s        | 1.00058           | 0.706786              |             |</pre>



<pre>| 3       | 8.63s        | 1.00393           | 0.705805              |             |</pre>



<pre>| 4       | 11.50s       | 1.00925           | 0.705878              |             |</pre>



<pre>| 5       | 14.38s       | 1.01576           | 0.706899              |             |</pre>



<pre>| 6       | 17.26s       | 1.02319           | 0.70859               |             |</pre>



<pre>| 7       | 20.19s       | 1.0319            | 0.710985              |             |</pre>



<pre>| 8       | 23.09s       | 1.0414            | 0.713765              |             |</pre>



<pre>| 9       | 26.02s       | 1.05091           | 0.716778              |             |</pre>



<pre>| 10      | 30.00s       | DIVERGED          | DIVERGED              |             |</pre>



<pre>| RESET   | 31.15s       | 1.00899           | 0.717212              |             |</pre>



<pre>| 1       | 34.14s       | 1.00375           | 0.713414              |             |</pre>



<pre>| 2       | 37.09s       | 1.00071           | 0.710531              |             |</pre>



<pre>| 3       | 40.04s       | 0.999623          | 0.708959              |             |</pre>



<pre>| 4       | 43.02s       | 0.999166          | 0.707771              |             |</pre>



<pre>| 5       | 45.99s       | 0.999128          | 0.706799              |             |</pre>



<pre>| 6       | 48.98s       | 0.999573          | 0.706194              |             |</pre>



<pre>| 7       | 52.03s       | 1.00041           | 0.705812              |             |</pre>



<pre>| 8       | 55.05s       | 1.00129           | 0.705521              |             |</pre>



<pre>| 9       | 58.24s       | 1.00227           | 0.705182              |             |</pre>



<pre>| 10      | 1m 1s        | 1.0035            | 0.705001              |             |</pre>



<pre>| 11      | 1m 4s        | 1.00478           | 0.704885              |             |</pre>



<pre>| 12      | 1m 7s        | 1.00631           | 0.704885              |             |</pre>



<pre>| 13      | 1m 10s       | 1.00787           | 0.704933              |             |</pre>



<pre>| 14      | 1m 13s       | 1.00976           | 0.705163              |             |</pre>



<pre>| 15      | 1m 16s       | 1.01188           | 0.705441              |             |</pre>



<pre>| 16      | 1m 19s       | 1.01412           | 0.70585               |             |</pre>



<pre>| 17      | 1m 22s       | 1.01647           | 0.706341              |             |</pre>



<pre>| 18      | 1m 25s       | 1.01901           | 0.706932              |             |</pre>



<pre>| 19      | 1m 30s       | 1.02165           | 0.707611              |             |</pre>



<pre>| 20      | 1m 34s       | 1.02429           | 0.708333              |             |</pre>



<pre>+---------+--------------+-------------------+-----------------------+-------------+</pre>



<pre>Optimization Complete: Maximum number of passes through the data reached (hard limit).</pre>



<pre>Computing final objective value and training RMSE.</pre>



<pre>       Final objective value: 1.02569</pre>



<pre>       Final training RMSE: 0.708689</pre>



<pre>recommendations finished on 1000/32830 queries. users per second: 1084.07</pre>



<pre>recommendations finished on 2000/32830 queries. users per second: 1075.3</pre>



<pre>recommendations finished on 3000/32830 queries. users per second: 1064.78</pre>



<pre>recommendations finished on 4000/32830 queries. users per second: 1064.12</pre>



<pre>recommendations finished on 5000/32830 queries. users per second: 1063.26</pre>



<pre>recommendations finished on 6000/32830 queries. users per second: 1060.44</pre>



<pre>recommendations finished on 7000/32830 queries. users per second: 1059.55</pre>



<pre>recommendations finished on 8000/32830 queries. users per second: 1054.97</pre>



<pre>recommendations finished on 9000/32830 queries. users per second: 1049.83</pre>



<pre>recommendations finished on 10000/32830 queries. users per second: 1049.5</pre>



<pre>recommendations finished on 11000/32830 queries. users per second: 1049.23</pre>



<pre>recommendations finished on 12000/32830 queries. users per second: 1048.45</pre>



<pre>recommendations finished on 13000/32830 queries. users per second: 1049.83</pre>



<pre>recommendations finished on 14000/32830 queries. users per second: 1049.28</pre>



<pre>recommendations finished on 15000/32830 queries. users per second: 1049.98</pre>



<pre>recommendations finished on 16000/32830 queries. users per second: 1049.97</pre>



<pre>recommendations finished on 17000/32830 queries. users per second: 1050.48</pre>



<pre>recommendations finished on 18000/32830 queries. users per second: 1050.82</pre>



<pre>recommendations finished on 19000/32830 queries. users per second: 1051.52</pre>



<pre>recommendations finished on 20000/32830 queries. users per second: 1051.99</pre>



<pre>recommendations finished on 21000/32830 queries. users per second: 1051.41</pre>



<pre>recommendations finished on 22000/32830 queries. users per second: 1051.29</pre>



<pre>recommendations finished on 23000/32830 queries. users per second: 1051.32</pre>



<pre>recommendations finished on 24000/32830 queries. users per second: 1050.02</pre>



<pre>recommendations finished on 25000/32830 queries. users per second: 1050.23</pre>



<pre>recommendations finished on 26000/32830 queries. users per second: 1050.6</pre>



<pre>recommendations finished on 27000/32830 queries. users per second: 1041.75</pre>



<pre>recommendations finished on 28000/32830 queries. users per second: 1031.57</pre>



<pre>recommendations finished on 29000/32830 queries. users per second: 1023.42</pre>



<pre>recommendations finished on 30000/32830 queries. users per second: 1014.01</pre>



<pre>recommendations finished on 31000/32830 queries. users per second: 986.963</pre>



<pre>recommendations finished on 32000/32830 queries. users per second: 940.168</pre>


    
    Precision and recall summary statistics by cutoff
    +--------+-----------------+------------------+
    | cutoff |  mean_precision |   mean_recall    |
    +--------+-----------------+------------------+
    |   1    | 0.0385259631491 | 0.00257976781166 |
    |   2    |  0.036013400335 | 0.00381568399893 |
    |   3    | 0.0335008375209 | 0.00502701439815 |
    |   4    |  0.035594639866 | 0.00788294807732 |
    |   5    | 0.0355108877722 |  0.010973850492  |
    |   6    |  0.035175879397 | 0.0123863217622  |
    |   7    | 0.0356544627901 | 0.0156718652408  |
    |   8    |  0.035594639866 | 0.0214525470472  |
    |   9    |  0.036292573981 | 0.0273290733644  |
    |   10   | 0.0356783919598 | 0.0293587353987  |
    +--------+-----------------+------------------+
    [10 rows x 3 columns]
    
    ('\nOverall RMSE: ', 0.682608698505078)
    
    Per User RMSE (best)
    +--------------------+-------+------------------+
    | review_profilename | count |       rmse       |
    +--------------------+-------+------------------+
    |       churry       |   1   | 0.00338116178882 |
    +--------------------+-------+------------------+
    [1 rows x 3 columns]
    
    
    Per User RMSE (worst)
    +--------------------+-------+---------------+
    | review_profilename | count |      rmse     |
    +--------------------+-------+---------------+
    |  BlueShirtMember   |   1   | 3.13824451289 |
    +--------------------+-------+---------------+
    [1 rows x 3 columns]
    
    
    Per Item RMSE (best)
    +-------------------------------+-------+-------------------+
    |           beer_name           | count |        rmse       |
    +-------------------------------+-------+-------------------+
    | Cuir (100% Bourbon Barrel ... |   1   | 0.000438262087311 |
    +-------------------------------+-------+-------------------+
    [1 rows x 3 columns]
    
    
    Per Item RMSE (worst)
    +---------------+-------+---------------+
    |   beer_name   | count |      rmse     |
    +---------------+-------+---------------+
    | Texas Tornado |   1   | 3.43595071754 |
    +---------------+-------+---------------+
    [1 rows x 3 columns]
    
    


```python
print rmse_results['rmse_by_user']
```

    +--------------------+-------+----------------+
    | review_profilename | count |      rmse      |
    +--------------------+-------+----------------+
    |  beerandcycling88  |   31  | 0.578938242543 |
    |    redblacks75     |   4   |  0.3909401147  |
    |      keith712      |   4   | 0.849652257291 |
    |     rickcampie     |   4   | 0.262216774602 |
    |       jgagne       |   8   | 0.474924373971 |
    |    SchmichaelJ     |   16  | 0.459888250176 |
    |     TheKelsey      |   1   | 0.667257625287 |
    |      keethrax      |   3   | 0.518599200294 |
    |       iddqd        |   1   | 0.390430205313 |
    |     DarthMalt      |   31  |  1.0286333728  |
    +--------------------+-------+----------------+
    [597 rows x 3 columns]
    Note: Only the head of the SFrame is printed.
    You can use print_rows(num_rows=m, num_columns=n) to print more rows and columns.
    


```python
print rmse_results['rmse_by_item']
```

    +--------------------------------+-------+----------------+
    |           beer_name            | count |      rmse      |
    +--------------------------------+-------+----------------+
    |   XS Imperial India Pale Ale   |   3   | 0.547998758436 |
    |     Fantôme Brise-BonBons      |   1   | 0.317487100972 |
    |  Smuttynose Old Brown Dog Ale  |   4   | 0.42437606394  |
    | Summit 90/- Scottish Style Ale |   1   | 0.295787403363 |
    |        Staropramen Dark        |   1   | 0.979192631824 |
    |    Dark Horizon 3rd Edition    |   1   | 0.315892054687 |
    |      Foster's Premium Ale      |   4   | 0.968118277418 |
    |      Mother Of All Storms      |   2   | 0.386009308445 |
    |  Heine Brothers Coffee Stout   |   1   | 0.178993231293 |
    |        Tallgrass Wheat         |   1   | 1.15430376366  |
    +--------------------------------+-------+----------------+
    [4305 rows x 3 columns]
    Note: Only the head of the SFrame is printed.
    You can use print_rows(num_rows=m, num_columns=n) to print more rows and columns.
    


```python
print rmse_results['rmse_overall']
```

    0.682608698505
    


```python
import graphlab.aggregate as agg
agg_list = [agg.AVG('precision'), agg.STD('precision'), agg.AVG('recall'), agg.STD('recall')]
rmse_results['precision_recall_by_user'].groupby('cutoff', agg_list)
```




<div style="max-height:1000px;max-width:1500px;overflow:auto;"><table frame="box" rules="cols">
    <tr>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">cutoff</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Avg of precision</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Stdv of precision</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Avg of recall</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Stdv of recall</th>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">16</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0307788944724</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0819829905763</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0392590328097</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.144282601322</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">10</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0356783919598</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0986512923017</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0293587353987</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.123759549637</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">36</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0261027359017</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0603486642753</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0762793963869</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.194685181467</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">26</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.02802473908</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.068398268088</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0555523755653</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.169767466715</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">41</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0247987907015</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0571159237705</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0824651270418</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.200921629684</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0335008375209</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.127955366054</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.00502701439815</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0349635231563</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0385259631491</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.192462238666</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.00257976781166</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0252162871503</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">6</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.035175879397</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.106857519441</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0123863217622</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0708947827859</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">11</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0345667732602</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0953452982825</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0321629617502</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.130590574446</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.036013400335</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.147427476381</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.00381568399893</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0281106570263</td>
    </tr>
</table>
[18 rows x 5 columns]<br/>Note: Only the head of the SFrame is printed.<br/>You can use print_rows(num_rows=m, num_columns=n) to print more rows and columns.
</div>



### Item Item 

- Next, we try item an item-item recommendation system using cosine similarity and the automatic training method. The results are much better than the previous base model. Using one selection the model has a 10% chance of choosing a beer correctly. Strangely enough the RMSE has also increased. So, the variation between the expected vs. observed was worse but precision and recall increased. We have a precision of around 9-10% for the first 3 recommendations.


```python
item_item = gl.recommender.item_similarity_recommender.create(train, user_id='review_profilename' ,item_id='beer_name',
                                                              target= 'review_overall',only_top_k=3,similarity_type='cosine')
results = item_item.get_similar_items(k=3)
rmse_results1 = item_item.evaluate(test)
results.head()
```


<pre>Recsys training: model = item_similarity</pre>



<pre>Warning: Ignoring columns brewery_id, brewery_name, review_time, review_aroma, review_appearance, beer_style, review_palate, review_taste, beer_abv, beer_beerid;</pre>



<pre>    To use these columns in scoring predictions, use a model that allows the use of additional features.</pre>



<pre>Preparing data set.</pre>



<pre>    Data has 1509514 observations with 32830 users and 44032 items.</pre>



<pre>    Data prepared in: 0.917939s</pre>



<pre>Training model from provided data.</pre>



<pre>Gathering per-item and per-user statistics.</pre>



<pre>+--------------------------------+------------+</pre>



<pre>| Elapsed Time (Item Statistics) | % Complete |</pre>



<pre>+--------------------------------+------------+</pre>



<pre>| 5.515ms                        | 3          |</pre>



<pre>| 16.043ms                       | 100        |</pre>



<pre>+--------------------------------+------------+</pre>



<pre>Setting up lookup tables.</pre>



<pre>Processing data in one pass using dense lookup tables.</pre>



<pre>+-------------------------------------+------------------+-----------------+</pre>



<pre>| Elapsed Time (Constructing Lookups) | Total % Complete | Items Processed |</pre>



<pre>+-------------------------------------+------------------+-----------------+</pre>



<pre>| 2.03s                               | 0                | 0               |</pre>



<pre>| 3.05s                               | 24               | 10604           |</pre>



<pre>| 4.04s                               | 46.5             | 20564           |</pre>



<pre>| 5.03s                               | 67.5             | 29821           |</pre>



<pre>| 6.07s                               | 85.5             | 37707           |</pre>



<pre>| 7.06s                               | 94.5             | 41655           |</pre>



<pre>| 11.35s                              | 100              | 44032           |</pre>



<pre>+-------------------------------------+------------------+-----------------+</pre>



<pre>Finalizing lookup tables.</pre>



<pre>Generating candidate set for working with new users.</pre>



<pre>Finished training in 11.3983s</pre>


    
    Precision and recall summary statistics by cutoff
    +--------+-----------------+-----------------+
    | cutoff |  mean_precision |   mean_recall   |
    +--------+-----------------+-----------------+
    |   1    |  0.108877721943 | 0.0169700087959 |
    |   2    | 0.0996649916248 | 0.0266026404115 |
    |   3    |  0.102177554439 | 0.0369474496913 |
    |   4    | 0.0975711892797 | 0.0440187250152 |
    |   5    | 0.0931323283082 | 0.0493152413701 |
    |   6    | 0.0912897822446 |  0.052246520015 |
    |   7    | 0.0899736779134 | 0.0564323699827 |
    |   8    | 0.0860552763819 | 0.0611713855881 |
    |   9    | 0.0837520938023 | 0.0640216632504 |
    |   10   | 0.0825795644891 | 0.0673860537351 |
    +--------+-----------------+-----------------+
    [10 rows x 3 columns]
    
    ('\nOverall RMSE: ', 3.8895012676868337)
    
    Per User RMSE (best)
    +--------------------+-------+----------------+
    | review_profilename | count |      rmse      |
    +--------------------+-------+----------------+
    |     AxelTheRed     |   1   | 0.155018925667 |
    +--------------------+-------+----------------+
    [1 rows x 3 columns]
    
    
    Per User RMSE (worst)
    +--------------------+-------+------+
    | review_profilename | count | rmse |
    +--------------------+-------+------+
    |      DonaCake      |   1   | 5.0  |
    +--------------------+-------+------+
    [1 rows x 3 columns]
    
    
    Per Item RMSE (best)
    +-------------------------------+-------+----------------+
    |           beer_name           | count |      rmse      |
    +-------------------------------+-------+----------------+
    | The Devil Made Me Do It! C... |   1   | 0.999174810122 |
    +-------------------------------+-------+----------------+
    [1 rows x 3 columns]
    
    
    Per Item RMSE (worst)
    +----------------+-------+------+
    |   beer_name    | count | rmse |
    +----------------+-------+------+
    | Amarillo Amber |   1   | 5.0  |
    +----------------+-------+------+
    [1 rows x 3 columns]
    
    




<div style="max-height:1000px;max-width:1500px;overflow:auto;"><table frame="box" rules="cols">
    <tr>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">beer_name</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">similar</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">score</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">rank</th>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Sausa Weizen</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Red Moon</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Sausa Weizen</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Black Horse Black Beer</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Sausa Weizen</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Sausa Pils</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Red Moon</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Sausa Weizen</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Red Moon</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Black Horse Black Beer</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Red Moon</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Sausa Pils</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Black Horse Black Beer</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Sausa Weizen</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Black Horse Black Beer</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Red Moon</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Black Horse Black Beer</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Sausa Pils</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Sausa Pils</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Sausa Weizen</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1.0</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1</td>
    </tr>
</table>
[10 rows x 4 columns]<br/>
</div>




```python
print rmse_results1['rmse_by_user']
```

    +--------------------+-------+---------------+
    | review_profilename | count |      rmse     |
    +--------------------+-------+---------------+
    |  beerandcycling88  |   31  | 3.88563848507 |
    |    redblacks75     |   4   | 4.38035386698 |
    |      keith712      |   4   | 4.42376123338 |
    |     rickcampie     |   4   |  3.6698065441 |
    |       jgagne       |   8   | 4.13555121574 |
    |    SchmichaelJ     |   16  | 3.93254966609 |
    |     TheKelsey      |   1   |      4.5      |
    |      keethrax      |   3   | 4.33973885543 |
    |       iddqd        |   1   |      3.5      |
    |     DarthMalt      |   31  | 3.60726040509 |
    +--------------------+-------+---------------+
    [597 rows x 3 columns]
    Note: Only the head of the SFrame is printed.
    You can use print_rows(num_rows=m, num_columns=n) to print more rows and columns.
    


```python
print rmse_results1['rmse_by_item']
```

    +--------------------------------+-------+---------------+
    |           beer_name            | count |      rmse     |
    +--------------------------------+-------+---------------+
    |   XS Imperial India Pale Ale   |   3   | 4.31629332127 |
    |     Fantôme Brise-BonBons      |   1   | 3.49636409717 |
    |  Smuttynose Old Brown Dog Ale  |   4   | 3.87497253152 |
    | Summit 90/- Scottish Style Ale |   1   | 3.47432802926 |
    |        Staropramen Dark        |   1   |      3.0      |
    |    Dark Horizon 3rd Edition    |   1   |      4.5      |
    |      Foster's Premium Ale      |   4   | 3.06186217848 |
    |      Mother Of All Storms      |   2   | 3.74942802657 |
    |  Heine Brothers Coffee Stout   |   1   |      4.0      |
    |        Tallgrass Wheat         |   1   |      2.5      |
    +--------------------------------+-------+---------------+
    [4305 rows x 3 columns]
    Note: Only the head of the SFrame is printed.
    You can use print_rows(num_rows=m, num_columns=n) to print more rows and columns.
    


```python
agg_list = [agg.AVG('precision'), agg.STD('precision'), agg.AVG('recall'), agg.STD('recall')]
rmse_results1['precision_recall_by_user'].groupby('cutoff', agg_list)
```




<div style="max-height:1000px;max-width:1500px;overflow:auto;"><table frame="box" rules="cols">
    <tr>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">cutoff</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Avg of precision</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Stdv of precision</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Avg of recall</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Stdv of recall</th>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">16</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0718174204355</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.139677725496</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0851225971046</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.187422373695</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">10</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0825795644891</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.162161010783</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0673860537351</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.171017992637</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">36</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0539270426205</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.110041309436</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.119875269871</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.212455345764</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">26</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0604947816003</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.119985995094</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.108894430178</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.208645823504</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">41</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0507823671202</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.103551132746</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.125222150812</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.214515265218</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.102177554439</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.217811271459</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0369474496913</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.141286469295</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.108877721943</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.311485735801</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0169700087959</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.106013687987</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">6</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0912897822446</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.178644086451</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.052246520015</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.158081192459</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">11</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0820770519263</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.156372505296</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.074678672209</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.178208683268</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0996649916248</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.236246234</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0266026404115</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.124940734242</td>
    </tr>
</table>
[18 rows x 5 columns]<br/>Note: Only the head of the SFrame is printed.<br/>You can use print_rows(num_rows=m, num_columns=n) to print more rows and columns.
</div>



### Ranking Factorization Recommender
- Next we test the Ranking Factorization Recommender system. This also didn’t perform that well, the RMSE was between 2.5 and .0001 so there was a smaller range than previously observed but the average precision and recall is still much lower than the item-item system. 


```python
rank_fact = gl.recommender.ranking_factorization_recommender.create(train, user_id='review_profilename' ,item_id='beer_name',
                                                              target= 'review_overall',num_factors = 30)
rmse_results2 = rank_fact.evaluate(test)
```


<pre>Recsys training: model = ranking_factorization_recommender</pre>



<pre>Preparing data set.</pre>



<pre>    Data has 1509514 observations with 32830 users and 44032 items.</pre>



<pre>    Data prepared in: 2.67265s</pre>



<pre>Training ranking_factorization_recommender for recommendations.</pre>



<pre>+--------------------------------+--------------------------------------------------+----------+</pre>



<pre>| Parameter                      | Description                                      | Value    |</pre>



<pre>+--------------------------------+--------------------------------------------------+----------+</pre>



<pre>| num_factors                    | Factor Dimension                                 | 2        |</pre>



<pre>| regularization                 | L2 Regularization on Factors                     | 1e-009   |</pre>



<pre>| solver                         | Solver used for training                         | adagrad  |</pre>



<pre>| linear_regularization          | L2 Regularization on Linear Coefficients         | 1e-009   |</pre>



<pre>| ranking_regularization         | Rank-based Regularization Weight                 | 0.25     |</pre>



<pre>| max_iterations                 | Maximum Number of Iterations                     | 25       |</pre>



<pre>+--------------------------------+--------------------------------------------------+----------+</pre>



<pre>  Optimizing model using SGD; tuning step size.</pre>



<pre>  Using 188689 / 1509514 points for tuning the step size.</pre>



<pre>+---------+-------------------+------------------------------------------+</pre>



<pre>| Attempt | Initial Step Size | Estimated Objective Value                |</pre>



<pre>+---------+-------------------+------------------------------------------+</pre>



<pre>| 0       | 4.16667           | Not Viable                               |</pre>



<pre>| 1       | 1.04167           | Not Viable                               |</pre>



<pre>| 2       | 0.260417          | Not Viable                               |</pre>



<pre>| 3       | 0.0651042         | Not Viable                               |</pre>



<pre>| 4       | 0.016276          | No Decrease (1.44445 >= 1.00711)         |</pre>



<pre>| 5       | 0.00406901        | 0.943218                                 |</pre>



<pre>| 6       | 0.00203451        | 0.646173                                 |</pre>



<pre>| 7       | 0.00101725        | 0.811328                                 |</pre>



<pre>| 8       | 0.000508626       | 0.826207                                 |</pre>



<pre>| 9       | 0.000254313       | 0.874448                                 |</pre>



<pre>+---------+-------------------+------------------------------------------+</pre>



<pre>| Final   | 0.00203451        | 0.646173                                 |</pre>



<pre>+---------+-------------------+------------------------------------------+</pre>



<pre>Starting Optimization.</pre>



<pre>+---------+--------------+-------------------+-----------------------+-------------+</pre>



<pre>| Iter.   | Elapsed Time | Approx. Objective | Approx. Training RMSE | Step Size   |</pre>



<pre>+---------+--------------+-------------------+-----------------------+-------------+</pre>



<pre>| Initial | 501us        | 1.00967           | 0.717703              |             |</pre>



<pre>+---------+--------------+-------------------+-----------------------+-------------+</pre>



<pre>| 1       | 1.43s        | 0.702593          | 0.515686              | 0.00203451  |</pre>



<pre>| 2       | 2.85s        | 0.640341          | 0.517591              | 0.00203451  |</pre>



<pre>| 3       | 4.36s        | 0.624531          | 0.514327              | 0.00203451  |</pre>



<pre>| 4       | 5.82s        | 0.616023          | 0.512085              | 0.00203451  |</pre>



<pre>| 5       | 7.28s        | 0.609277          | 0.510864              | 0.00203451  |</pre>



<pre>| 6       | 8.73s        | 0.605235          | 0.510579              | 0.00203451  |</pre>



<pre>| 7       | 10.19s       | 0.600875          | 0.509939              | 0.00203451  |</pre>



<pre>| 8       | 11.63s       | 0.597015          | 0.51049               | 0.00203451  |</pre>



<pre>| 9       | 13.14s       | 0.594057          | 0.510221              | 0.00203451  |</pre>



<pre>| 10      | 14.59s       | 0.590948          | 0.509902              | 0.00203451  |</pre>



<pre>| 11      | 16.03s       | 0.589604          | 0.510714              | 0.00203451  |</pre>



<pre>| 12      | 17.49s       | 0.58707           | 0.511016              | 0.00203451  |</pre>



<pre>| 13      | 18.97s       | 0.585837          | 0.511714              | 0.00203451  |</pre>



<pre>| 14      | 20.45s       | 0.583106          | 0.512339              | 0.00203451  |</pre>



<pre>| 15      | 21.97s       | 0.58222           | 0.512516              | 0.00203451  |</pre>



<pre>| 16      | 23.42s       | 0.580852          | 0.513146              | 0.00203451  |</pre>



<pre>| 17      | 24.92s       | 0.580902          | 0.514443              | 0.00203451  |</pre>



<pre>| 18      | 26.42s       | 0.579566          | 0.515092              | 0.00203451  |</pre>



<pre>| 19      | 27.85s       | 0.579009          | 0.516441              | 0.00203451  |</pre>



<pre>| 20      | 29.31s       | 0.57787           | 0.517097              | 0.00203451  |</pre>



<pre>| 21      | 30.86s       | 0.579148          | 0.518666              | 0.00203451  |</pre>



<pre>| 22      | 32.34s       | 0.577875          | 0.519538              | 0.00203451  |</pre>



<pre>| 23      | 33.84s       | 0.576993          | 0.52061               | 0.00203451  |</pre>



<pre>| 24      | 35.37s       | 0.579366          | 0.522702              | 0.00203451  |</pre>



<pre>| 25      | 36.85s       | 0.578581          | 0.523914              | 0.00203451  |</pre>



<pre>+---------+--------------+-------------------+-----------------------+-------------+</pre>



<pre>Optimization Complete: Maximum number of passes through the data reached.</pre>



<pre>Computing final objective value and training RMSE.</pre>



<pre>       Final objective value: 0.581038</pre>



<pre>       Final training RMSE: 0.525197</pre>


    
    Precision and recall summary statistics by cutoff
    +--------+-----------------+------------------+
    | cutoff |  mean_precision |   mean_recall    |
    +--------+-----------------+------------------+
    |   1    | 0.0402010050251 | 0.00346772190364 |
    |   2    | 0.0435510887772 | 0.00561252618396 |
    |   3    | 0.0446677833613 | 0.00746177151256 |
    |   4    | 0.0452261306533 | 0.00999651953163 |
    |   5    | 0.0465661641541 | 0.0152867115226  |
    |   6    | 0.0441094360692 | 0.0178029339018  |
    |   7    | 0.0445082555635 | 0.0198098216245  |
    |   8    | 0.0431323283082 | 0.0222076737324  |
    |   9    | 0.0431788572492 | 0.0242972994549  |
    |   10   | 0.0438860971524 | 0.0286593255475  |
    +--------+-----------------+------------------+
    [10 rows x 3 columns]
    
    ('\nOverall RMSE: ', 0.5199147228208264)
    
    Per User RMSE (best)
    +--------------------+-------+------------------+
    | review_profilename | count |       rmse       |
    +--------------------+-------+------------------+
    |  aquariumdrinker   |   1   | 0.00418499380506 |
    +--------------------+-------+------------------+
    [1 rows x 3 columns]
    
    
    Per User RMSE (worst)
    +--------------------+-------+---------------+
    | review_profilename | count |      rmse     |
    +--------------------+-------+---------------+
    |       Mecham       |   1   | 2.05942761443 |
    +--------------------+-------+---------------+
    [1 rows x 3 columns]
    
    
    Per Item RMSE (best)
    +---------------------+-------+------------------+
    |      beer_name      | count |       rmse       |
    +---------------------+-------+------------------+
    | Shiner Dunkelweizen |   1   | 0.00142402897359 |
    +---------------------+-------+------------------+
    [1 rows x 3 columns]
    
    
    Per Item RMSE (worst)
    +---------------+-------+---------------+
    |   beer_name   | count |      rmse     |
    +---------------+-------+---------------+
    | Texas Tornado |   1   | 2.53148181401 |
    +---------------+-------+---------------+
    [1 rows x 3 columns]
    
    


```python
rmse_results2['precision_recall_by_user'].groupby('cutoff', agg_list)
```




<div style="max-height:1000px;max-width:1500px;overflow:auto;"><table frame="box" rules="cols">
    <tr>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">cutoff</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Avg of precision</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Stdv of precision</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Avg of recall</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Stdv of recall</th>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">16</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.037269681742</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0943227164735</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0458633808291</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.146594763402</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">10</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0438860971524</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.116554271689</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0286593255475</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.105650373585</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">36</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0294062907128</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0712241526907</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0771129504292</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.189121114885</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">26</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0325344672078</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0819123863485</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0584624679707</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.160020647399</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">41</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0285574212526</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0680741464015</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0852627644602</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.19820534174</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0446677833613</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.148996102131</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.00746177151256</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0503568573989</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0402010050251</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.19643035463</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.00346772190364</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0436957517736</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">6</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0441094360692</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.128735683352</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0178029339018</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0922718719453</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">11</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0426374295721</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.1109154512</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0339869522519</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.12223844155</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0435510887772</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.157809925807</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.00561252618396</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0473963907542</td>
    </tr>
</table>
[18 rows x 5 columns]<br/>Note: Only the head of the SFrame is printed.<br/>You can use print_rows(num_rows=m, num_columns=n) to print more rows and columns.
</div>



### Factorization Recommender
 - Here we try just a factorization recommender system, which also preforms poorly. It has an average precision about .35 for all cutoff and an average recall around .4. Again the item-item recommender out preformed this system


```python
item_content = gl.recommender.factorization_recommender.create(train, user_id='review_profilename' ,item_id='beer_name',
                                                              target= 'review_overall')

rmse_results3 = item_content.evaluate(test)
```


<pre>Recsys training: model = factorization_recommender</pre>



<pre>Preparing data set.</pre>



<pre>    Data has 1509514 observations with 32830 users and 44032 items.</pre>



<pre>    Data prepared in: 2.58549s</pre>



<pre>Training factorization_recommender for recommendations.</pre>



<pre>+--------------------------------+--------------------------------------------------+----------+</pre>



<pre>| Parameter                      | Description                                      | Value    |</pre>



<pre>+--------------------------------+--------------------------------------------------+----------+</pre>



<pre>| num_factors                    | Factor Dimension                                 | 8        |</pre>



<pre>| regularization                 | L2 Regularization on Factors                     | 1e-008   |</pre>



<pre>| solver                         | Solver used for training                         | adagrad  |</pre>



<pre>| linear_regularization          | L2 Regularization on Linear Coefficients         | 1e-010   |</pre>



<pre>| max_iterations                 | Maximum Number of Iterations                     | 50       |</pre>



<pre>+--------------------------------+--------------------------------------------------+----------+</pre>



<pre>  Optimizing model using SGD; tuning step size.</pre>



<pre>  Using 188689 / 1509514 points for tuning the step size.</pre>



<pre>+---------+-------------------+------------------------------------------+</pre>



<pre>| Attempt | Initial Step Size | Estimated Objective Value                |</pre>



<pre>+---------+-------------------+------------------------------------------+</pre>



<pre>| 0       | 4.16667           | Not Viable                               |</pre>



<pre>| 1       | 1.04167           | Not Viable                               |</pre>



<pre>| 2       | 0.260417          | Not Viable                               |</pre>



<pre>| 3       | 0.0651042         | Not Viable                               |</pre>



<pre>| 4       | 0.016276          | Not Viable                               |</pre>



<pre>| 5       | 0.00406901        | No Decrease (0.685986 >= 0.515925)       |</pre>



<pre>| 6       | 0.00101725        | No Decrease (1.14399 >= 0.515925)        |</pre>



<pre>| 7       | 0.000254313       | No Decrease (1.11878 >= 0.515925)        |</pre>



<pre>| 8       | 6.35783e-005      | 0.493291                                 |</pre>



<pre>| 9       | 3.17891e-005      | 0.475473                                 |</pre>



<pre>| 10      | 1.58946e-005      | 0.489317                                 |</pre>



<pre>| 11      | 7.94729e-006      | 0.501046                                 |</pre>



<pre>| 12      | 3.97364e-006      | 0.508301                                 |</pre>



<pre>+---------+-------------------+------------------------------------------+</pre>



<pre>| Final   | 3.17891e-005      | 0.475473                                 |</pre>



<pre>+---------+-------------------+------------------------------------------+</pre>



<pre>Starting Optimization.</pre>



<pre>+---------+--------------+-------------------+-----------------------+-------------+</pre>



<pre>| Iter.   | Elapsed Time | Approx. Objective | Approx. Training RMSE | Step Size   |</pre>



<pre>+---------+--------------+-------------------+-----------------------+-------------+</pre>



<pre>| Initial | 0us          | 0.515099          | 0.717704              |             |</pre>



<pre>+---------+--------------+-------------------+-----------------------+-------------+</pre>



<pre>| 1       | 529.408ms    | 0.479024          | 0.692116              |             |</pre>



<pre>| 2       | 1.02s        | 0.473154          | 0.687862              |             |</pre>



<pre>| 3       | 1.52s        | 0.487246          | 0.69803               |             |</pre>



<pre>| 4       | 2.11s        | 0.507809          | 0.712607              |             |</pre>



<pre>| 5       | 2.62s        | 0.532342          | 0.729618              |             |</pre>



<pre>| 6       | 3.12s        | 0.559725          | 0.748148              |             |</pre>



<pre>| 10      | 5.45s        | DIVERGED          | DIVERGED              |             |</pre>



<pre>| RESET   | 5.59s        | 0.515606          | 0.718057              |             |</pre>



<pre>| 1       | 6.12s        | 0.494167          | 0.70297               |             |</pre>



<pre>| 2       | 6.67s        | 0.480935          | 0.693495              |             |</pre>



<pre>| 5       | 8.27s        | 0.474238          | 0.68865               |             |</pre>



<pre>| 10      | 11.15s       | 0.496832          | 0.704863              |             |</pre>



<pre>| 15      | 14.09s       | 0.534049          | 0.730786              |             |</pre>



<pre>| 18      | 15.97s       | DIVERGED          | DIVERGED              |             |</pre>



<pre>| RESET   | 16.12s       | 0.51571           | 0.71813               |             |</pre>



<pre>| 2       | 17.44s       | 0.49496           | 0.703534              |             |</pre>



<pre>| 7       | 20.72s       | 0.47872           | 0.691896              |             |</pre>



<pre>| 12      | 23.73s       | 0.473344          | 0.688                 |             |</pre>



<pre>| 17      | 26.75s       | 0.473587          | 0.688177              |             |</pre>



<pre>| 22      | 29.76s       | 0.477777          | 0.691214              |             |</pre>



<pre>| 25      | 31.76s       | 0.481407          | 0.693835              |             |</pre>



<pre>| 27      | 33.04s       | 0.484218          | 0.695857              |             |</pre>



<pre>+---------+--------------+-------------------+-----------------------+-------------+</pre>



<pre>Optimization Complete: Maximum number of passes through the data reached (hard limit).</pre>



<pre>Computing final objective value and training RMSE.</pre>



<pre>       Final objective value: 0.485017</pre>



<pre>       Final training RMSE: 0.696432</pre>


    
    Precision and recall summary statistics by cutoff
    +--------+-----------------+------------------+
    | cutoff |  mean_precision |   mean_recall    |
    +--------+-----------------+------------------+
    |   1    | 0.0402010050251 | 0.00352161550262 |
    |   2    |  0.035175879397 | 0.0053751621869  |
    |   3    |  0.035734226689 | 0.00765664203118 |
    |   4    |  0.036013400335 | 0.00927929525624 |
    |   5    |  0.036850921273 |  0.010527499824  |
    |   6    |  0.036292573981 | 0.0124957749667  |
    |   7    | 0.0366116295765 |  0.014274622191  |
    |   8    | 0.0366415410385 |  0.01726186892   |
    |   9    |  0.035734226689 | 0.0180129514551  |
    |   10   | 0.0361809045226 | 0.0221705309116  |
    +--------+-----------------+------------------+
    [10 rows x 3 columns]
    
    ('\nOverall RMSE: ', 0.6722797927364667)
    
    Per User RMSE (best)
    +--------------------+-------+------------------+
    | review_profilename | count |       rmse       |
    +--------------------+-------+------------------+
    |      davec004      |   1   | 0.00659887407111 |
    +--------------------+-------+------------------+
    [1 rows x 3 columns]
    
    
    Per User RMSE (worst)
    +--------------------+-------+--------------+
    | review_profilename | count |     rmse     |
    +--------------------+-------+--------------+
    |  BlueShirtMember   |   1   | 3.2963741857 |
    +--------------------+-------+--------------+
    [1 rows x 3 columns]
    
    
    Per Item RMSE (best)
    +---------------+-------+-------------------+
    |   beer_name   | count |        rmse       |
    +---------------+-------+-------------------+
    | Zywiec Porter |   1   | 0.000983048433277 |
    +---------------+-------+-------------------+
    [1 rows x 3 columns]
    
    
    Per Item RMSE (worst)
    +---------------+-------+---------------+
    |   beer_name   | count |      rmse     |
    +---------------+-------+---------------+
    | Texas Tornado |   1   | 3.80472434065 |
    +---------------+-------+---------------+
    [1 rows x 3 columns]
    
    

### Visualization 

- Here we group them together and plot them out. For some reason I was unable to get matplotlib to run with graphlab and I tried uninstalling reinstalling, it seems to be a known problem too. So the plots are provided in another attachment. They depict the item-item system outperforming both the Ranking factorization and the factorization recommender systems.



```python
compare_struct = gl.compare(test,[item_item, rank_fact, model])
```

    PROGRESS: Evaluate model M0
    
    Precision and recall summary statistics by cutoff
    +--------+-----------------+-----------------+
    | cutoff |  mean_precision |   mean_recall   |
    +--------+-----------------+-----------------+
    |   1    |  0.108877721943 | 0.0169700087959 |
    |   2    | 0.0996649916248 | 0.0266026404115 |
    |   3    |  0.102177554439 | 0.0369474496913 |
    |   4    | 0.0979899497487 | 0.0442978986612 |
    |   5    | 0.0931323283082 | 0.0493152413701 |
    |   6    | 0.0912897822446 |  0.052246520015 |
    |   7    | 0.0899736779134 | 0.0564323699827 |
    |   8    | 0.0860552763819 | 0.0611713855881 |
    |   9    | 0.0837520938023 | 0.0640216632504 |
    |   10   | 0.0825795644891 | 0.0673860537351 |
    +--------+-----------------+-----------------+
    [10 rows x 3 columns]
    
    PROGRESS: Evaluate model M1
    
    Precision and recall summary statistics by cutoff
    +--------+-----------------+------------------+
    | cutoff |  mean_precision |   mean_recall    |
    +--------+-----------------+------------------+
    |   1    | 0.0402010050251 | 0.00346772190364 |
    |   2    | 0.0435510887772 | 0.00561252618396 |
    |   3    | 0.0446677833613 | 0.00746177151256 |
    |   4    | 0.0452261306533 | 0.00999651953163 |
    |   5    | 0.0465661641541 | 0.0152867115226  |
    |   6    | 0.0441094360692 | 0.0178029339018  |
    |   7    | 0.0445082555635 | 0.0198098216245  |
    |   8    | 0.0431323283082 | 0.0222076737324  |
    |   9    | 0.0431788572492 | 0.0242972994549  |
    |   10   | 0.0438860971524 | 0.0286593255475  |
    +--------+-----------------+------------------+
    [10 rows x 3 columns]
    
    PROGRESS: Evaluate model M2
    
    Precision and recall summary statistics by cutoff
    +--------+-----------------+------------------+
    | cutoff |  mean_precision |   mean_recall    |
    +--------+-----------------+------------------+
    |   1    | 0.0502512562814 | 0.00273725688411 |
    |   2    | 0.0435510887772 | 0.00786873443516 |
    |   3    | 0.0396426577331 |  0.011070034522  |
    |   4    |  0.036850921273 | 0.0124994585019  |
    |   5    | 0.0358458961474 | 0.0153672437708  |
    |   6    |  0.034059184813 | 0.0162735393075  |
    |   7    |  0.032304379038 | 0.0176382691919  |
    |   8    | 0.0322445561139 | 0.0208971020424  |
    |   9    | 0.0325702587009 |  0.022135519795  |
    |   10   | 0.0323283082077 | 0.0243938437446  |
    +--------+-----------------+------------------+
    [10 rows x 3 columns]
    
    Model compare metric: precision_recall
    


```python
#import matplotlib 
#import matplotlib.cbook # i cant get matplotlib to work inline, seems its a common bug on dato forums, i tried reinstalling 
#%matplotlib inline
#Error Message: 'AttributeError: 'module' object has no attribute 'cbook'
gl.show_comparison(compare_struct,[item_item, rank_fact, model])
```

    Canvas is accessible via web browser at the URL: http://localhost:52086/index.html
    Opening Canvas in default web browser.
    

- tried to create a grid search type thing with and item-item system but there isnt support, i probably could have done it with loops though


```python
#params = {'user_id' : 'review_profilename', 'item_id':'beer_name','target':'review_overall',
         #'similarity_type': ['jaccard','cosine','pearson'], 'threshold': [.001, .01], 'training_method':['auto', 'dense', 'sparse']}
#job = gl.model_parameter_search.create((train,test), gl.recommender.item_similarity_recommender.create,
                                      #params,
                                      #max_models = 9,
                                      #environment = None)
```

### Testing parameters

- So, I wanted to test parameters for the item-item matrix, so I tested different similarity types as well as the training method. For the similarity types I tested Jaccard, Cosine, and Pearson. The results didn’t fluctuate much. For the training method I tested auto, dense, and sparse and again there was no significant difference in the results. The output is shown below and can also be found in the other image I attached.



```python
item_item1 = gl.recommender.item_similarity_recommender.create(train, user_id='review_profilename' ,item_id='beer_name',
                                                              target= 'review_overall',only_top_k=3,similarity_type='jaccard')

rmse_results4 = item_item1.evaluate(test)

```


<pre>Recsys training: model = item_similarity</pre>



<pre>Warning: Ignoring columns brewery_id, brewery_name, review_time, review_aroma, review_appearance, beer_style, review_palate, review_taste, beer_abv, beer_beerid;</pre>



<pre>    To use these columns in scoring predictions, use a model that allows the use of additional features.</pre>



<pre>Preparing data set.</pre>



<pre>    Data has 1509514 observations with 32830 users and 44032 items.</pre>



<pre>    Data prepared in: 0.821719s</pre>



<pre>Training model from provided data.</pre>



<pre>Gathering per-item and per-user statistics.</pre>



<pre>+--------------------------------+------------+</pre>



<pre>| Elapsed Time (Item Statistics) | % Complete |</pre>



<pre>+--------------------------------+------------+</pre>



<pre>| 4.512ms                        | 3          |</pre>



<pre>| 15.542ms                       | 100        |</pre>



<pre>+--------------------------------+------------+</pre>



<pre>Setting up lookup tables.</pre>



<pre>Processing data in one pass using dense lookup tables.</pre>



<pre>+-------------------------------------+------------------+-----------------+</pre>



<pre>| Elapsed Time (Constructing Lookups) | Total % Complete | Items Processed |</pre>



<pre>+-------------------------------------+------------------+-----------------+</pre>



<pre>| 1.88s                               | 0.25             | 135             |</pre>



<pre>| 2.88s                               | 31               | 13658           |</pre>



<pre>| 3.88s                               | 58.25            | 25667           |</pre>



<pre>| 4.88s                               | 83.25            | 36753           |</pre>



<pre>| 5.92s                               | 97.25            | 42858           |</pre>



<pre>| 9.12s                               | 100              | 44032           |</pre>



<pre>+-------------------------------------+------------------+-----------------+</pre>



<pre>Finalizing lookup tables.</pre>



<pre>Generating candidate set for working with new users.</pre>



<pre>Finished training in 9.16808s</pre>


    
    Precision and recall summary statistics by cutoff
    +--------+-----------------+-----------------+
    | cutoff |  mean_precision |   mean_recall   |
    +--------+-----------------+-----------------+
    |   1    |  0.12730318258  | 0.0200943219968 |
    |   2    |  0.115577889447 | 0.0326628996112 |
    |   3    |  0.102735901731 | 0.0381122205575 |
    |   4    | 0.0958961474037 | 0.0440197098846 |
    |   5    | 0.0907872696817 |  0.051158059538 |
    |   6    | 0.0876605248465 |  0.055261697583 |
    |   7    | 0.0859057190715 | 0.0588357871061 |
    |   8    | 0.0839614740369 | 0.0627022914731 |
    |   9    | 0.0813325888703 | 0.0656662792129 |
    |   10   | 0.0788944723618 | 0.0682574702034 |
    +--------+-----------------+-----------------+
    [10 rows x 3 columns]
    
    ('\nOverall RMSE: ', 3.897191762640845)
    
    Per User RMSE (best)
    +--------------------+-------+---------------+
    | review_profilename | count |      rmse     |
    +--------------------+-------+---------------+
    |     AxelTheRed     |   1   | 0.73851031065 |
    +--------------------+-------+---------------+
    [1 rows x 3 columns]
    
    
    Per User RMSE (worst)
    +--------------------+-------+------+
    | review_profilename | count | rmse |
    +--------------------+-------+------+
    |      DonaCake      |   1   | 5.0  |
    +--------------------+-------+------+
    [1 rows x 3 columns]
    
    
    Per Item RMSE (best)
    +-----------+-------+----------------+
    | beer_name | count |      rmse      |
    +-----------+-------+----------------+
    |   Biobok  |   1   | 0.997245179282 |
    +-----------+-------+----------------+
    [1 rows x 3 columns]
    
    
    Per Item RMSE (worst)
    +----------------+-------+------+
    |   beer_name    | count | rmse |
    +----------------+-------+------+
    | Amarillo Amber |   1   | 5.0  |
    +----------------+-------+------+
    [1 rows x 3 columns]
    
    


```python
rmse_results4['precision_recall_by_user'].groupby('cutoff', agg_list)
```




<div style="max-height:1000px;max-width:1500px;overflow:auto;"><table frame="box" rules="cols">
    <tr>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">cutoff</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Avg of precision</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Stdv of precision</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Avg of recall</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Stdv of recall</th>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">16</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0680485762144</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.137090499345</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0785707235125</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.179438189768</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">10</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0788944723618</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.156565260055</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0682574702034</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.174688788324</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">36</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0508561325144</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.104788918781</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.116669221851</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.210566039807</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">26</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.057595670661</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.117007932345</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.103938347775</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.204066290249</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">41</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.048739633125</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.101510323451</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.121975561422</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.212347534898</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.102735901731</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.211914681344</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0381122205575</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.143487408258</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.12730318258</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.333312289429</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0200943219968</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.110855248445</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">6</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0876605248465</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.171597573709</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.055261697583</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.167997766769</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">11</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0770519262982</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.15587435437</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.069302722703</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.174853422383</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.115577889447</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.255673071803</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0326628996112</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.139914990952</td>
    </tr>
</table>
[18 rows x 5 columns]<br/>Note: Only the head of the SFrame is printed.<br/>You can use print_rows(num_rows=m, num_columns=n) to print more rows and columns.
</div>




```python
item_item2 = gl.recommender.item_similarity_recommender.create(train, user_id='review_profilename' ,item_id='beer_name',
                                                              target= 'review_overall',only_top_k=4,similarity_type='jaccard',training_method = 'sparse')

rmse_results5 = item_item2.evaluate(test)
```


<pre>Recsys training: model = item_similarity</pre>



<pre>Warning: Ignoring columns brewery_id, brewery_name, review_time, review_aroma, review_appearance, beer_style, review_palate, review_taste, beer_abv, beer_beerid;</pre>



<pre>    To use these columns in scoring predictions, use a model that allows the use of additional features.</pre>



<pre>Preparing data set.</pre>



<pre>    Data has 1509514 observations with 32830 users and 44032 items.</pre>



<pre>    Data prepared in: 0.820681s</pre>



<pre>Training model from provided data.</pre>



<pre>Gathering per-item and per-user statistics.</pre>



<pre>+--------------------------------+------------+</pre>



<pre>| Elapsed Time (Item Statistics) | % Complete |</pre>



<pre>+--------------------------------+------------+</pre>



<pre>| 5.515ms                        | 3          |</pre>



<pre>| 14.539ms                       | 100        |</pre>



<pre>+--------------------------------+------------+</pre>



<pre>Setting up lookup tables.</pre>



<pre>Processing data in one pass using sparse lookup tables.</pre>



<pre>+-------------------------------------+------------------+-----------------+</pre>



<pre>| Elapsed Time (Constructing Lookups) | Total % Complete | Items Processed |</pre>



<pre>+-------------------------------------+------------------+-----------------+</pre>



<pre>| 683.818ms                           | 0                | 0               |</pre>



<pre>| 1.68s                               | 6.75             | 2985            |</pre>



<pre>| 2.68s                               | 14               | 6214            |</pre>



<pre>| 3.71s                               | 18.5             | 8187            |</pre>



<pre>| 4.70s                               | 27               | 11911           |</pre>



<pre>| 5.68s                               | 34.75            | 15398           |</pre>



<pre>| 6.68s                               | 41.5             | 18320           |</pre>



<pre>| 7.69s                               | 47               | 20700           |</pre>



<pre>| 8.69s                               | 49.75            | 21956           |</pre>



<pre>| 9.70s                               | 55.5             | 24522           |</pre>



<pre>| 10.69s                              | 60               | 26458           |</pre>



<pre>| 11.68s                              | 66.25            | 29173           |</pre>



<pre>| 12.68s                              | 72.75            | 32062           |</pre>



<pre>| 13.68s                              | 79               | 34797           |</pre>



<pre>| 14.70s                              | 85               | 37442           |</pre>



<pre>| 15.69s                              | 91.5             | 40345           |</pre>



<pre>| 16.68s                              | 97.75            | 43075           |</pre>



<pre>| 18.27s                              | 100              | 44032           |</pre>



<pre>+-------------------------------------+------------------+-----------------+</pre>



<pre>Finalizing lookup tables.</pre>



<pre>Generating candidate set for working with new users.</pre>



<pre>Finished training in 18.3162s</pre>


    
    Precision and recall summary statistics by cutoff
    +--------+-----------------+-----------------+
    | cutoff |  mean_precision |   mean_recall   |
    +--------+-----------------+-----------------+
    |   1    |  0.128978224456 | 0.0199836976114 |
    |   2    |  0.118090452261 | 0.0294753600348 |
    |   3    |  0.107761027359 |  0.04101637346  |
    |   4    |  0.100502512563 | 0.0443693698612 |
    |   5    | 0.0968174204355 | 0.0502247044972 |
    |   6    | 0.0921273031826 | 0.0573069832429 |
    |   7    | 0.0854271356784 | 0.0608611585133 |
    |   8    | 0.0824958123953 | 0.0636698990695 |
    |   9    | 0.0815187046343 | 0.0680629663957 |
    |   10   |  0.080067001675 | 0.0724210738535 |
    +--------+-----------------+-----------------+
    [10 rows x 3 columns]
    
    ('\nOverall RMSE: ', 3.896859490041479)
    
    Per User RMSE (best)
    +--------------------+-------+---------------+
    | review_profilename | count |      rmse     |
    +--------------------+-------+---------------+
    |     AxelTheRed     |   1   | 0.73851031065 |
    +--------------------+-------+---------------+
    [1 rows x 3 columns]
    
    
    Per User RMSE (worst)
    +--------------------+-------+------+
    | review_profilename | count | rmse |
    +--------------------+-------+------+
    |      DonaCake      |   1   | 5.0  |
    +--------------------+-------+------+
    [1 rows x 3 columns]
    
    
    Per Item RMSE (best)
    +-----------+-------+----------------+
    | beer_name | count |      rmse      |
    +-----------+-------+----------------+
    |   Biobok  |   1   | 0.997245179282 |
    +-----------+-------+----------------+
    [1 rows x 3 columns]
    
    
    Per Item RMSE (worst)
    +----------------+-------+------+
    |   beer_name    | count | rmse |
    +----------------+-------+------+
    | Amarillo Amber |   1   | 5.0  |
    +----------------+-------+------+
    [1 rows x 3 columns]
    
    


```python
rmse_results5['precision_recall_by_user'].groupby('cutoff', agg_list)
```




<div style="max-height:1000px;max-width:1500px;overflow:auto;"><table frame="box" rules="cols">
    <tr>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">cutoff</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Avg of precision</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Stdv of precision</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Avg of recall</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Stdv of recall</th>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">16</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.070351758794</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.14259485738</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0852812797065</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.191074947886</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">10</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.080067001675</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.156665404963</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0724210738535</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.182173344905</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">36</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0544853899125</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.110610459534</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.128475061693</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.223412790498</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">26</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0603659322252</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.122623960712</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.109720858959</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.210792532192</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">41</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0518854434776</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.105313221947</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.134794159659</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.225149825942</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.107761027359</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.226072053674</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.04101637346</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.147208225729</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.128978224456</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.335175837542</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0199836976114</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.104803368627</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">6</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0921273031826</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.182215507423</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0573069832429</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.169164237683</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">11</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.07857469164</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.154217265909</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0754416478084</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.183311552975</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.118090452261</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.258602814378</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0294753600348</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.123496212879</td>
    </tr>
</table>
[18 rows x 5 columns]<br/>Note: Only the head of the SFrame is printed.<br/>You can use print_rows(num_rows=m, num_columns=n) to print more rows and columns.
</div>




```python
item_item3 = gl.recommender.item_similarity_recommender.create(train, user_id='review_profilename' ,item_id='beer_name',
                                                              target= 'review_overall',only_top_k=4,similarity_type='jaccard',training_method = 'dense')

rmse_results6 = item_item3.evaluate(test)
rmse_results6['precision_recall_by_user'].groupby('cutoff', agg_list)
```


<pre>Recsys training: model = item_similarity</pre>



<pre>Warning: Ignoring columns brewery_id, brewery_name, review_time, review_aroma, review_appearance, beer_style, review_palate, review_taste, beer_abv, beer_beerid;</pre>



<pre>    To use these columns in scoring predictions, use a model that allows the use of additional features.</pre>



<pre>Preparing data set.</pre>



<pre>    Data has 1509514 observations with 32830 users and 44032 items.</pre>



<pre>    Data prepared in: 0.847765s</pre>



<pre>Training model from provided data.</pre>



<pre>Gathering per-item and per-user statistics.</pre>



<pre>+--------------------------------+------------+</pre>



<pre>| Elapsed Time (Item Statistics) | % Complete |</pre>



<pre>+--------------------------------+------------+</pre>



<pre>| 4.511ms                        | 3          |</pre>



<pre>| 20.053ms                       | 100        |</pre>



<pre>+--------------------------------+------------+</pre>



<pre>Setting up lookup tables.</pre>



<pre>Processing data in one pass using dense lookup tables.</pre>



<pre>+-------------------------------------+------------------+-----------------+</pre>



<pre>| Elapsed Time (Constructing Lookups) | Total % Complete | Items Processed |</pre>



<pre>+-------------------------------------+------------------+-----------------+</pre>



<pre>| 1.99s                               | 0                | 3               |</pre>



<pre>| 2.99s                               | 27               | 11964           |</pre>



<pre>| 3.99s                               | 51.75            | 22842           |</pre>



<pre>| 4.99s                               | 75.5             | 33312           |</pre>



<pre>| 6.06s                               | 90.5             | 39930           |</pre>



<pre>| 7.00s                               | 99.5             | 43833           |</pre>



<pre>| 9.99s                               | 100              | 44032           |</pre>



<pre>+-------------------------------------+------------------+-----------------+</pre>



<pre>Finalizing lookup tables.</pre>



<pre>Generating candidate set for working with new users.</pre>



<pre>Finished training in 10.0425s</pre>


    
    Precision and recall summary statistics by cutoff
    +--------+-----------------+-----------------+
    | cutoff |  mean_precision |   mean_recall   |
    +--------+-----------------+-----------------+
    |   1    |  0.12730318258  | 0.0197975818474 |
    |   2    |  0.117252931323 | 0.0298475915629 |
    |   3    |  0.108319374651 | 0.0410191952067 |
    |   4    |  0.10175879397  | 0.0447478020173 |
    |   5    | 0.0961474036851 | 0.0501182396471 |
    |   6    | 0.0921273031826 | 0.0572195497791 |
    |   7    | 0.0844699688921 | 0.0607120082436 |
    |   8    | 0.0816582914573 | 0.0635623498153 |
    |   9    | 0.0805881258143 |  0.067843158928 |
    |   10   | 0.0798994974874 | 0.0725362496354 |
    +--------+-----------------+-----------------+
    [10 rows x 3 columns]
    
    ('\nOverall RMSE: ', 3.896861603739727)
    
    Per User RMSE (best)
    +--------------------+-------+---------------+
    | review_profilename | count |      rmse     |
    +--------------------+-------+---------------+
    |     AxelTheRed     |   1   | 0.73851031065 |
    +--------------------+-------+---------------+
    [1 rows x 3 columns]
    
    
    Per User RMSE (worst)
    +--------------------+-------+------+
    | review_profilename | count | rmse |
    +--------------------+-------+------+
    |      DonaCake      |   1   | 5.0  |
    +--------------------+-------+------+
    [1 rows x 3 columns]
    
    
    Per Item RMSE (best)
    +-----------+-------+----------------+
    | beer_name | count |      rmse      |
    +-----------+-------+----------------+
    |   Biobok  |   1   | 0.997245179282 |
    +-----------+-------+----------------+
    [1 rows x 3 columns]
    
    
    Per Item RMSE (worst)
    +----------------+-------+------+
    |   beer_name    | count | rmse |
    +----------------+-------+------+
    | Amarillo Amber |   1   | 5.0  |
    +----------------+-------+------+
    [1 rows x 3 columns]
    
    




<div style="max-height:1000px;max-width:1500px;overflow:auto;"><table frame="box" rules="cols">
    <tr>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">cutoff</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Avg of precision</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Stdv of precision</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Avg of recall</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">Stdv of recall</th>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">16</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0700376884422</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.141066427098</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0852880587504</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.191029887882</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">10</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0798994974874</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.15616206186</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0725362496354</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.182184682021</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">36</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0544388609715</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.110018327914</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.128836492466</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.223329692006</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">26</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0602370828501</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.122059605369</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.109735994225</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.21079517673</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">41</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.052130571557</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.105890759279</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.134600532131</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.224950516056</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.108319374651</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.225392568158</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0410191952067</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.147191514485</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.12730318258</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.333312289429</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0197975818474</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.104740013698</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">6</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0921273031826</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.182470679912</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0572195497791</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.169172940346</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">11</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0782701385716</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.15365298415</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0753652675193</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.183317624357</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.117252931323</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.258173895168</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0298475915629</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.124823013588</td>
    </tr>
</table>
[18 rows x 5 columns]<br/>Note: Only the head of the SFrame is printed.<br/>You can use print_rows(num_rows=m, num_columns=n) to print more rows and columns.
</div>




```python
compare_struct = gl.compare(test,[item_item1, item_item2,item_item3])
```

    PROGRESS: Evaluate model M0
    
    Precision and recall summary statistics by cutoff
    +--------+-----------------+-----------------+
    | cutoff |  mean_precision |   mean_recall   |
    +--------+-----------------+-----------------+
    |   1    |  0.12730318258  | 0.0199446586951 |
    |   2    |  0.118090452261 | 0.0298631012099 |
    |   3    |  0.109436069235 |  0.041244459459 |
    |   4    |  0.10175879397  | 0.0449011922957 |
    |   5    | 0.0971524288107 | 0.0504032302616 |
    |   6    | 0.0918481295366 | 0.0572846792095 |
    |   7    | 0.0851878439818 | 0.0608418737711 |
    |   8    | 0.0827051926298 | 0.0637737911571 |
    |   9    | 0.0815187046343 | 0.0680242881437 |
    |   10   | 0.0804020100503 | 0.0726836448326 |
    +--------+-----------------+-----------------+
    [10 rows x 3 columns]
    
    PROGRESS: Evaluate model M1
    
    Precision and recall summary statistics by cutoff
    +--------+-----------------+-----------------+
    | cutoff |  mean_precision |   mean_recall   |
    +--------+-----------------+-----------------+
    |   1    |  0.128978224456 | 0.0199836976114 |
    |   2    |  0.118090452261 | 0.0294753600348 |
    |   3    |  0.107761027359 | 0.0410093996402 |
    |   4    |  0.100502512563 | 0.0443292418163 |
    |   5    | 0.0961474036851 | 0.0498860394771 |
    |   6    | 0.0915689558906 | 0.0569487270897 |
    |   7    | 0.0849485522852 | 0.0605170899886 |
    |   8    | 0.0816582914573 | 0.0633417190846 |
    |   9    | 0.0802158942862 | 0.0675857887058 |
    |   10   | 0.0795644891122 | 0.0720023296828 |
    +--------+-----------------+-----------------+
    [10 rows x 3 columns]
    
    PROGRESS: Evaluate model M2
    
    Precision and recall summary statistics by cutoff
    +--------+-----------------+-----------------+
    | cutoff |  mean_precision |   mean_recall   |
    +--------+-----------------+-----------------+
    |   1    |  0.12730318258  | 0.0197975818474 |
    |   2    |  0.117252931323 | 0.0298475915629 |
    |   3    |  0.108319374651 | 0.0410191952067 |
    |   4    |  0.10175879397  | 0.0447478020173 |
    |   5    | 0.0961474036851 | 0.0501182396471 |
    |   6    | 0.0921273031826 | 0.0572195497791 |
    |   7    | 0.0844699688921 | 0.0607120082436 |
    |   8    | 0.0816582914573 | 0.0635623498153 |
    |   9    | 0.0807742415783 | 0.0678939177727 |
    |   10   |  0.080067001675 | 0.0725870084801 |
    +--------+-----------------+-----------------+
    [10 rows x 3 columns]
    
    Model compare metric: precision_recall
    


```python
gl.show_comparison(compare_struct,[item_item1, item_item2,item_item3])
```

    Canvas is updated and available in a tab in the default browser.
    

# Testing it Out

- Here are I just give the item-item recommender some sample beers and see how it preforms. The first beer I try is Corona Light and the recommended beer is Michelob Ultra. I think that works pretty well, they are similar beers. The next beer I tried was Coor’s Light, which recommended Bud Light and Budweiser, these beers are definitely similar to Coors Light. I then tried a user recommendation, which didn’t perform as well, but not knowing the user its hard to say for sure.


```python
item_item2.get_similar_items(items = ['Corona Light'])
```




<div style="max-height:1000px;max-width:1500px;overflow:auto;"><table frame="box" rules="cols">
    <tr>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">beer_name</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">similar</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">score</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">rank</th>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Corona Light</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Michelob Ultra</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.186629533768</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Corona Light</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Miller Genuine Draft</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.175349414349</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Corona Light</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Amstel Light</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.173784971237</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Corona Light</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Bud Ice</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.17365270853</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">4</td>
    </tr>
</table>
[4 rows x 4 columns]<br/>
</div>




```python
item_item2.get_similar_items(items = ['Coors Light'])
```




<div style="max-height:1000px;max-width:1500px;overflow:auto;"><table frame="box" rules="cols">
    <tr>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">beer_name</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">similar</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">score</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">rank</th>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Coors Light</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Bud Light</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.288586974144</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Coors Light</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Budweiser</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.263473033905</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Coors Light</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Corona Extra</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.25945019722</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Coors Light</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Miller Lite</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.25552970171</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">4</td>
    </tr>
</table>
[4 rows x 4 columns]<br/>
</div>




```python
item_item2.recommend(users =['rickcampie'], k=4)
```




<div style="max-height:1000px;max-width:1500px;overflow:auto;"><table frame="box" rules="cols">
    <tr>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">review_profilename</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">beer_name</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">score</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">rank</th>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">rickcampie</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Cascazilla</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0377279818058</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">rickcampie</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Wachusett IPA (India Pale<br>Ale) ...</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0297293464343</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">rickcampie</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Sierra Nevada Celebration<br>Ale ...</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0293260713418</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">3</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">rickcampie</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Old Rasputin Russian<br>Imperial Stout ...</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">0.0283443927765</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">4</td>
    </tr>
</table>
[4 rows x 4 columns]<br/>
</div>



### Conclusion 
- I am pretty happy with the way the model preformed. Although precision and recall aren’t the best it seems like the model still performs well for item recommendations. This was very fun to implement.



```python

```
