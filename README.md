# Local MS SQL Server Agent using LangChain and Ollama

This is based on the work done by Coding-Crashkurse. It is a python notebook that demonstrates how to create a SQL agent that can query as well as update a SQL Server database from a natural language statement entered by a user. The structure of the application is the same as the original one in that it takes a question from a user and it first checks the relevance of the question, then retrieves the database schema, then converts the user question into a SQL query, and tries to execute that query. If the query fails, then it is sent back to the LLM to regenerate the question and does this 2 more times. If it fails after the third attempt, then the system stops trying to generate a query. If the query executes successfully, then the LLM responds to the user depending on what the original question was. A user has the power to update a database table by, for example adding a user to the database using natural language. The key differences with the work by Coding-Crashkurse are:

- Using a Local LLM that does not require an API key or even an internet connection instead of the subscription-based OpenAI.
- Using a SQL Server database instead of SQLite.
- Explicitly stating the database schema to use.
- Added a graphical interface using Gradio.
- Added tests for key classes and functions to help with troubleshooting.


![Screenshot 2025-02-24 183219](https://github.com/user-attachments/assets/41688bd7-2065-4c52-8201-11041cdbe788)


**Local LLMs tested**

I have successfully tested this using the following local LLMs:

- Llama3.1:latest
- Qwen2.5-coder:3b
- Qwen2.5:latest
- Mistral:latest

I have tested all of these on an RTX 4060 8 GB GPU and the query to show all orders for the current user executes in about 15 seconds, with 10 seconds of that being for checking the relevance of the question. I used the AdventureWorksLT 2022 database with 10 tables and about a thousand records in each table. My next goal is to try and speed up the response time by figuring out a way to compress the database schema as it currently uses around 5000 tokens and is responsible for two-thirds of the response time.
