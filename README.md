# Digital-Hiring

## Goal: 
To predict whether a candidate is a suitable match for a company based on video interview and resume data. We will then match it with the job description to see if they are a good fit for the company.

## Overall Approach:
We get data in three forms from an interviewee:
- Video - soft skills like body language
- Audio - Communication and Comprehension skills
- Text - Credibility of their skills, qualifications and work experience.
- Our approach in this project was to use these three forms of data to assess and create a ranking system among the different candidates.
- We focused on interpreting candidates' facial expressions from the video data. Facial expressions would be the closest thing to the body language of a candidate, and this would be a very good way to gauge the confidence, fear, anxiety and other feelings in a candidate during an interview.
- From the audio data, we focused on bringing out the most critical keywords told by candidates regarding their experience and skill sets. We can then map it to the requirements of companies from the job description. We can also gauge the confidence in the candidates by looking at common elocutionary mistakes made by the candidates, which may give us various signals about their comfort levels.
- From the text data, we focused on extracting the key tokens that match the job description, and based on the frequency matching, we can judge whether the candidate has the required skillsets for the job.

### Video Approach: 
- Since a video is a collection of images with 30 images or frames per second, we decided to use a few images per second so that we don’t have to deal with computational complexity. At the same time, there won’t be information loss if we suppose three images per second.
- Now, we work on using these images to identify facial features, which will help us identify the different types of expressions portrayed by interviewees.
- We have seven classes, and depending on the moods like happiness, sadness, neutrality, contempt, etc., we can give an overall score on the candidate’s emotions during the interview.
- We will have positivity, negativity, and neutrality scores accordingly.
- We run this model locally, using the Kaggle Dataset.


### Audio Approach:
- We take the .mp4 video file and use it to convert it to an audio file with the help of the Moviepy library. Link: https://pypi.org/project/moviepy/
- This audio is then converted into text or transcript using the Whisper library from OpenAI. We run this library on Google Colab due to hardware constraints to run it locally. We took help of this particular repository for Whisper API : https://github.com/openai/whisper
- The audio transcript is now analysed using three methods:
- **_Silence Time Analysis_**: Based on the change in the decibels of sound emitted during an interview, we can identify moments of silence where a candidate cannot think on their feet and are underconfident about their abilities to convert their free-flowing thoughts into speech. We use a threshold of 3s to help us identify their confidence in their speech. This can determine their soft skills, like good oratory skills.
- **_Emotion Analysis_**: We use the VADER(a sentiment reasoning library) and the NLTK library to determine whether the text expresses a positive, negative or neutral emotion. This can again be used to determine their soft skills, like good oratory skills.
- **_Filler Word Analysis_**: Due to the inability to frame proper sentences in high-pressure environments, candidates may not properly structure their sentences, which can hamper their ability to communicate effectively.
- We then use a weighted combination of all three scores from this analysis to get their conversational skills points out of 100.


### Text Approach:
- We used job description key matching between the job description and the audio transcribed files. In this, we used the word2vec library to perform semantic analysis and also used cosine similarity. Further, we identified mean cosine similarity for a particular candidate and did the matching for the sub-rating of skills.
- Use of SemanticLSTM - We used this approach to identify the comprehension skills of an interviewee based on how they are portraying their skills.   
- We also did the key matching between the resume and the audio transcribed files. In this, we used frequency matching for the words.
- We also used the LeetCode API to find different metrics in a candidate’s coding ability - 
- Number of Easy/Medium/Hard questions solved
- LeetCode Rank
