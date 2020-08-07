# sherlockAndAnagrams
HackeRrank Solution to Sherlock And Anagrams


```go
// Complete the sherlockAndAnagrams function below.
func sherlockAndAnagrams(s string) int32 {

	// fmt.Println("\nStart")

	var anagrams int32
	subStrings := []string{}

	// get all possible substrings
	for i, _ := range s { // for each rune in s
		for j := i + 1; j < len(s)+1; j++ { // for each remaining rune in s from i
			subStrings = append(subStrings, s[i:j]) // add the substring to subStrings
		}
	}
	// fmt.Println(subStrings)

	for i, subString := range subStrings { // for each substring at i
		remSubstrings := subStrings[:i]              // get remaining substrings after i
		for _, altSubString := range remSubstrings { // compare substring to every remaining substring
			if isAnagram(subString, altSubString) { // if they are anagrams
				anagrams++ // increment the anagram counter
			}
		}
	}

	return anagrams // return final count of anagrams
}

// isAnagram : compare two strings to determine if they are anagrams
func isAnagram(s1, s2 string) bool {

	if len(s1) != len(s2) { // if s1 and s2 are not the same length
		return false // they cannot be anagrams
	}

	runeCount := map[rune]int{} // data structure to count each rune

	for _, r := range s1 { // for each rune in s1
		runeCount[r]++ // count the occurrences of the rune
	}

	for _, r := range s2 { // for each rune in s2
		if runeCount[r] > 0 { // if it existed in s1
			runeCount[r]-- // and there are the same number in each, okay
		} else { // if the rune wasn't in s1 or there are more occurrences in s2
			// fmt.Printf("%v and %v are not anagrams\n", s1, s2)
			return false // they cannot be anagrams
		}
	}
	// fmt.Printf("!!%v and %v are anagrams!!\n", s1, s2)
	return true // if all occurrences of each rune are equal, we have an anagram
}

```
