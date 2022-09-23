import java.util.*;

public class AbsurdleManager {
    private Set<String> wordsPossible;
    private static int length;

    // pre: Throws an IllegalArgumentException if length is 
    //      less than 1 
    // post: Initializes a new game of Absurdle and adds all words
    //       from the dictionary to the set
    public AbsurdleManager(Collection<String> dictionary, int length) {
        this.length = length;
        if (length < 1) {
            throw new IllegalArgumentException();
        }
        wordsPossible = new TreeSet<String>();
        for (String word : dictionary) {
            if (word.length() == length) {
                wordsPossible.add(word);
            }
        }
    }

    // The comment for this method is provided. Do not modify this comment:
    // Params:
    //  String word -- the secret word trying to be guessed. Assumes word is made up of only
    //                 lower case letters and is the same length as guess.
    //  String guess -- the guess for the word. Assumes guess is made up of only
    //                  lower case letters and is the same length as word.
    // Exceptions:
    //   none
    // Returns:
    //   returns a string, made up of gray, yellow, or green squares, representing a
    //   standard wordle clue for the provided guess made against the provided secret word.
    public static String patternFor(String word, String guess) {
        String[] pattern = new String[word.length()];
        Map<Character, Integer> counts = new TreeMap<>();
        for (int i = 0; i < word.length(); i++) {
            if (!(counts.containsKey(word.charAt(i)))) {
                counts.put(word.charAt(i), 1);
            } else {
                counts.put(word.charAt(i), counts.get(word.charAt(i)) + 1);
            }
        }
        for (int i = 0; i < word.length(); i++) {
            if (word.charAt(i) == guess.charAt(i)) {
                pattern[i] = "🟩";
                counts.put(guess.charAt(i), counts.get(guess.charAt(i)) - 1);
            }
        }
        for (int i = 0; i < word.length(); i++) {
            if (pattern[i] == null && counts.containsKey(guess.charAt(i)) 
                && counts.get(guess.charAt(i)) != 0) {
                pattern[i] = "🟨";
                counts.put(guess.charAt(i), counts.get(guess.charAt(i)) - 1);
            }
        }
        for (int i = 0; i < word.length(); i++) {
            if (pattern[i] == null) {
                pattern[i] = "⬜";
            }     
        }
        String result = "";
        for (int i = 0; i < pattern.length; i++) {
            result += pattern[i];
        }
        return result;
    }

    // post: accesses the current set of words considered by the manager
    public Set<String> words() {
        return wordsPossible;
    }
    
    // pre: Throws an IllegalStateException if the set of words
    //      is empty, throws an IllegalArgumentException if the 
    //      guess does not have the correct length
    // post: Determines the next set of words under consideration, returns the
    //       pattern for the guess, and updates the current set of words
    public String record(String guess) {
        if (wordsPossible.isEmpty()) {
            throw new IllegalStateException();
        }
        if(guess.length() != length) {
            throw new IllegalArgumentException();
        }
        Map<String, Set<String>> patternMap = new TreeMap<>();
        for (String word: wordsPossible) {
            String patternTracker = patternFor(word, guess);
            Set<String> wordSets = new TreeSet<String>();
            if(!patternMap.containsKey(patternTracker)) {
                patternMap.put(patternTracker, wordSets);
            }
            patternMap.get(patternTracker).add(word);
        }
        int maxSet = 0;
        String toReturn = "";
        for(String pattern: patternMap.keySet()) {
            if(patternMap.get(pattern).size() > maxSet) {
                maxSet = patternMap.get(pattern).size();
                toReturn = pattern;
            }
        }
        wordsPossible = patternMap.get(toReturn);
        return toReturn;
    }
}

 
