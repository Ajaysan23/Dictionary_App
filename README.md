# Dictionary_App
#Import pickle to make serilization
import pickle

#The function to take word input and appropriate meaning to that word
def add_word(word_dict):
    word = input("Enter word: ")
    meaning = input("Enter meaning: ")
    word_dict[word] = meaning
    save_words(word_dict)
    print("Word added successfully!")

#The function returns meaning to the inout word
def find_meaning(word_dict):
    word = input("Enter word to find meaning: ")
    if word in word_dict:
        print("Meaning: ", word_dict[word])
    else:
        print("Word not found in dictionary.")

#If user wants to update the meaning this function will run
def update_word(word_dict):
    word = input("Enter word to update: ")
    if word in word_dict:
        meaning = input("Enter new meaning: ")
        word_dict[word] = meaning
        save_words(word_dict)
        print("Word updated successfully!")
    else:
        print("Word not found in dictionary.")

#This function takes a dictionary word_dict as input and saves it to a file named 'words.txt' using pickle for serialization.
def save_words(word_dict):
    with open('words.txt', 'wb') as file:
        pickle.dump(word_dict, file)

#This function loads the dictionary from the 'words.txt' file using pickle and returns it. If the file is not found, an empty dictionary is returned        
def load_words():
    try:
        with open('words.txt', 'rb') as file:
            word_dict = pickle.load(file)
    except FileNotFoundError:
        word_dict = {}
    return word_dict

''' 
This is the main function of the dictionary app that displays a menu to the user 
and takes input for different operations based on the user's 
choice. It calls the respective functions to perform the desired operation, until the user chooses to exit 
'''

def main():
    word_dict = load_words()
    while True:
        print("Main Menu\n1. Add a new word\n2. Find the meaning\n3. Update a word\n4. Exit")
        choice = input("Enter Choice: ")
        if choice == '1':
            add_word(word_dict)
        elif choice == '2':
            find_meaning(word_dict)
        elif choice == '3':
            update_word(word_dict)
        elif choice == '4':
            print("Thank you for using the dictionary app!")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == '__main__':
    main()
