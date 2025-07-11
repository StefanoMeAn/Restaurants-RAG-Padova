# Restaurants-RAG-Padova
Question Answering system with RAG about reviews of restaurants in Padova

This project creates a small pipeline for answering questions regarding restaurants in Padova. 
The project can be structured as follow:
  Secion 0: Data retrieval
    Using the APIs from Google Maps, the following tasks were performed:
    1. Extract relevant restaurants in Padova. It was created a grid of 50 diffent small areas. Each area can retrieve up to 60 places.
    2. Duplicated places were removed alongside with places that do not belong to Padova.
    3. Details for each place was also extracted, this includes metadata and also reviews (5 per each)
    At the end, there were 559 restaurants and 2500+ reviews

  Section 1: Data refining
    The retrieved information was normalized and cleaned. Actions performed were:
    1. Convert values into list or dicts.
    2. Check null values
    3. Remove links or symbols in the reviews dataframe. Emoticons were not removed.
    4. Also, landmarks were retrieved and the distance from each restaurant was stored. Only the 3 closest were taken into account.

  Section 2: Text composition
    Here, it was decided to create one document for each restaurant. This will have two keys:
    1. A text description that includes name, location, price, rating and proximity to landmarks. Also, serving offers, schedule, contact information was added. Finally, the 5 reviews were added.
    All this information was formatted in natural language to make easy to understand.
    2. Metadata with main parameters such as: name, price, rating.

  Section 3: Corpus creation
    In this section, the .json file was defined with as many entries as the number of restaurants and the previously extracted metadata.

  Section 4: Model creation
    Here the main basis of the project is defined.
    First, it was load the "microsoft/Phi-3-mini-4k-instruct" model that will be the instructor-tuned model. With this, the model will know what approach must do. 
    Second, the prompt template was defined. More information can be found in the file.
    Third, the information was divided into chunks were each one has the metadata. This will allow the model to always take into account the place it is analyzing.
    Fourth, Chroma was used in order to construct the embeddings.

    Section 5: Test model
      Finally, the model was tested using the questions provided. In order to reduce memory consumption, every 5 questions, the GPU memory was flushed. 

Conclusions:

Model is able to answer the given questions, which is what we inteded. Nevertheless, answers are too long. Despite modifying some parameters, the final "questions-answers.txt" had what was considered the most suitable configuration. Perhaps some fine-tunning was necesary or to concadenate a model able to summarize answers.
