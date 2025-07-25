# Restaurants-RAG-Padova

**Question Answering system with RAG about reviews of restaurants in Padova**

---

## Project overview

This project creates a small pipeline for answering questions regarding restaurants in Padova.

---

## The project can be structured as follows:

### Section 0: Data retrieval

Using the APIs from Google Maps, the following tasks were performed:  
1. Extract relevant restaurants in Padova. A grid of 50 different small areas was created. Each area can retrieve up to 60 places.  
2. Duplicated places were removed alongside places that do not belong to Padova.  
3. Details for each place were also extracted, including metadata and reviews (5 per place).  

At the end, there were 559 restaurants and 2500+ reviews.

---

### Section 1: Data refining

The retrieved information was normalized and cleaned. Actions performed were:  
1. Convert values into lists or dicts.  
2. Check for null values.  
3. Remove links or symbols in the reviews dataframe. Emoticons were not removed.  
4. Also, landmarks were retrieved and the distance from each restaurant was stored. Only the 3 closest were taken into account.

---

### Section 2: Text composition

Here, it was decided to create one document for each restaurant. This will have two keys:  
1. A text description that includes name, location, price, rating, and proximity to landmarks. Also, serving offers, schedule, and contact information were added. Finally, the 5 reviews were included. All this information was formatted in natural language to make it easy to understand.  
2. Metadata with main parameters such as name, price, and rating.

---

### Section 3: Corpus creation

In this section, the `.json` file was defined with as many entries as the number of restaurants and the previously extracted metadata.

---

### Section 4: Model creation

Here the main basis of the project is defined:  
- First, the `"microsoft/Phi-3-mini-4k-instruct"` model was loaded, which is an instruction-tuned model. With this, the model will know the approach to take.  
- Second, the prompt template was defined. More information can be found in the file.  
- Third, the information was divided into chunks where each one has the metadata. This will allow the model to always take into account the place it is analyzing.  
- Fourth, Chroma was used in order to construct the embeddings.

---

### Section 5: Test model

Finally, the model was tested using the provided questions. To reduce memory consumption, every 5 questions, the GPU memory was flushed.

---

## Conclusions:

- The model is able to answer the given questions, which is what we intended. Nevertheless, answers are too long.  
- Despite modifying some parameters, the final `questions-answers.txt` contained what was considered the most suitable configuration.  
- Perhaps some fine-tuning was necessary or concatenating a model able to summarize answers.


## Questions & Answers:

**Question related to a landmark proximity**
**A. "Is there a restaurant close to a church?"**
 Yes, both Ristorante pizzeria bar L'OASI DEI SAPORI and Morning Cafe' Padova are restaurants with locations within proximity to churches as indicated by their distances mentioned in Documents 1 and 2 respectively; however, it should be noted that these specific measurements may vary depending on actual walking distance or public transportation routes used during different times of day or year.
 
 **B. "What is the closest restaurant to Piazzale Stazione?"**
  The three restaurants mentioned (Pizzeria da Giuliano, BAR PIZZERIA 21, and Rustichelli & Mangione) all share the same location near Piazzale della Stazione; therefore, they are equally close without additional data needed for comparison. However, if one must choose among them solely based on proximity as defined by shared address, it's impossible to determine which would be "closest" since each occupies different street numbers within the vicinity but shares the common area name. To accurately identify the nearest establishment relative to another specific point or landmark outside this group requires further geographical detail.
  
**C. "Is there a restaurant near Prato della Valle?"**
   Yes, both Al Prato with its location being directly adjacent (Via Prato della Valle) as well as The Food Hub which shares the same street name but different addresses within it offer restaurants nearby Prato della Valle; however, they differ slightly by distance relative to other landmarks mentioned for each establishment.

**Questions from dataset**
**1. What are the best restaurants in the city?**
      Based on ratings alone, La Pizzeria Maxim has an excellent reputation; it offers personalized service along with high quality Italian cuisine. For American fast food lovers seeking value deals like discounted drink prices during weekdays, consider visiting Hamerca's Ghetto Viale Dell'Arco Padova. Both establishments provide distinct dining experiences tailored to different preferences within the same locale.

**2. Where can I find the best Italian food in the city?**
    	 Based on ratings alone, both Spunciotti Di Pesce - Andreazzi Nereo and Ristorante Pizzeria S'Aligusta offer excellent experiences with perfect scores; however, considering reviews suggest fresh local specialties and friendly service respectively, these two establishments stand out among others rated similarly. It would be advisable to visit either one depending on whether you prefer traditional street food or quality pizza by the lake view.

**3. Are there any 24-hour restaurants in the city?**
	 Yes, both Fastdrink24 and Wok Time offer extended opening hours during weekdays; however, neither operates all day every night as per available data.




