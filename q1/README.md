# Research Question 1: What are the characteristics of popular & successful repositories?

### Authors
Hashem Alsailani, Nathan Allen

### Methods

#### Prediction Technique

Our study utilizes multiple linear regression to predict three primary indicators of GitHub repository popularity: annual stars, annual forks, and open issues per year. These indicators are treated as separate dependent variables in our models. The independent variables are derived from a comprehensive set of features that characterize repository attributes, with the inclusion of a manually created 'age' feature representing the maturity of the repository. The regression model for each dependent variable $Y_{k}$ is formulated as follows:

$$
Y_{k} = b_0 + b_1X_1 + b_2X_2 + \ldots + b_rX_r
$$

Here, $Y_{k}$ signifies the k-th dependent variable (stars, forks, or issues per year), $X_i$ are the independent variables from our assembled feature set, and $b_j$ are the regression coefficients. This structured approach allows us to quantitatively assess the influence of various repository characteristics on its popularity metrics.

#### Estimating the Errors

To determine the accuracy of our models, we calculate the Relative Squared Error (RSE) for each prediction. For a repository $r$, let $N_k(r)$ be the actual observed value of the k-th dependent variable, and $Nb_k(r)$ the corresponding predicted value derived from our regression model. The RSE for each dependent variable is computed as follows:

$$
RSE_k = \left( \frac{Nb_k(r)}{N_k(r)} - 1 \right)^2
$$

To evaluate the overall performance of our models across the dataset, we compute the mean Relative Squared Error (mRSE) for each dependent metric, defined as the arithmetic mean of the RSE values across all evaluated repositories:

$$
mRSE_k = \frac{1}{|R|} \sum_{r \in R} \left( \frac{Nb_k(r)}{N_k(r)} - 1 \right)^2
$$

This approach ensures that our model's predictive accuracy is assessed comprehensively, providing a reliable measure of how well it can forecast the popularity metrics of GitHub repositories based on their characteristics.

#### Feature Selection

To optimize the input feature set for predicting the annual metrics of stars, forks, and open issues on GitHub repositories, LASSO Regression (Least Absolute Shrinkage and Selection Operator) was utilized. LASSO Regression serves as both a regularization and variable selection technique, which helps in enhancing the predictiveness of the regression model while simultaneously reducing the complexity.

The mathematical formulation for LASSO Regression is represented as:

$$
\min_{\beta} \{ \frac{1}{2n} \sum_{i=1}^{n} (y_i - X_i \beta)^2 + \lambda \sum_{j=1}^{p} |\beta_j|\right\}
$$

In this formula, $y_i$ denotes the dependent variable vector, $X_i$ represents the matrix of input features, $\beta$ are the coefficients, and $\lambda$ is the regularization parameter that controls the extent of sparsity in the coefficient vector $\beta$. The objective is to minimize the residual sum of squares subject to a penalty on the absolute size of the coefficients. This penalty term encourages the solution to have fewer non-zero coefficients, effectively reducing the number of features in the model.

The selection of $\lambda$ is crucial as it determines the balance between simplicity and fit of the model. A higher $\lambda$ value increases the number of coefficients shrunk to zero, thus prioritizing a simpler model, whereas a lower $\lambda$ retains more features but risks overfitting.

#### SoTA Classification

The classification of state-of-the-art (SoTA) claiming GitHub repositories involves several computational steps to handle and analyze textual data effectively. Below we outline the methodological process employed in our study, detailing each step under sub-headings.

##### I. Data Preparation

The initial step in our analysis involves creating a standardized list of common machine learning (ML) phrases. This list is utilized to filter and focus the textual content of repository descriptions. These descriptions are then subjected to tokenization, a process where text is broken down into its constituent tokens (words or phrases). We employed the model "sentence-transformers/all-mpnet-base-v2" to remove non-essential words, commonly referred to as fluff words, enhancing the relevance of the textual data for further processing.

$$
T_d = \text{Tokenize}(D, \text{model})
$$

Where \( T_d \) represents the tokenized description, and \( D \) is the original repository description. The tokenization model aids in refining the content to features more pertinent to our analytical goals.

