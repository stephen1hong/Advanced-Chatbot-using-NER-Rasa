# Advanced-Chatbot-using-NER-Rasa

Idea:
To build achatbot that understand the context (intent)and can also extract entities, 
we need an NLP pipeline that canperform intent classification,along with NER extraction,
and then provide an acurate response.

Rasa NLU is a Natral Language Understanding tool forunderstnding a text/document. 

for example:  a question: 
"I am looking for a french restaurant in the cneter of town"

the chatbot system return: 
Intent: search_restaunt
entities:
       -cusine: mexican
       -location: center of town

Steps: 
 1)Install Rasa in console
  pip install rasa_nlu
  pip install coloredlogs sklearn_crfsuite spacy
  python -m spacy download en
 2) Prepare dataset
   create the JASON file in the current working directory
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
   language: "en"
   pipeline: spacy_sklearn"
   fine_tune-spacy_ner: true
  *) run training using command in console:
   python -m rasa_nlu.train \
   --config config_spacy.yml \
   --data restaurant.json \
   --path projects

4) deploying the model 
  *) using Rasa, you don't even need to write any API services--everythig is available in the package.
   to expose the trained model as service, you just need to execute such command in console:
   python -m rasa_nlu.server --path projects
   if everything goes right, then a RESTful API will be exposed at port 5000 and a log file will be displayed.
  *) To access the API, you can use such command in a separate console for querying the model, for example:
   curl -X POST localhost:5000/parse -d '{"q": I am looking for Mexican food"}' | python -m json.tool

   Output:
   {
    ......

   }
   
