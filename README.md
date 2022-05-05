# DS-3002-Final-Projects
This repo contains my code and analysis for my discord trivia bot and my data ingestion projects

#######################################################################################################################################################################

Data Ingestion Project

replit link: https://replit.com/@HridaySingh/TimeDriftV2#main.py

API used: https://4feaquhyai.execute-api.us-east-1.amazonaws.com/api/pi

Analysis:

The database creates three fields in a JSON format: a factor (int type), a form of pi (float type), and the time (either string type or converted to date type). I chose to write these pieces of data to a SQL database because the columns keep their data type throughout the process. I used the time columns as the primary key as it is unique. My process created a SQL database and a table for the data with the data types mentioned above to create the schema (using SQLite). From there I created three functions: one for requesting data and converting it to text from the provided API, one for writing the data into the SQL table, and one for incrementing a counter to stop the process and close the SQL connection. I put each of these processes on a separate thread (decreasing the run time because of parallel processing), and schedule each task to execute every 60 seconds until they were performed 60 times.

The factor column appears to be equal to the minute of the time column cubed (example: 17:10:58 has 10 as the minute and the factor column equals 10 cubed or 1000). There doesn’t appear to be a discernable pattern with the pi variables, except at the 00-minute and 01-minute marks, pi appears to equal 4.0. Finally, the time simply increases by one minute and the seconds should be the same except for potential time drift caused by the speed at which the process takes to run (the time drift for my code after 4 runs averaged between 0.015-0.033 seconds per run). The successful db update screenshot can be seen in the repo.


#######################################################################################################################################################################

Discord Trivia Bot

replit link: https://replit.com/@HridaySingh/TimeDriftV2#main.py

API used: https://jservice.io/api/random (for trivia questions) and Discord API (via the discord python package)

Server invite link: https://discord.gg/vBwQUwQCw2

Analysis:

My discord bot plays a trivia game with the user. You can provide the phrase containing the word  ‘question’, and a question from a trivia API (consisting of a database of old jeopardy questions) will provide a random question. The bot will then start a 10-second timer and count down. The user can ask for a ‘hint’ or ‘clue’ and the bot will provide information on the category of the question. Once the timer runs out, the user can ask for the ‘answer’ and the bot will provide it. If you want the answer to be displayed right after the timer, simply message “$trivia” instead of ‘question’ and the answer will be provided right after the timer ends (good for single players). If a clue or answer is asked for before a question is asked (at the beginning of the game), the bot will respond that no question has been asked yet. If it is later in the game, the previous answer and clue will be provided for reference (in case the user wants to double-check the clue or answer). The three things the bot responds to are: phrases containing the word question (or $trivia), phrases containing the word answer, and phrases containing the word clue (or hint). Additionally, by asking for help (or $help) the bot will provide a message with words used to play the game. I have additionally connected my bot to an uptime robot and added functionality in keep_alive.py so this game will run even when the script is closed on my end.
