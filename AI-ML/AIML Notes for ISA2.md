
# Ensemble Learning 

- Combines multiple models to improve the overall performance of predictions.
- Base Model should be different (2 cases) :
	1. Use different Algorithms (different models) and same data.
	2. Same Algorithm and different data.
- Helps to ==capture different patterns in the data.==


![[Pasted image 20241001183902.png]]

1. **Voting :**
	- Diff. Algo - Same Dataset
	- If classification - use voting
	- If regression - mean
2. **Stacking :**
	- **Diff. Algo - Same Dataset**
	- Adds a combining model which gives weightage to each base model. 
	- Better result : More weightage.
	- Bad result : Less weightage.
	-  Stacking involves ==training multiple base models== and then ==using another model (meta-learner)== to learn how ==to best combine their predictions==. This approach can utilize the strengths of various algorithms
	![[Pasted image 20241001185933.png]]

3. Bagging :
	- Bootstrap + Aggregation.
	- Same Algorithm, Different data.
	- Diagram.
	- These subset data are random datapoints. 2 subset data points can have same datapoints, repitition could also be there.
	- Even though the base models are same but due to different data, they perform differently, now for predicting a new data point we give it to all base models and whatever predictions we get from each of them, we finalize to 1 by voting or averaging.
	- Ex : Random Forest (Collection of Decision Trees)
4. Boosting :
	- Same Base Models, different data.
	- Boosting focuses on training models sequentially, where ==each model learns from the errors of the previous ones==. The final prediction is a weighted sum of the predictions from all models. AdaBoost and Gradient Boosting are common boosting techniques.
	- ==**The final prediction is calculated as a weighted sum of the individual predictions.**==

# Ensemble Learning Benefits :

- ==Imporovement in performance.==
- ==Low Bias, Low Variance== : Bias and Variance are usually inversly proportional, Ensemble learning tries to make both less. If one has low bias-high variance then Ensemble Learning makes it Low Bias and Low Variance and vice versa.
- (Low Bias : Less error in trainig, Low Variance : Not much changes happen in model if we change the data)
- ==Robustness== : Not much changes happen in model if we change the data. Yep, same as low variance :/ .

<hr><hr>


