# README for `new_split` Function

The `new_split` function is a C function designed to split a given input string `s` into an array of tokens based on a set of specified delimiters. This function dynamically allocates memory to store the tokens and returns a pointer to an array of character pointers (i.e., a "double-pointer" or `char **`) that represent the individual tokens extracted from the input string. 

## Function Signature

```c
char **new_split(char *s, char *delimiters);
```
## Difference between My new_split function and a typical split function

Certainly, you can highlight the key difference between My `new_split` function and a typical split function as follows:

- **Custom `new_split` Function**: my `new_split` function splits the input string based on the delimiters while retaining the delimiters themselves in the resulting 2D array. In other words, the delimiters are included as separate tokens in the array.

- **Typical Split Function**: A typical split function, found in many programming languages and libraries, splits the input string based on the delimiters but excludes the delimiters from the resulting array of tokens. It focuses on extracting the content between delimiters.

Here's an example to illustrate the difference:

Suppose we have the input string: `"Hello, world! This is a 'sample string' with delimiters."` and we want to split it using `, ! '` as delimiters.

- **Custom `new_split` Function Result**:
  - Token 0: `"Hello"`
  - Token 1: `","`
  - Token 2: `"world"`
  - Token 3: `"!"`
  - Token 4: `"This"`
  - Token 5: `"is"`
  - Token 6: `"a"`
  - Token 7: `"'sample string'"`
  - Token 8: `"with"`
  - Token 9: `"delimiters."`

- **Typical Split Function Result** (for comparison):
  - Token 0: `"Hello"`
  - Token 1: `"world"`
  - Token 2: `"This"`
  - Token 3: `"is"`
  - Token 4: `"a"`
  - Token 5: `"sample string"`
  - Token 6: `"with"`
  - Token 7: `"delimiters."`

In summary, My `new_split` function keeps the delimiters as separate tokens in the resulting array, while a typical split function omits the delimiters and focuses solely on the content between them. This key distinction can be useful depending on the specific requirements of My application.

## Parameters

- `s` (Input): The input string that needs to be split into tokens.
- `delimiters` (Input): A string containing the characters that will be used as delimiters to separate the input string into tokens.

## Return Value

- `char **`: A pointer to an array of character pointers (strings) representing the individual tokens extracted from the input string. The array is terminated with a `NULL` pointer.

## Function Description

The `new_split` function employs a variety of techniques to parse the input string `s` and extract tokens based on the specified delimiters. Here is a step-by-step explanation of how the function works:

1. **Memory Allocation**: The function starts by allocating memory for an array of character pointers (i.e., the `tokens` array) to store the extracted tokens. Initially, the size of this array is set to the length of the input string `s`. If memory allocation fails, the function prints an error message and exits.

2. **Tokenization Loop**: The function iterates through each character in the input string `s` while maintaining pointers to the start and end of the current token being processed. It also keeps track of whether it is inside a pair of single or double quotes, which can affect how delimiters are treated.

3. **Quote Handling**: If the function encounters single or double quotes, it toggles the `in_quotes` flag to indicate whether it is inside quotes. It also keeps track of the type of quote character encountered. The `escaped` flag is used to handle escaped characters within quotes.

4. **Delimiter Detection**: When a delimiter character is encountered (unless it's inside quotes or escaped), the function checks if there is a non-empty token to extract. If so, it dynamically allocates memory for the token and copies the characters from `start` to `end`. The token is then added to the `tokens` array. If the `tokens` array is full, it is dynamically resized to accommodate more tokens.

5. **Continuation**: After processing a token, the `start` pointer is updated to the character immediately following the delimiter.

6. **Escaped Character Handling**: The `escaped` flag is used to indicate that a backslash character was encountered within quotes. It is toggled to prevent treating the following character as a delimiter.

7. **Final Tokenization**: Once the loop completes, the function checks if there is an unprocessed token at the end of the input string. If so, it follows the same tokenization process as before.

8. **Termination**: The array of tokens is terminated with a `NULL` pointer to indicate the end of the token list.

## Error Handling

- If memory allocation fails at any point, the function prints an "allocation err" message and exits with a status code of 1.

## Example Usage

Here's an example of how you can use the `new_split` function:

```c
char *input_string = "Hello, world! This is a 'sample string' with delimiters.";
char *delimiter_chars = " ,!'";
char **tokens = new_split(input_string, delimiter_chars);

// Iterate through and print the tokens
for (int i = 0; tokens[i] != NULL; i++) {
    printf("Token %d: %s\n", i, tokens[i]);
}

// Don't forget to free the allocated memory when done
for (int i = 0; tokens[i] != NULL; i++) {
    free(tokens[i]);
}
free(tokens);
```

## Note

- Ensure that you free the allocated memory for tokens when you are done using them to prevent memory leaks.

Please feel free to modify and integrate this function into My C program as needed.