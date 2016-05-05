{:title "Anagram Kata"
:layout :post
:tags ["katas" "clojure" "tdd"]}

I have an interview tomorrow, and so I decided to warm up with one of
the coding katas from [here](http://codekata.com/kata/kata06-anagrams/).
The challenge is to take a list of words, one per line, and append to
the end of the line all anagrammatic words for that word from throughout
the list.

I stumbled through a few approaches, but settled on the following:

1.  Create a hashmap with the alphabetized letters of each word forming
    each key, and a sorted set of each word with those letters as the
    values for each key.
2.  For each line in the original file, alphabetize the letters and
    lookup the corresponding key in the hashmap from step 1.
3.  Append all of the anagrams after the original word after removing
    the second appearance of the word (it will appear twice because the
    value will show up both as the original word and as an entry in the
    hashmap).

I wrote the tests and implementation as follows:

### `alphabetize-letters`

Test:

    (deftest alphabetize-letters-test
      (is (= "act" (alphabetize-letters "cat")))
      (is (= "foo" (alphabetize-letters "ofo")))
      (is (= "" (alphabetize-letters ""))))

Code:

      (defn alphabetize-letters [word]
        (apply str (sort word)))

### `make-dictionary`

Test:

    (deftest make-dictionary-test
      (is (= {"aet" #{"ate" "eat" "tae" "tea"}
              "moo" #{"moo"}
              "cow" #{"cow"}
              "aept" #{"pate"}}
            (make-dictionary test-list))))

Code:

    (defn make-dictionary [coll]
      (reduce
      (fn [accum el]
        (update accum (alphabetize-letters el) #(apply sorted-set (conj % el))))
      {}
      coll))
      
### `make-anagram-list`

Test:

    (def test-list #{"tea" "eat" "ate" "tae" "moo" "cow" "pate"})

    (deftest make-anagram-list-test
      (is (= [["ate" "eat" "tae" "tea"]
              ["cow"]
              ["eat" "ate" "tae" "tea"]
              ["moo"]
              ["pate"]
              ["tae" "ate" "eat" "tea"]
              ["tea" "ate" "eat" "tae"]]
            (make-anagram-list test-list))))

Code:

    (defn make-anagram-list [coll]
      (let [entries (sort coll)
            dictionary (make-dictionary coll)]
        (reduce
        (fn [accum el]
          (conj
            accum
            (distinct (vec (cons el (get dictionary (alphabetize-letters el)))))))
        []
        entries)))
        

### `main`

    (defn -main [& args]
      (let [in-file (first args)
            out-file (second args)
            word-list (import-wordlist in-file)
            anagram-list (make-anagram-list word-list)
            out-string (clojure.string/join "\n" (map #(clojure.string/join " " %) anagram-list))]
        (spit out-file out-string)))

Conclusion
----------

I suspect this could be faster if the code run on each entry were
optimized, but compiling the dictionary should only take linear time (it
walks the input string once) and the building up of the output string
should also take linear time (because the hashmap lookups take O(1)
time, as I understand it).
