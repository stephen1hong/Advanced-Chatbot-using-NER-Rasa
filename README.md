# Advanced-Chatbot-using-NER-Rasa


To build achatbot that understand the context (intent) and also extract entities, 
we need an NLP pipeline that canperf orm intent classification, along with NER extraction,
and then provide an accurate response.

Rasa NLU is a Natral Language Understanding tool forunderstnding a text/document. 

Usages: 
 1) Install Rasa in console
  * pip install rasa_nlu
  * pip install coloredlogs sklearn_crfsuite spacy
  * python -m spacy download en
 2) Prepare dataset
   * create the JASON file in the current working directory:
   "rasturant.json"
 
 the struture looks like:
 {
  "rasa_nlu_data"{
   entity_examples": [entity_list],
   intent_examples": [intent_list]
   }
 }
3) training the model
   *) create a "config_spacy.yml" file in the working directory, consist of 3 lines:
    * language: "en"
    * pipeline: spacy_sklearn"
    * fine_tune-spacy_ner: true
  *) run training using command in console:
     * python -m rasa_nlu.train \
   --config config_spacy.yml \
   --data restaurant.json \
   --path projects

4) deploying the model 
  *) run command:
      * python -m rasa_nlu.server --path projects
   
  *) To access the API for querying the model, run command like below:
      * curl -X POST localhost:5000/parse -d '{"q": I am looking for Mexican food"}' | python -m json.tool

---
Reference: "Python Deep Learning projects," M. Lamons, R. Kumar, A. Nagaraja 

   