##### II. Embedding Conversion + Similarity Score

Following pre-processing, the tokenized repository descriptions \( T_d \) and the ML phrases are transformed into embeddings. Embeddings are high-dimensional vectors that capture semantic meanings of the text, allowing computational models to process text-based data effectively. We utilized techniques that convert text into vector space models, where the proximity of vectors indicates semantic similarities.

$$
E_r = \text{Embed}(T_d)
$$

$$
E_m = \text{Embed}(M)
$$

Where $E_r$ is the embedding of the repository description and \( E_m \) is the embedding of ML phrases. The embeddings are then compared using cosine similarity, a metric used to measure how similar the documents are irrespective of their size.

$$
\text{Cosine Similarity} = \frac{E_r \cdot E_m}{\|E_r\| \|E_m\|}
$$

This measure helps in identifying repositories whose descriptions are semantically close to common ML phrases, suggesting potential SoTA claims.

##### III. Contextual Tagging using AI

To classify repositories as claiming state-of-the-art status, we leveraged the gpt3.5 turbo API. This advanced AI tool assists in tagging by analyzing the context of repository descriptions and aligning them with our predefined criteria for SoTA claims.

$$
\text{Tags} = \text{AI\_Tag}(E_r, \text{GPT-3.5 Turbo})
$$

Where \( \text{Tags} \) are the labels assigned by the AI based on the analysis of the embeddings \( E_r \) under the guidance of GPT-3.5 Turbo's contextual understanding capabilities.

This step-by-step approach ensures a rigorous and nuanced classification of GitHub repositories, providing insights into the landscape of claimed innovations within the ML community. By linking textual analysis with AI-driven tagging, our methodology supports a robust assessment of SoTA claims in public repository descriptions, crucial for the dynamic field of machine learning research.

##### IV. Handling Class Imbalance

The datasets used for classifying SoTA and non-SoTA repositories exhibited a pronounced class imbalance, with SoTA-claiming repositories making up 30% of Dataset 2 and 20% of Dataset 1. To mitigate this imbalance and enhance model performance, we have now adopted the method of applying class weights directly in the model training process. This approach adjusts the importance assigned to each class during the training of the machine learning model, compensating for imbalances by assigning higher weights to the minority class and lower weights to the majority class.

The mathematical basis for class weights can be formulated as follows:

$$
w_j = \frac{N}{k \times n_j}
$$

where \(w_j\) is the weight for class \(j\), \(N\) is the total number of samples in the dataset, \(k\) is the number of classes, and \(n_j\) is the number of samples in class \(j\). By applying these weights, the loss function during training is adjusted so that errors in predicting the minority class have a larger impact compared to the majority class. This effectively increases the cost of misclassifying the minority class, urging the model to pay more attention to it.

This method of handling class imbalance is directly integrated into the training phase of the model, ensuring that all classes are treated with appropriate importance relative to their representation in the data. This helps preserve the generalizability of the model across different datasets without introducing synthetic samples or potentially impacting the model’s ability to learn from real data distributions.

#### Model Interpretation

In the analysis of predictive models, understanding the influence of each feature on the predicted outcomes is crucial. Our approach to model interpretation encompasses both the visualization of input feature weights and the application of Shapley Additive exPlanations (SHAP) values to provide a more nuanced understanding of model behavior.

##### **Visualizing Feature Weights**

Feature weights are fundamental to interpreting the traditional linear models where each weight represents the strength and direction of the relationship between a feature and the outcome. By analyzing these weights, one can determine which features are most influential, and how changes in those features are expected to impact the predicted results. The positive or negative sign of each weight indicates whether the feature contributes positively or negatively to the outcome, respectively.

$$
\text{Influence} = \beta_i \times \text{Feature}_i
$$

Where $\beta_i$ is the weight associated with the $i$-th feature. This method is straightforward and provides a direct interpretation but is limited to linear associations.

##### **Shapley Additive exPlanations (SHAP) Values**

