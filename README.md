
# Problem Statement
Unlike the Equity Market, the Bond Market suffers from a severe lack of information.  With no quotes publicly available, the best way to get a quote is to solicit multiple brokers and wait for a reply.  Benchmark Solutions plans to predict accurate prices that incorporate interest rate data, trades or quotes of the bond in question, trades or quotes of other bonds or CDS of the issuer of the bond in question as well as other input sources. 


# Background
This project is based on a Kaggle Competition from 2012 hosted by Benchmark Solutions.  Benchmark sought to bring instant accurate bond pricing to customers by using neural networks.  Several teams competed in achieving this goal.  The highest team score was .68 Mean Absolute Error.  Following the competition students Swetava Ganguli and Jared Dunnmon took on the challenge to apply machine learning methods to the data set to produce better results.  After their models, Ganguli and Dunnmon were able to generate predictions with .66 WEPS (a metric of their own design similar to MAE).  

Reading the specifics of the Ganguli, Dunnmon paper and reviewing their results I decided to use multilayer Neural Networks and GLMs to create better and faster predictions.

 In their review of the results the authors concluded that “NNs and GLMs give best results in terms of combined speed and accuracy.” And “the success of neural networks on this dataset implies that investigating the application of multilayer networks and deep learning methods to this problem may yield better bond price predictions.”

# Data
The training set consisted of The training dataset consisted of 762,678 data points and 61 features.  Columns consist of Price, Time to Maturity, Trade Size, Callable, Trade Type and time series moving averages for 1 - 10 previous trades of Price, Trade Size, Trade Type and Curved Based Price. Weights were included by Benchmark, calculated as the square root of the time since the last trade scaled so the mean is 1.The dataset came well prepared, requiring little to no cleaning on my part.  Filling in NaN values for time series lag and dummying out categorical columns into binary variants were the steps I took preparing the data.   After the data was prepared, I used principal component analysis (PCA) on the entire data set in order to see if there existed a reduced feature set that retains the majority of the explanatory power of the full feature set.

# Models
My initial model was based on the suggestions of Ganguli and Dunnmon using a 5 layer Neural network and editing the number of nodes per layer.
Second and third models were GLMs which included an ordinary least squares regression (OLS) and a weighted least squares regression (WLS)
My fourth model was a Long Short-Term Memory Neural Network of similar design to my original model - 5 layers with varying node sizes.
I included a random forest regressor as a fifth additional option.

# Results
With the consideration of speed and accuracy I found that the multi-layer Neural Network (NN) produced the best results.  Reaching convergence around 100 epochs in just under 36 minutes and returning the lowest MAE.

LSTM NN which came close to the first NN in accuracy but took substantially longer to run, reaching convergence at just over 100 epochs taking 5 hours and 22 minutes.

OLS and WLS performed very quickly but fell short in accuracy.

Random Forest had decent results but at the cost of speed.

