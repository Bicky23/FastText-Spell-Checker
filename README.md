# SPELL CHECKER deployed as a REST API using Flask

The project uses a deep learning based approach to suggest upto three correct recommendations for any given word. Peter Norvig's [blog](https://norvig.com/spell-correct.html) was a nice inspiration while building up the solution. However it was this [blog](https://blog.usejournal.com/a-simple-spell-checker-built-from-word-vectors-9f28452b6f26) that really made. 


## Dataset for training

Web Inventory of Transcribed and Translated Talks; it is a ready-to-use version for research purposes of the multilingual transcriptions of TED talks.


## Model architecture 

The network architecture makes use of the architecture **FastText**, developed by Facebook. It has the advantage of traditional word vectors like **Glove**, **word2vec** etc in the sense that it can produce word vectors even for out-of-sample words. Also, for rare words it has been found be much more impactful than word vector representations.

Every word is represented in a 100-dimensional feature space and the model is trained on the data with  `window_size=5` and `min_count=5` with the help of `gensim` library. The trained model contains 100-D representation of all possible unique characters of the training dataset.


## Procedure

- Start a virtual environment and install requirements
- Run the file `model.py`. This will download your training data as well as train the **FastText** model on it, learn the representations and save them as `model.bin`
- Write `app.py` which is the API application that will be deployed
- Test the API


## Testing the API

1. Run the Flask API locally for testing. Go to directory with `app.py`
> python app.py

This outputs
> * Serving Flask app "app" (lazy loading)
 * Environment: production
   WARNING: Do not use the development server in a production environment.
   Use a production WSGI server instead.
 * Debug mode: on
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 154-300-115


2. Using curl in a new terminal to make a GET request at the URL of the API
> curl -X GET http://127.0.0.1:5000/spellCorrect -d query='sellection'

3. Example of successful output
> {
    "prediction": [
        "selection"
    ]
}







