# Laptop Price Prediction : Exploratoratory data analysis and best line fit for Laptop data

Motivation:
  Buying a new laptop can get a bit trickier as there are 100s of brands available. I created an application which can help the consumer in chosing the laptop that suits them.
  This is a regression problem, and the prediction is done on the price as title suggests. TypeName, Inches, ScreenResolution, Cpu, Ram, Memory, Gpu, OpSys, Weight, TouchScreen, 
  IPS, X_res, Y_res are taken as independent variables.
  
Dataset Description:
  My first impressions of the data said that the data isn't clean. And it's quite clear that sufficient attention needs to be paid for this data during pre-processing.
  The sample data looks as follows:
  
  <img src="https://github.com/ferozqureshi/Laptop-Price-Prediction/blob/main/headlaptop.png" height="200" /> <br/>

## Process followed in solving the problem:
&nbsp; &nbsp;1️⃣Loading in data <br/> 
&nbsp; &nbsp;2️⃣Preprocessing the data <br/> 
&nbsp; &nbsp;3️⃣Creating different models <br/> 
&nbsp; &nbsp;4️⃣evaluating model performance <br/> 
&nbsp; &nbsp;5️⃣creating a Streamlit ML app
	
	
### 1️⃣Loading in data:
&nbsp; &nbsp;&nbsp; &nbsp;Pandas has been used to load the csv from local machine.
### 2️⃣Pre-processing the data
&nbsp; &nbsp;&nbsp; &nbsp;It was clear that pre-processing is an important step when I've seen the data for first time. Firstly, I've divided the columns into
categorical and numerical types; Company, TypeName, ScreenResolution, Cpu, Ram, Memory, Gpu, OpSys, Weight being the categorical columns and Inches, Price are 
numerical columns.<br/>
&nbsp; &nbsp;&nbsp; &nbsp;On observation I saw that if I remove "GB" from RAM, I can 
make it an integer value, now same goes with Memory and Weight. For Weight, I can classify it as floating variable
using the str.replace().<br/>
&nbsp; &nbsp;&nbsp; &nbsp;The price distribution can be viewed as below: <br/><br/>
&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;<img src="https://github.com/ferozqureshi/Laptop-Price-Prediction/blob/main/price_distribution.png" height="200" /> <br/>
&nbsp; &nbsp;&nbsp; &nbsp;The heatmap looks as follows:
<img src="https://github.com/ferozqureshi/Laptop-Price-Prediction/blob/main/heatmap.png" />
&nbsp;In keras there is [TextVectorization](https://www.tensorflow.org/api_docs/python/tf/keras/layers/TextVectorization) layer which does it for us.These tokens(maps text features to integer sequences)don't actually add more value until we convert them into word embeddings.
<br/> 
&nbsp; &nbsp;&nbsp; &nbsp;I have taken the vocab dictionary in the textvectorizer to be 200,000 (max_tokens=20000)
which is a big dictionary, and I've done it to maximize the accuracy. I've taken the maximum sequence length to be 1800.

#### The pipeline that I've followed:
   - Converted slices of an array in the form of objects by using tf.Dataset.from_tensor_slices()
   - Cached the data dataset.cache()
   - Shuffled the data using dataset.shuffle()
   - Made batches of 16 data points by using dataset.batch(16)
   - To prevent bottleneck, I have done the pre-fetching using dataset.prefetch(8)

### 3️⃣Creating an RNN LSTM model
1) Firstly, I've created an Embedding layer which converts the tokens to embeddings.<br/>
2) Next, I've used LSTM (Long Short-Term Memory) bidirectional layer to fit it.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;It is well known that LSTM performs better with
sequences, and sequences is what we've. <br/>
&nbsp;&nbsp;&nbsp;&nbsp;I've used tanh activation because tensorflow dictates to use tanh in specific to LSTM.
 The reason why I've used bidirectional layer is because 
 the sequences can have modifier words which changes the meaning of
of the sentence.

I've trained for 5 epochs till the losses are ; training loss:-  , validation loss:-



### 4️⃣Evaluating model performance
The following metrics has been used:<br/>
   - Precison
   - Recall
   - CategoricalAccuracy
   - make a note of all metrics

### 5️⃣Creating a gradio DL app
Finally, I serialized the model to h5 file
and integrated it with gradio.

Final look of Web Api: a gif...
  
