# Coding-Assignment
The Python code for the "A permutation Check" assignment is available in this repository. Finding all possible combinations of a particular pattern.   Input/Output: The code accepts input in the form of several test cases, . It produces "YES" in each case when a permutation is found and "NO" in the absence of one.
from collections import Counter

Code Python :
def is_permutation_present(pattern, text):
    # Create counters for the given pattern and initial portion of the text
    pattern_counter = Counter(pattern)
    text_counter = Counter(text[:len(pattern)])

    # Check if the initial portion of the text is a permutation of the pattern
    if pattern_counter == text_counter:
        return "YES"

    # Iterate through the remaining part of the text using the sliding window technique
    for i in range(len(pattern), len(text)):
        # Update the text_counter for the sliding window
        text_counter[text[i - len(pattern)]] -= 1
        if text_counter[text[i - len(pattern)]] == 0:
            del text_counter[text[i - len(pattern)]]
        text_counter[text[i]] += 1

        # Check if the current window is a permutation of the pattern
        if pattern_counter == text_counter:
            return "YES"

    # If no permutation is found, return "NO"
    return "NO"

# Sample Input
sample_input = """3
hack
indiahacks
code
eddy
coder
iamredoc"""

# Process Sample Input
input_lines = sample_input.strip().split('\n')
T = int(input_lines[0])
test_cases = input_lines[1:]

# Process and Output Results
for i in range(0, 2 * T, 2):
    current_pattern = test_cases[i].strip()
    current_text = test_cases[i + 1].strip()
    result = is_permutation_present(current_pattern, current_text)
    print(result)

