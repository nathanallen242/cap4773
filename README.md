# Group 4: Final Project

This central repository will contain all relevant [Jupyter](https://jupyter.org/) notebooks, setup configurations & analysis files for each independent research question, Q1-3.

### Abstract
Explore the essence of our project and its overarching objectives here. *(0.5% common grade weight)*

*In the rapidly evolving scene of open source development, Github emerged as a social media platform helping software engineers collaborate. This study will explore various Github repositories and user behaviours to understand the dynamics of repository popularity, success, and the identification of false actors within the platform. First, we investigate the characteristics of popular and successful github repo repositories, with the intention of finding that contributing factors of success and popularity are not the same. We look at factors such as number of, number of forks, programming language, etc. We define popularity as the number of stars, a popular consideration by past papers. We also define success as a project claiming to be state of the art. Second, we address the detection of false actors in the social community. We examine the characteristics of false actors and analyze their potential impact on popularity. Lastly, we assess the impact of development consistency vs irregularity on popularity. Our findings aim to provide insights to factors that can enhance repository success, popularity, and credibility in GitHub.*


### Motivation and RQs
Discover what drives our research and review the specific research questions we are addressing. *(1% common grade weight)*

#### Research Questions
- **RQ1:** What are the characteristics of popular & successful repositories?
- **RQ2:** How can we determine false actors? What makes a GitHub user suspicious?
- **RQ3:** How can development consistency affect repository popularity?

#### Hypotheses
- **H1:** The factors influencing repository popularity differ from those determining its success.
- **H2:** False actors have drastically different activity and account behavior than real accounts.
- **H3:** The popularity of a repository is positively correlated with development consistency.

### Literature Review
Access a synthesis of existing knowledge and theoretical frameworks relevant to our research topic. *(0.5% common grade weight)*

- H. Borges, A. Hora, and M. T. Valente, "Understanding the Factors That Impact the Popularity of GitHub Repositories," 2016 IEEE International Conference on Software Maintenance and Evolution (ICSME), Raleigh, NC, USA, 2016, pp. 334-344, doi: 10.1109/ICSME.2016.31.
- Hudson Borges, Marco Tulio Valente, "What’s in a GitHub Star? Understanding Repository Starring Practices in a Social Coding Platform," Journal of Systems and Software, Volume 146, 2018, Pages 112-129, ISSN 0164-1212, https://doi.org/10.1016/j.jss.2018.09.016.
- Phylum Research Team, “Detecting potential Bad Actors in GitHub,” Phylum (2021).
- Golzadeh, M., Decan, A., Legay, D., & Mens, T. (2021). "A ground-truth dataset and classification model for detecting bots in GitHub issue and PR comments," Journal of Systems and Software, 175, 110911. https://doi.org/10.1016/j.jss.2021.110911
- Grönlund, Mårten and Jonathan Jefford-Baker, “Measuring correlation between commit frequency and popularity on GitHub.” (2017).

### Data
Detailed descriptions of the datasets we use, including sources and any preprocessing steps. *(2% common grade weight)*

#### Pre-processing Steps
The following pre-processing steps were applied to the datasets used in this research:

1. **Select the relevant columns:** Each research question required different columns/nested objects.
2. **Impute missing values:** If necessary, missing values were either replaced or removed.
3. **Feature Creation:** New features were derived from existing columns as required.
4. **Feature Selection:** Utilized traditional machine learning techniques to retain only relevant features.

#### Datasets
- **A Representative User-centric Dataset of 10 Million GitHub Developers**
  - Source: [Kaggle Dataset](https://www.kaggle.com/datasets/johntukey/github-dataset)
  - Description: 50 GB, user-centric JSON file containing data on GitHub users and their repositories.
  
- **Github Public Repository Metadata**
  - Source: [Kaggle Dataset](https://www.kaggle.com/datasets/pelmers/github-repository-metadata-with-5-stars)
  - Description: ~3.1 million rows containing repository-related information within the GitHub ecosystem; more repository-centric.

### Method
For detailed methodologies, please follow the specific directory linked to each research question.

### Results
For comprehensive results, please consult the specific directory for each research question.

### Discussion
For detailed discussions, insights, and interpretations, navigate to the relevant directory as per each research question.

### References
Consult this section for a list of all academic and technical resources referenced in our research. *(0.5% common grade weight)*

- H. Borges, A. Hora, and M. T. Valente, "Understanding the Factors That Impact the Popularity of GitHub Repositories," 2016 IEEE International Conference on Software Maintenance and Evolution (ICSME), Raleigh, NC, USA, 2016, pp. 334-344, doi: 10.1109/ICSME.2016.31.
- Hudson Borges, Marco Tulio Valente, "What’s in a GitHub Star? Understanding Repository Starring Practices in a Social Coding Platform," Journal of Systems and Software, Volume 146, 2018, Pages 112-129, ISSN 0164-1212, https://doi.org/10.1016/j.jss.2018.09.016.
- Phylum Research Team, “Detecting potential Bad Actors in GitHub,” Phylum (2021).
- Golzadeh, M., Decan, A., Legay, D., & Mens, T. (2021). "A ground-truth dataset and classification model for detecting bots in GitHub issue and PR comments," Journal of Systems and Software, 175, 110911. https://doi.org/10.1016/j.jss.2021.110911
- Grönlund, Mårten and Jonathan Jefford-Baker, “Measuring correlation between commit frequency and popularity on GitHub.” (2017).
