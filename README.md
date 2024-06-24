# Personalized-Travel-Agent

Personalized-Travel-Agent is an AI-powered chatbot designed to assist users with **Travel-related Queries & Planning**. It provides a seamless interface for obtaining **General Travel Information and Exploring Tour Packages**.

## Introduction

The Personalized-Travel-Agent-Chatbot is your personal travel assistant, making trip planning effortless and enjoyable. With its user-friendly interface and AI-powered capabilities, it offers instant and accurate travel insights. Whether you need information on **city distances, flight times, or enticing travel packages**, our chatbot has you covered for seamless trip planning.

## Features

### General Travel Information (GTI)
- Distance between cities
- Flight times
- Estimated flight costs
- Travel tips and advice

### Tour Package Information (TPI)
- Customized vacation packages stored in **Local SQLite db**
- Package inclusions (accommodations, transportation, tours, activities)
- Various package types (luxury to budget-friendly options)
- Comparison of different travel agent offerings

## Technology Stack

- Web Interface: Streamlit
- AI Model: Gemini-pro LLM
- Hosting: Streamlit Cloud
- Backend: Python
- Database: SQLite

## How It Works


#### Visual Representation - Workflow

```
[User Input]
       |
       v
[Intent Classification Model]
       |
       +-----------------+
       |                 |
       v                 v
[General Travel      [Tour Package
 Information (GTI)]   Information (TPI)]
       |                 |
       v                 v
[GTI Prompt]         [TPI Prompt]
       |                 |
       v                 v
[Gemini-pro LLM]    [Gemini-pro LLM]
       |                 |
       v                 v
[Process Response]  [Natural Language to SQL Query Generation]
       |                 |
       |                 v
       v            [Trigger the Local Database (SQLite) to retrieve the Tour Packages]
       |                 |
       |                 v
       +-----------------+
                |
                v
      [Display Results to User]
```

This flowchart illustrates the process from user input to result display:

1. User submits a query through the Streamlit interface.
2. The app's model identifies the intent of the user's query, categorizing it as either General Travel Information (GTI) or Tour Package Information (TPI).
3. Based on the identified intent, the appropriate prompt is triggered:
   - For GTI: Provides information on distances, flight times, and cost ranges.
   - For TPI: Offers details on tour packages, including costs, duration, inclusions, and package types.
4. The appropriate prompt is sent to the Gemini-pro LLM for processing.
5. The response from the LLM is processed.
6. The final results are displayed to the user through the Streamlit interface.

## Prompts

### General Travel Information (GTI) Prompt
```python
prompt_gti = f"""
You are tasked with developing a travel planner system that handles multiple questions from the users like the distance
between the cities, flight time, range of the cost of the flight. The system should act as a virtual travel planner, providing information about 
distance between the cities, flight time and range of the cost of the flight when users inquire about travel options between places. The system 
should showcase virtual data, including  distance between the cities, flight time, range of the cost of the flight. The output response 
should be summarized and show information about the distance, flight time and range of the cost of flight.
user_question: {query}
"""
```

### Tour Package Information (TPI) Prompt
```python
prompt_tpi = f"""
You are tasked with developing a travel planner system that handles multiple travel agent tour packages for various cities. 
The system should act as a virtual travel planner, providing information about tour packages when users inquire about travel options between 
places or for a specific destination. The system should showcase virtual data for each tour package, including cost, duration, what is 
included in the package, and if there are any family tour packages available. Additionally, include a category for 'package type' and 
output all the different types of packages offered by each agent.
user_question: {query}
"""
```

### Intent Detection Prompt

```python
prompt_intent = f"""
        "prompt": "You are tasked with developing a Intent Detector for helping the user to plan their travel. 
            The system should act as a virtual Intent Detector travel planner and if the user query is about including distance between the cities, flight time, range of the cost of the flight then the response is "General Travel Information". 
            If the user query is about vacation travel or vacation plan or tour plan options between places or for a specific destination then the response should be "Tour Package Information. The output should be presented as ##Intent: Response in this format where Response is your output.",
            "user_question" --> "{query}"
        """
```

### Response
```python
result = get_gemini_repsonse(prompt_temp) ### Custom Fucntion to get the response for the prompt
```

## Deployment

The app is hosted on Streamlit Cloud for seamless accessibility, performance, and easy scalability and maintenance.

App Link: https://personal-travel-assistant.streamlit.app
