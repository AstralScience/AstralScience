- 👋 Hi, I’m @AstralScience
- 👀 I’m interested in nuclear science and mathematics
- 🌱 I’m currently learning computer programming and science
- 💞️ I’m looking to collaborate on wikis and neural networks
- 📫 How to reach me: you don't

<!---
AstralScience/AstralScience is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

Here's some random source code.
```pyimport time
import nltk
import math
import random
from nltk.corpus import words
nltk.download('words')
english_dictionary = words.words()
wordlisting = english_dictionary
print("Length of dictionary: " + str(len(wordlisting)))


def check(give):
    difp = []
    resultant = give
    for n in range(0, len(resultant)-1):
        if resultant[n] == resultant[len(resultant)-1]:
            break
        worden = resultant[n]
        wordenmap = list(map(str, worden))
        print(worden)
        difp = []
        for m in range(resultant.index(worden), len(resultant)):
            sened = resultant[m]
            senemap = list(map(str, sened))
            print(worden + " " + sened)
            difn = 0
            for l in range(0, len(resultant[0])):
                if senemap[l] == wordenmap[l]:
                    difn += 1

            difp.append(difn)
        print(difp)
        difm = difp[::-1]
        print(difm)
        if len(resultant[0]) - 1 in difm:
            pra = difm.index(len(resultant[0]) - 1)
        pentarn = len(resultant) - 1 - pra
        print(pentarn)
        if pentarn > n+1:
            c = 0
            for g in range(n + 1, pentarn):
                resultant.pop(g-c)
                c += 1


    return resultant


check(["a","b","c"])



change = []
score = []
letters = []
final_score = []
used_paths = [math.inf]
used_paves = [["1"]]
extra = 0
stop = 0
start = input("Please choose a starting word from the English dictionary: ")
end = input("Now choose a ending word, it must have the same length as the starting word (" + str(len(start)) + ")i: ")
maxim = int(input("Alright, now choose a maximum amount of steps, if you don't want a maximum, choose 25: "))
minim = int(input("All done! Now this one is optional, if you want to have a minimum amount of steps, input it now. If not, choose 0: "))
locked = bool(input("Final question, do you want the program to run continuously to find the optimal path? (true/false): "))
used = [start]
word = start
steps = 0
if start in wordlisting:
    print("Starting word is good")
else:
    print("Starting word has been denied, please reset.")
    start = "cat"
    end = "dog"
if end in wordlisting:
    print("Ending word is good")
else:
    print("Ending word has been denied, please reset.")
    wordlisting.append(end)
if len(start) != len(end):
    print("Length doesn't match, please reset.")
    start = "cat"
    end = "dog"
wordlisting.remove(start)
finished = 0
finish_steps = 149
if not locked:
    while finish_steps > maxim or finish_steps < minim:
        print(0)
        print(start)
        steps = 0
        while word != end and stop == 0:
            change = []
            score = []
            letters = []
            final_score = []
            for i in range(0, len(wordlisting)):
                wording = wordlisting[i]
                word_map = list(map(str, wording))
                count = len(word_map)
                origmap = list(map(str, word))
                oricount = len(origmap)
                guess_change = 0
                if oricount == count:
                    letters.append(0)
                    for a in range(0, count):
                        if word_map[a] == origmap[a]:
                            guess_change += 1
                else:
                    letters.append(1)
                    guess_change = -5
                if guess_change == (oricount - 1):
                    change.append(1)
                else:
                    change.append(0)
                endmap = list(map(str, end))
                total_score = 0
                if count == len(endmap):
                    for a in range(0, count):
                        if word_map[a] == endmap[a]:
                            total_score += 1
                if wording == end:
                    score.append(999999999999999999)
                else:
                    score.append(total_score)
            for i in range(0, len(wordlisting)):
                appendable = change[i] * score[i] - (letters[i] * 999999999)
                final_score.append(appendable)
            maxi = max(final_score)
            filtered = [i for i, x in enumerate(final_score) if x == maxi]
            ind = random.choice(filtered)
            new_word = wordlisting[ind]
            word = new_word
            wordlisting.remove(word)
            if word in wordlisting:
                wordlisting.remove(word)
            if word[0].upper() + word[1:] in wordlisting:
                wordlisting.remove(word[0].upper() + word[1:])
            if word[0].upper() + word[1:] in wordlisting:
                wordlisting.remove(word[0].upper() + word[1:])

            steps += 1
            if steps > maxim:
                stop = 1
            used.append(new_word)
            print(steps)
            print(new_word)
            if steps >= 150:
                print("MAXIMUM LIMIT REACHED, CANNOT FIND REASONABLE PATH.")
                if steps <= maxim:
                    extra = 1
                stop = 1
            if steps < 10 and word == "Aaronic":
                print("PROBABLE PATH IS UNLIKELY TO BE FOUND (DUE TO THE FACT THAT THE WORD AARONIC WAS FOUND.)")
                if steps <= maxim:
                    extra = 1
                stop = 1
            if change[ind] != 1:
                print("PATH IS IMPROBABLE, SINCE TWO WORDS DO NOT MATCH.")
                if steps <= maxim:
                    extra = 1
                stop = 1
        if stop == 0:
            used = check(used)
        used = ' > '.join(used)
        if steps < 150 and stop != 1:
            print("FINISHED!")
            print("Total Steps: " + str(steps))
            print(used)
            print(" ")
            print("Details:")
            print("Starting Word: " + start)
            print("Ending Word: " + end)
            print(" ")
            print("Amount of Steps: " + str(steps))
            print("Used Path: " + str(used))
            print(" ")
            print("Score: " + str(max(min((maxim * 2 - steps) / (maxim / 100), 100), 0)) + "%")
        else:
            print("Path not succesfully found.")
        word = start
        if extra == 1:
            finish_steps = 149
        else:
            finish_steps = steps
        used = [start]
        chance = random.randint(3, 5)
        if chance == 5:
            wordlisting = words.words()
            print("Dictionary Reset")
        wordlisting.append(end)
        wordlisting.append(end)

        stop = 0
        extra = 0
if locked:
    while locked:
        print(0)
        print(start)
        steps = 0
        while word != end and stop == 0:
            change = []
            score = []
            letters = []
            final_score = []
            for i in range(0, len(wordlisting)):
                wording = wordlisting[i]
                word_map = list(map(str, wording))
                count = len(word_map)
                origmap = list(map(str, word))
                oricount = len(origmap)
                guess_change = 0
                if oricount == count:
                    letters.append(0)
                    for a in range(0, count):
                        if word_map[a] == origmap[a]:
                            guess_change += 1
                else:
                    letters.append(1)
                    guess_change = -5
                if guess_change == (oricount - 1):
                    change.append(1)
                else:
                    change.append(0)
                endmap = list(map(str, end))
                total_score = 0
                if count == len(endmap):
                    for a in range(0, count):
                        if word_map[a] == endmap[a]:
                            total_score += 1
                if wording == end:
                    score.append(999999999999999999)
                else:
                    score.append(total_score)
            for i in range(0, len(wordlisting)):
                appendable = change[i] * score[i] - (letters[i] * 999999999)
                final_score.append(appendable)
            maxi = max(final_score)
            filtered = [i for i, x in enumerate(final_score) if x == maxi]
            ind = random.choice(filtered)
            new_word = wordlisting[ind]
            word = new_word
            wordlisting.remove(word)
            if word in wordlisting:
                wordlisting.remove(word)
            if word[0].upper() + word[1:] in wordlisting:
                wordlisting.remove(word[0].upper() + word[1:])
            if word[0].upper() + word[1:] in wordlisting:
                wordlisting.remove(word[0].upper() + word[1:])

            steps += 1
            if steps > maxim:
                stop = 1
            used.append(new_word)
            print(steps)
            print(new_word)
            if steps >= 25:
                print("MAXIMUM LIMIT REACHED, CANNOT FIND REASONABLE PATH.")
                stop = 1
            if steps < 10 and word == "Aaronic":
                print("PROBABLE PATH IS UNLIKELY TO BE FOUND (DUE TO THE FACT THAT THE WORD AARONIC WAS FOUND.)")
                stop = 1
            if change[ind] != 1:
                print("PATH IS IMPROBABLE, SINCE TWO WORDS DO NOT MATCH.")
                stop = 1
        if stop == 1:
            finish_steps = 999999
        else:
            finish_steps = steps
        used_paths.append(finish_steps)
        used_paves.append(used)
        if stop == 0:
            used = check(used)
            steps = len(used) - 1
        used = ' > '.join(used)
        if steps < 150 and stop != 1:
            optimal_path = min(used_paths)
            pre_pave = used_paths.index(optimal_path)
            optimal_pave = used_paves[pre_pave]
            print("FINISHED!")
            print("Total Steps: " + str(steps))
            print(used)
            print(" ")
            print("Details:")
            print("Starting Word: " + start)
            print("Ending Word: " + end)
            print(" ")
            print("Amount of Steps: " + str(steps))
            print("Used Path: " + str(used))
            print(" ")
            print("Score: " + str(max(min((maxim * 2 - steps) / (maxim / 100), 100), 0)) + "%")
            print(" ")
            print("Optimal Path:")
            print("Optimal Score: " + str(optimal_path) + " steps")
            print("Current Optimal Path: " + str(' > '.join(optimal_pave)))

        else:
            print("Path not succesfully found.")
        word = start
        used = [start]
        chance = random.randint(3, 5)
        if chance == 5:
            wordlisting = words.words()
            print("Dictionary Reset")
        wordlisting.append(end)
        wordlisting.append(end)
        print(used_paths)
        print(used_paves)


        stop = 0
        extra = 0




```
