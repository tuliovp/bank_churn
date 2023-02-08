              <h1 style="font-size: 32px;">Case - Random Forest & SHAP Values (2022)</h1>
              <p>The following project was carried out for a major Canadian bank, aiming to understand the factors that help predict its customer churn.</p>
              <a class="btn1 btn-secondary btn1 text-uppercase" href="https://github.com/tuliovp/bank_turnover/tree/master">Github</a>
                <div class="case_content">
                  <h1>Description</h1>
                  <hr>
                  <p>
                    The base-model used for performance comparison was Logistic Regression. However, Random Forest Classifier provided better predictions and a lower acceptable MAE and RMSE. SHAP values helped to interpret the importance of each independent variable.
                    <br><br>
                    Customer churn is one of the most important metrics for a growing business to evaluate. While it's not the happiest measure, it's a number that can give your company the hard truth about its customer retention. Data analysis can help. We have information regarding more than 10 thousand customers and 19 features, the columns of the dataset that can be used as independent variables. The idea is to understand what drives the attrition and possible solutions.
                    <br>
                    I have used Python to do the pre-processing, cleaning, and exploratory analysis in a Jupyter Notebook.
                    As I found “smoke signals” or anything that caught my attention, I used Power BI for more interactive views and to save time. The cleaning process was simple: 
                    <ol>
                      <li>No missing values;</li>
                      <li>No negative values;</li>
                      <li>No duplicate rows/user ID’s;</li>
                      <li>Convert datatype of <code>Credit_Limit</code> and <code>Avg_Open_To_Buy</code> to int, to save memory;</li>
                      <li>Convert datatype of <code>Attrition_Flag to bool</code>, to save memory;</li>
                      <li>No need for <code>CLIENTNUM</code>, an index will do the job as there are no duplicates;</li>
                      <li>No need for <code>Avg_Open_To_Buy</code>, as <code>Credit_Limit</code>, <code>Total_Revolving_Bal</code> and <code>Avg_Utilization_Ratio</code> are enough and more useful (also, taking it out will avoid multicollinearity later on)</li>
                    </ol>
                    Three features were extracted in the process:
                    <ul>
                      <li><code>Increased Amt Change</code> 𝑄𝑜𝑄=𝟏 𝑖𝑓 𝐴𝑚𝑡 𝐶ℎ𝑎𝑛𝑔𝑒 𝑄𝑜𝑄>1</li>
                      <li> <code>Increased Ct Change</code> 𝑄𝑜𝑄=𝟏 𝑖𝑓 𝐶𝑡 𝐶ℎ𝑎𝑛𝑔𝑒 𝑄𝑜𝑄>1</li>
                      <li><code>Purchase Weight</code> =  (𝑇𝑟𝑎𝑛𝑠𝑎𝑐𝑡𝑖𝑜𝑛 𝐴𝑚𝑜𝑢𝑛𝑡)/(𝑇𝑟𝑎𝑛𝑠𝑎𝑐𝑡𝑖𝑜𝑛 𝐶𝑜𝑢𝑛𝑡)</li>
                    </ul>
                    <br>

                    <br><br>
                    <br>
                    <b>Exploratory Analysis:</b><br><br>
                    <br>
                    An analysis of key influencers in Power BI shows that <code>attrition_flag</code> is more likely to increase (1 – meaning the client leaves the bank), when they are reached out by more than 5 marketing campaigns. The average of <code>attrition_flag</code> grows by 0.84.
                    On the other hand, when clients have an average revolving balance, that is, the balance that carries over from one month to the next, between 581-2382, the average of the <code>attrition_flag</code> is more likely to decrease (it falls around 0.3)

                    <br><br>
                    <br>
                    <b>Predicting Churn:</b><br><br>
                    <br>
                    To create the base model, I used logistic regression, because it was the most obvious one. Problems having binary outcomes, such as Yes/No, 0/1, True/False, are the ones that we call classification problems. For the best fit of categorical dependent variables, like our case, a curve is required which is being possible with the help of Logistic Regression.
                    I thought the model could be improved - Pseudo R-squ.: 0.5068, in addition to several variables not being statistically significant (p-value greater than 0.05), so I performed a feature importance process using Decision Trees to try to reduce the number of variables and tested a Random Forest algorithm.
                    In the end, we ended up with 8 main features that most explain a churn rate prediction, from 0 to 1.
                    <br><br>
                    As we saw in the exploratory analysis, classes are unbalanced (84/16). So I use StratifiedShuffleSplit to split the train and test model, using 80% to train and 20% to test the predictions. Also we need to turn categorical variables into dummy variables - binary "switches" that turn the parameters in the equation on or off.

                    <br><br>
                    When there are several categorical independent variables, such as age, gender, salary range, Random Forest usually performs better than a Logistic Regression. But mainly, in addition to having given good predictions and an acceptable MAE and RMSE, it's not a black-box. That means we can measure the importance of each feature, as well as estimate the strength of the ensemble, correlation and generalization error (PE) in each division of the tree, allowing the model to be adjusted and validated during training.

                    <br><br>
                    <b>Analysis using SHAP values:</b><br><br>
                    SHAP values (SHapley Additive exPlanations) is a method based on cooperative game theory and used to increase transparency and interpretability of machine learning models. SHAP values interpret the impact of having a certain value for a given feature in comparison to the prediction we'd make if that feature took some baseline value. 
                    <br><br>Linear models, for example, can use their coefficients as a metric for the overall importance of each feature, but they are scaled with the scale of the variable itself, which might lead to distortions and misinterpretations. Also, the coefficient cannot account for the local importance of the feature, and how it changes with lower or higher values. The same can be said for feature importances of tree-based models, and this is why SHAP is useful for interpretability of models.
                    <br>We could ask "How much was a prediction driven by the fact that the team scored 3 goals?" But it's easier to give a concrete, numeric answer if we restate this as "How much was a prediction driven by the fact that the team scored 3 goals, instead of some baseline number of goals?" - 
                    Of course, each team has many features. <br>So if we answer this question for number of goals, we could repeat the process for all other features.
                    <br><br>SHAP values do this in a way that guarantees a nice property. Specifically, you decompose a prediction with the following equation:
                    <code>sum(SHAP values for all features) = pred_for_team - pred_for_baseline_values</code>

                    <br><br>
                  </p>
                  <br>
                  <h1>Read more</h1>
                  <hr>
                  <p>
                  Feel free to check how everything in the Jupyter Notebooks is working for yourself in the Portfolio link below. And please let me know if you have any comments.
                  </p>
                    <br>
                    <div class="row">
                      <div class="column">
                        <a class="btn btn-secondary btn text-uppercase" href="[https://github.com/tuliovp/bank_turnover/tree/master](https://tuliovp.github.io/#shap)">Portfolio</a>
                      </div>
                    </div>
                </div>