To overcome the limitations of basic feature weight interpretation, we employed SHAP values, which offer a more comprehensive insight into the contribution of each feature across a complex model's predictions. SHAP values are derived from game theory, specifically from the concept of Shapley values, which distribute the "payout" (prediction effect) among the "players" (features).

The key difference between SHAP and traditional feature importance is that SHAP considers the interaction effects between features. It provides a value for each feature for each prediction, indicating how much each feature contributed, positively or negatively, to that specific prediction. This is particularly useful in models where interactions or non-linearities obscure the effects of individual features.

$$
\phi_i = \sum_{S \subseteq N \setminus \{i\}} \frac{|S|!(|N|-|S|-1)!}{|N|!} \left[v(S \cup \{i\}) - v(S)\right]
$$

Where $\phi_i$ is the SHAP value for feature $i$, $S$ is a subset of features excluding $i$, $N$ is the total set of features, and $v$ is the model's prediction function.

### Results

#### Popularity

| Model                  | Stars (%) | Forks (%) | Issues (%) |
|------------------------|-----------|-----------|------------|
| Baseline Model         |-3.75% ± 0.18%|-8.18% ± 0.40%|-15.71% ± 0.45%|
| Linear Regression      |19.42% ± 0.51%|17.87% ± 0.38%|10.42% ± 0.31%|
| XGBoost                |21.20% ± 0.36%|19.69% ± 0.50%|13.03% ± 0.39%|

Table A: Model's regression performance on Dataset 1, by $R^2$ score

| Model                  | Stars (%) | Forks (%) | Issues (%) |
|------------------------|-----------|-----------|------------|
| Baseline Model         |-10.94% ± 0.09%|-1.08% ± 0.02%|-9.53% ± 0.06%|
| Linear Regression      |14.52% ± 0.15%|18.36% ± 0.21%|24.18% ± 0.12%|
| XGBoost                |16.34% ± 0.10%|19.85% ± 0.12%|27.65% ± 0.13%|

Table B: Model's regression performance on Dataset 2, by $R^2$ score

| Model                  | Stars (%) | Forks (%) | Issues (%) |
|------------------------|-----------|-----------|------------|
| Baseline Model         |-10.95% ± 0.09%|-1.09% ± 0.03%|-9.51% ± 0.09%|
| Linear Regression      |44.76% ± 0.12%|45.76% ± 0.18%|50.70% ± 0.13%|
| XGBoost                |49.63% ± 0.15%|54.72% ± 0.14%|49.78% ± 0.23%|

Table C: Model's regression performance on Dataset 2, by $R^2$ score

#### Success

| Model                  | Accuracy (%) | Precision (%) | Recall (%) | F1 Score |
|------------------------|--------------|---------------|------------|----------|
| Baseline Model         |59.13% ± 0.70%|49.81% ± 0.98%|49.81% ± 0.98%|49.79% ± 0.98%|
| Logistic Regression    |59.96% ± 1.29%|56.90% ± 0.98%|58.35% ± 1.14%|56.21% ± 1.07%|
| Random Forest          |71.08% ± 1.87%|59.43% ± 2.68%|53.45% ± 1.22%|51.25% ± 2.25%|
| XGBoost                |63.79% ± 0.97%|58.57% ± 1.11%|59.81% ± 1.38%|58.65% ± 1.16%|

Table D: Model's performance on Dataset 1, by classification metrics

| Model                  | Accuracy (%) | Precision (%) | Recall (%) | F1 Score |
|------------------------|--------------|---------------|------------|----------|
| Baseline Model         |55.10% ± 0.65%|49.97% ± 0.84%|49.96% ± 0.84%|49.96% ± 0.83%|
| Logistic Regression    |37.91% ± 1.29%|51.68% ± 1.21%|50.71% ± 0.54%|34.21% ± 1.78%|
| Random Forest          |67.15% ± 0.77%|61.52% ± 0.63%|55.91% ± 0.48%|54.39% ± 0.90%|
| XGBoost                |60.16% ± 0.82%|58.82% ± 1.27%|59.76% ± 1.40%|58.40% ± 1.17%|

Table E: Model's performance on Dataset 2, by classification metrics


### Discussion
