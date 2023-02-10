# Assessment-
import os
import re

def check_racial_insensitivity(text):
    with open("racial_slurs.txt", "r") as file:
        racial_slurs = file.read().splitlines()
        
    for word in racial_slurs:
        if re.search(f"\\b{word}\\b", text, re.IGNORECASE):
            return "High"
    return "Low"

def get_racial_insensitivity_score(file_path):
    with open(file_path, "r") as file:
        content = file.read()
        sentences = re.split(r'[\n]+', content)
        
    racial_insensitivity_scores = {}
    for sentence in sentences:
        sentence = sentence.strip()
        if sentence:
            score = check_racial_insensitivity(sentence)
            racial_insensitivity_scores[sentence] = score
            
    return racial_insensitivity_scores

if __name__ == "__main__":
    file_path = input("Enter the file path: ")
    if os.path.exists(file_path):
        scores = get_racial_insensitivity_score(file_path)
        for sentence, score in scores.items():
            print(f"Sentence: {sentence} | Racial Insensitivity Score: {score}")
    else:
        print("The file does not exist.")
