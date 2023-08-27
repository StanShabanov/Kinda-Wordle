//Stan Shabanov
//2/16/2023
//Absurdle

//Absurdle The game provides feedback on each guess, indicating which letters are 
//correct and in the correct position, which letters are correct but in 
//the wrong position, and which letters are incorrect. The objective of 
//the game is to guess the word as quickly as possible using the feedback 
//provided after each guess. Wordle is a simple yet addictive game that 
//challenges players' vocabulary, logic, and deduction skills.

import java.util.*;
import java.io.*;

public class Absurdle  {
    public static final String GREEN = "🟩";
    public static final String YELLOW = "🟨";
    public static final String GRAY = "⬜";

    // [[ ALL OF MAIN PROVIDED ]]
    public static void main(String[] args) throws FileNotFoundException {
        Scanner console = new Scanner(System.in);
        System.out.println("Welcome to the game of Absurdle.");

        System.out.print("What dictionary would you like to use? ");
        String dictName = console.next();

        System.out.print("What length word would you like to guess? ");
        int wordLength = console.nextInt();

        List<String> contents = loadFile(new Scanner(new File(dictName)));
        Set<String> words = pruneDictionary(contents, wordLength);

        List<String> guessedPatterns = new ArrayList<>();
        while (!isFinished(guessedPatterns)) {
            System.out.print("> ");
            String guess = console.next();
            String pattern = record(guess, words, wordLength);
            guessedPatterns.add(pattern);
            System.out.println(": " + pattern);
            System.out.println();
        }
        System.out.println("Absurdle " + guessedPatterns.size() + "/∞");
        System.out.println();
        printPatterns(guessedPatterns);
    }

    // [[ PROVIDED ]]
    // Prints out the given list of patterns.
    // - List<String> patterns: list of patterns from the game
    public static void printPatterns(List<String> patterns) {
        for (String pattern : patterns) {
            System.out.println(pattern);
        }
    }

    // [[ PROVIDED ]]
    // Returns true if the game is finished, meaning the user guessed the word. Returns
    // false otherwise.
    // - List<String> patterns: list of patterns from the game
    public static boolean isFinished(List<String> patterns) {
        if (patterns.isEmpty()) {
            return false;
        }
        String lastPattern = patterns.get(patterns.size() - 1);
        return !lastPattern.contains("⬜") && !lastPattern.contains("🟨");
    }

    // [[ PROVIDED ]]
    // Loads the contents of a given file Scanner into a List<String> and returns it.
    // - Scanner dictScan: contains file contents
    public static List<String> loadFile(Scanner dictScan) {
        List<String> contents = new ArrayList<>();
        while (dictScan.hasNext()) {
            contents.add(dictScan.next());
        }
        return contents;
    }

    // TODO: Write your code here! 
    //This method adds works from list of contents provided and uses word length.
    //it also makes sure there are no duplicates. 
    //Parameters: 
    // - contents : used from the dictionary 
    // - wordLength: the words of length that the user provided
    // Returns:
    //    - userinput: words that fit the word length
    public static Set<String> pruneDictionary(List<String> contents, int wordLength) {
        if (wordLength < 1) {
        throw new IllegalArgumentException();
        }

        Set<String> userInput = new HashSet<>();
        for(String words : contents){
            if(words.length() == wordLength){
                userInput.add(words);
            }
        }   
        return userInput;
    }
    //this method provides set of words that showcases the real words
    //Parameters:
    //    - guess: the word the user guessed
    //    - words: all words that have been inputed
    //    - wordlength: length of the word the user has inputed
    //Returns:
    //    - String: the last method for the target word
    public static String record(String guess, Set<String> words, int wordLength) {
        if(words.isEmpty() || guess.length() != wordLength){
        throw new IllegalArgumentException();
        }
        Map<String, Set<String>> userGuesses = new TreeMap<>();
        for(String word : words){
            String userPattern = patternFor(word, guess);
            if(!userGuesses.containsKey(userPattern)){
                userGuesses.put(userPattern, new TreeSet<>());
            }
        userGuesses.get(userPattern).add(word);
        }
        words.clear();
        String userKeyPattern = "";
        for(String key : userGuesses.keySet()){
            if(userGuesses.get(key).size() > words.size()){
                words.clear();
                words.addAll(userGuesses.get(key));
                userKeyPattern = key;
            }
        }

        return userKeyPattern;


    }
    //this method checks the user inut of the word and uses it to match
    //and return a check boxes of patterns that light up based on the word input
    // Parameters:
    //    - word: the target word
    //    - guess: the word the user guessed or inputed
    // Returns:
    //    - String: for the target word of last method 
    public static String patternFor(String word, String guess) {
        for(int i = 0; i < word.length(); i++){
            char current = guess.charAt(i);
            if (current == word.charAt(i) && Character.isLetter(current)){
                guess = changeInputWord(guess, '!', i);
                word = changeInputWord(word, '!', i);
            }
        }

        for(int i = 0; i < word.length(); i++){
            char current = guess.charAt(i);
            if(Character.isLetter(current)){
                int currentIndex = word.indexOf(current);
                if (currentIndex >= 0){
                    guess = guess.replaceFirst("" + current, "&" );
                    word = word.replaceFirst("" + current, "&" );
                }
            }
        }

        for(int i = 0; i < word.length(); i++){
            char current = guess.charAt(i);
            if(Character.isLetter(current)){
                guess = changeInputWord(guess, '#', i);
                word = changeInputWord(word, '#', i);
            }
        }
        return changeExpression(guess);
        }
    
    //this method changes the input of words provided by user to match to 
    // a target characters
    //Parameters:
    //  -ouput: change that will happen to the words
    //  -character: the character and non-letter it will be transformed to
    //  -i: the indexes that shall not be changed
    //Returns:
    //  -String: non-leter character for the word guessed and target word wich is a pattern
    public static String changeInputWord(String output, char character, int i){
        return output.substring(0, i) + character + output.substring(i+1);
    }
    //this method will use the changeInputWord method to get the non-character
    //words to be implemeted as a expression.
    //Parameters:
    //  -ouput: word that is going to change to a visible output
    //Returns:
    //  -String: non-leter character for the word guessed and target word wich is a pattern
    public static String changeExpression(String output){
        output = output.replace("!" , "🟩");
        output = output.replace("&" , "🟨");
        output = output.replace("#" , "⬜");
        return output;
    }
}
