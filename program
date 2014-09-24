#This program searches through text files and identifies several attributes:
#Number of characters, sentences, words, unique words. As well, % unique words,
#longest word, and a list of the top 10 most frequent words over 5 letters.

import collections

def readFile(fileName):
    """
    This function opens and reads a text file.
    """
    inFile = open(fileName, "r")
    fileContentsList = inFile.read()
    inFile.close()
    return fileContentsList

def cleanText(aList):
    """
    This function "cleans" the text file by replacing linefeeds, double spaces, and hypens
    with a single space. It also converts all the letters in the string to lower case.
    """
    cleanString = " "
    cleanText = aList.replace("\n", " ")
    cleanText2 = cleanText.replace("-", " ")
    for aChar in cleanText2:
        if aChar.isalpha() or aChar == " ":
            cleanString = cleanString + aChar
    lowerCaseText = cleanString.lower()
    while lowerCaseText.count("  ") > 0:
        lowerCaseText = lowerCaseText.replace("  ", " ")
    return lowerCaseText
 
def splitText(string):
    """
    This function splits the text into a list, using a single "space" as the delimiter.
    """
    aList = []
    aList = string.split(" ")
    return aList

def sortedList(aList):
    """
    This function sorts the list alphabetically.
    """
    filteredList = filter(None, aList)
    sortedList = sorted(filteredList)
    return sortedList

def uniqueWords(aList):
    """
    Creates a list of unique words sorted alphabetically.
    """
    uniqueWords = set(aList)
    sortedUniqueWords = sorted(uniqueWords)
    return sortedUniqueWords

def numCharacters(stuffInFile):
    """
    This function returns a list that contains all the letter found in the input string.
    """
    characterList = list(stuffInFile)
    return characterList

def numSentences(stuffInFile):
    """
    Finds total number of sentences in the text file by searching for periods,
    exclamation marks, and question marks.
    """
    period = stuffInFile.count(".")
    exclamationMark = stuffInFile.count("!")
    questionMark = stuffInFile.count("?")
    totalSentences = period + exclamationMark + questionMark
    return totalSentences

def uniqueWordPercent(uniqueWordList, cleanedTextAsList):
    """
    Calculates and returns the percent of unique words within the text.
    """
    lenUniqueWords = len(uniqueWordList)
    lenAllWords = len(cleanedTextAsList)
    percentUnique = lenUniqueWords / float(lenAllWords) * 100.0
    return percentUnique

def longestWord(uniqueWordList):
    """
    This function finds the longest unique word in a list.
    """
    longestWord = max(uniqueWordList, key=len)
    return longestWord

def dictionaryList(cleanedTextAsList, uniqueWordList):
    """
    Creates a dictionary that stores each unique word, along with its frequency,
    or number of occurrences.
    """
    dictionary = {}
    for aVal in uniqueWordList:
        lineDict = {aVal: (cleanedTextAsList.count(aVal))}
        dictionary.update(lineDict)
    return dictionary

def writeDictionary(fileName, fileContents):
    """
    Prints out the contents of a dictionary into a text file, in this case providing a
    key: value pair on every line. The key-value pairs are sorted alphabetically.
    """
    outFile = open(fileName, "w")
    sortedDict = collections.OrderedDict(sorted(fileContents.items()))
    for key, value in sortedDict.items():
        outFile.write(str(key)+ " " +str(value)+ "\n")
    outFile.close()
    
def mostUsedWords(dictionary):
    """
    When supplied a dictionary, this function will return a list of tuples containing the top ten
    most frequent words in the list over 5 letters long.
    """
    aDict = {} #This dictionary stores all words with more than 5 letters in it.
    for key, value in dictionary.items():
        if len(key) > 5:
            aDict[key] = value
    #Sorts aDict in order, from most -> least frequency. Then takes the first 10 (word, frequency) pairs.     
    topTenWords = sorted(aDict.items(), key=lambda item: -item[1])[:10] 
    return topTenWords
          
def main():
    listOfSpeeches = ("PMHarperBerlinWall.txt", "PresObamaBerlinSpeech.txt", "PresObamaInauguralAddress.txt")
    speechNames = ("Harper's Berlin Speech: ", "Obama's Berlin Speech: ", "Obama's Inaugural Address: ")
    speechDicts = ("PMHarperBerlinWallDict.txt", "PresObamaBerlinSpeechDict.txt", "PresObamaInauguralAddressDict.txt")
    #Using a for loop to iterate main 3 times (3 speeches).
    for i in range(3):
        #This set of code "cleans" the text file, preparing it into a sorted list of only words. It then
        #creates a dictionary to store these values and the frequency occurred.
        try:
            stuffInFile = readFile(listOfSpeeches[i])
        except ValueError:
            print("No text was found in this file. Please try again!")
        cleanedString = cleanText(stuffInFile) 
        textAsString = splitText(cleanedString)
        cleanedTextAsList = sortedList(textAsString)
        uniqueWordList = uniqueWords(cleanedTextAsList)
        dictionary = dictionaryList(cleanedTextAsList, uniqueWordList)

        #This set calculates the number of characters, sentences, unique word percent, longest word, writes
        #a dictionary to a text file, and writes a list of tuples of top 10 words over 5 letters long.
        numOfCharacters = numCharacters(stuffInFile)
        numOfSentences = numSentences(stuffInFile)
        percentUnique = uniqueWordPercent(uniqueWordList, cleanedTextAsList)
        longWord = longestWord(uniqueWordList)
        dictFile = writeDictionary(speechDicts[i], dictionary)
        wordsUsedMost = mostUsedWords(dictionary)

        #Prints out the various outputs calculated above.
        print(speechNames[i])
        print(str(len(numOfCharacters)) + " characters.")
        print(str(numOfSentences) + " sentences.")
        print(str(len(cleanedTextAsList)) + " words.")
        print(str(len(uniqueWordList)) + " unique words.")
        print("{0:2.1f}% of the words are unique.".format(percentUnique))
        print("Longest word is: " + longWord)
        print("\nMost used words over 5 letters are: ")
        for word, number in wordsUsedMost:
            print(str(word) + ":", str(number) +" times") #This list is ordered from most frequent -> least frequent words.
        print("-" * 30)
        

main()
