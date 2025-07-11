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
4. Also, landmarks we
