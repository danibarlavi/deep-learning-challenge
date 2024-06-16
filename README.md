# deep-learning-challenge

# OVERVIEW
The purpose of this analysis is to help the non-profit organization, Alphabet Soup, identify potential funding targets using machine learning. The goal is to create a model that can predict which groups/business/organizations are most likely to have "the best chance of success in their ventures" out of Alphabet Soup's applicant pool. 

# RESULTS
# A. Data Preprocessing:
  # The target variable for my model is the column IS_SUCCESSFUL, which features a boolean value of 0 or 1 demonstrating whether each applicant in the dataset 'successfully' received a loan. 
  # The following variables serve as features for my model:
    - APPLICATION_TYPE - As set by Alphabet Soup's filing system
    - AFFILIATION - Group affiliation
    - CLASSIFICATION - Governmental organization classification
    - USE_CASE - Use case/industry
    - ORGANIZATION - Type of organization
    - STATUS - Active or not
    - INCOME_AMT - Self-explanatory
    - SPECIAL_CONSIDERATIONS - Whether Alphabet Soup had 'special considerations' for this applicant
    - ASK_AMT - Self-explanatory
    ![image](https://github.com/danibarlavi/deep-learning-challenge/assets/153565413/bcfe52b3-bc60-4900-b9d1-5225e923da83) - Sample of charity_data.csv
  # I removed the following variables as they are neither targets nor features:
   - EIN (Employer Identification Number)
   - Name (Name of applicant organization)


# B. Compiling, Training, and Evaluating the Model:
  - I used three hidden layers and one 'output' layer for my model. I used a descending amount of neurons to try to 'hone in' on the binary classification for my model's output. I started with 8 neurons in my first hidden layer, decreasing to 4 in the second, 2 in the third, and 1 in the output layer. I used a small amount of neurons because of the binary nature of the code's output.
  - I used 'swish' as my activation function for my hidden layers as I read it performs better than relu at the cost of more computing power. I was unworried about computing power as I was using Google Colab for this project.
  - I used 'sigmoid' as my activation function for my output layer as the output is binary and 'sigmoid' is the standard activation function for binary analysis.
  - ![image](https://github.com/danibarlavi/deep-learning-challenge/assets/153565413/0ad0f8b0-600a-4699-902c-5ff42e631cc2)
  - I was unable to reach the target performance of 75%, capping out in the high 60s/low 70s, giving up after several hours of tweaking the model.

# Increasing Model Performance
 - I took the following steps to increase model performance:
     - **Changing Activation Function**: I replaced the 'relu' activation function with 'swish' as described above.
     - **Adding a layer**: I increased the number of total layers from 3 to 4.
     - **Removing identifying variables** I removed 'EIN' and 'NAME' from the model as both variables were simply identifiers and did not help from a predictive standpoint.
         - ![image](https://github.com/danibarlavi/deep-learning-challenge/assets/153565413/cbde1e55-631c-492f-acdf-b5d0d1ea98c1)
     - **Binning**: Perhaps the most extensive optimization step I took. I made the following modifications to the data:
         - Bin all 'Application Types' with less than 1000 entries into 'Other'.
            - ![image](https://github.com/danibarlavi/deep-learning-challenge/assets/153565413/6038a8e0-e195-49e8-bfa7-1c7f54639404)
         - Bin all 'Classifications' with less than 2000 entries into 'Other'.
           - ![image](https://github.com/danibarlavi/deep-learning-challenge/assets/153565413/46bda251-cfce-4200-9466-492a7f4f4010)
         - Bin 'ASK_AMT' into just two bins:
           - ![image](https://github.com/danibarlavi/deep-learning-challenge/assets/153565413/9544d132-a31d-458f-a0f4-8e038fca8ac2)
        - Bin all 'Affiliations' with less than 10K entries into 'Other'.
            - ![image](https://github.com/danibarlavi/deep-learning-challenge/assets/153565413/07e07838-9f0d-4d5f-84d4-f6714f18a240)
        - Bin all 'Organization' types with less than 500 entries into 'Other'
          - ![image](https://github.com/danibarlavi/deep-learning-challenge/assets/153565413/73483d76-e493-4096-afc0-5409061a32fe)
        - Bin all 'Use Cases' with less than 500 entires into 'Other'
          - ![image](https://github.com/danibarlavi/deep-learning-challenge/assets/153565413/758be7ab-45e9-420e-9468-6d37b3ddb3c0)
      - **Removing outliers**
          - I filtered out all applications with 'Yes' in 'Special Considerations' in order to reduce outliers as there are factors influencing those applications not included in the dataset.


# SUMMARY:
My final model had an accuracy of about 70%, short of the 75% goal set in this assignment. I'm very pleased with the increase in performance from the intial 65% that resulted from my data cleaning and binning, and would be curious to take steps to further optimize the model by adjusting the machine learning settings a bit more, including batch size, number of epochs, number of layers, and neurons per layer. I do wonder whether my hypothesis that fewer neurons would be better for a simple, binary output is flawed, and mt next step would be to test the model only changing the amount of neurons used, perhaps multiplying each by a factor of 10 to see where I get. 

If I could recommend a different model to solve this classification problem, I would actually first instruct Alphabet Soup to research further data on how the Organizations they funded or did not fund performed _after_ the application process, rather than just training a model on data surrounding which applicants were approved. A model trained on the existing dataset does not actually accomplish the goal of 'selecting applicants for funding with the best chance of success in their ventures', rather it accomplishes selecting applicants for funding who are most like the applicants Alphabet Soup has selected in the past. This does not add much to their decision making process, only reinforcing pre-existing notions and biases in how they currently make funding decisions. A model that looks at the profits or other quantifiable achievements of applicants who did and did not receive funding would be much more helpful in this process.






