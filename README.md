# Question-Answer-Generator

Hi everyone! I created this project for fun, where I use Google's Flan-T5 to generate question-answer pairs from a given Wikipedia link.

**Why Google's Flan-T5?**

In this project, I am using Google's Flan-T5 'base' version. Flan stands for Fine-tuned LAnguage Net while T5 stands for Text-to-Text Transfer Transformer.

Flan-T5 is a pre-trained NLP model that was trained for a variety of language tasks such as translation, summarization, and question answering (QA). Since QA is one of the tasks it was trained on, Flan-T5 is appropriate for this task, as that's half of the battle done! Many of the tasks used to train Flan-T5 also heavily involve questions, such as logical reasoning and verifying scientific facts. Hence, the transfer learning is effective for something as general as generating questions.

I used the base version as it's the standard version, and this small-scale task does not benefit from using the Large or XXL version.

##Evaluating the Results

**Relevance**

From the example of Skyrim above, we can see that the question-pairs are pretty good and produce both general ("What is the name of the game world that the team set the game in?") and detailed ("What is the name of the game that Skyrim has been credited with influencing?") questions.

However, the questions can be too general sometimes. There are questions like:

- "What is the name of the game that was released worldwide for Microsoft Windows, PlayStation 3, and Xbox 360?"
- "What is the name of the game that was released in June 2013?"

The model produces questions like this because it processes the texts by themselves, in isolation from the other paragraphs and also the broader general knowledge.

**Correctness**

Generally, the answers are correct as long as the correct answer is found nearby. Otherwise, the model seems to confuse nearby proper nouns as the answer. For example:

Question: "Who is the captured dragon?"

Context: "The Dragonborn's allies hatch a plan to capture a dragon at Whiterun. The Dragonborn helps negotiate a truce in the civil war to prevent either side from capturing Whiterun during this delicate operation. The captured dragon, Odahviing, questions whether Alduin deserves lordship over dragons."

Since the ground truth, "Odahviing," is found 2 sentences away from the mention of the captured dragon, the model assigns a higher probability to "Whiterun," a location, instead.

**Improvements**

The most immediate improvement to this model is to add the ability to take into account the whole Wikipedia page as input at once before generating questions. This will encourage the model to generate more relevant questions instead of looking at each paragraph in isolation. Currently, the limit is at 512 characters, and expanding it would require much more computational power.

**Play around with it and hope you have fun!**
