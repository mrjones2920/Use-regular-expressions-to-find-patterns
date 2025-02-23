# Use regular expressions to find patterns

<h1>Introduction</h1>
Security analysts often analyze log files, including those that contain information about login attempts. For example as an analyst, you might flag IP addresses that relate to unusual attempts to log in to the system.

Another area of focus in cybersecurity is detecting devices that require updates. Software updates help prevent security issues due to vulnerabilities.

Using regular expressions in Python can help automate the processes involved in both of these areas of cybersecurity. Regular expression patterns and functions can be used to efficiently extract important information from strings and files.

In this lab, you'll write regular expressions to extract information such as device IDs or IP addresses.

<h1>Scenario</h1>
In this lab, you're working as a security analyst and your main tasks are as follows:

extracting device IDs containing certain characters from a log; these characters correspond with a certain operating system that requires an update.
extracting all IP addresses from a log and then comparing them to those that are flagged in a list.
<h1>Task 1</h1>
In order to work with regular expressions in Python, start by importing the re module. This module contains many functions that will help you work with regular expressions. By running the following code cell, the module will be available through the rest of the notebook.

![image](https://github.com/user-attachments/assets/3a7cb0c9-30c4-4a54-9c07-76f4cdccd5d4)

<h1>Task 2</h1>
In your work as a cybersecurity analyst, you're responsible for updating devices. A device ID that begins with the characters "r15" indicates that the device has a certain operating system that must be updated.

You're given a log of device IDs, stored in a variable named devices. Your eventual goal is to extract the device IDs that start with the characters "r15". For now, display the contents of the whole string to examine what it contains. Be sure to replace the ### YOUR CODE HERE ### with your own code before you run the following cell.

![image](https://github.com/user-attachments/assets/2fcf096e-8bc8-440a-aa73-f16bfc97f26a)

<h1>Task 3</h1>
In this task, you'll write a pattern to find devices that start with the character combination of "r15".

Use the regular expression symbols \w and + to create the pattern, and store it as a string in a variable named target_pattern.

Be sure to replace the ### YOUR CODE HERE ### with your own code before you run the following cell. Note that the code cell will contain only variable assignments, so running it will not produce an output.

![image](https://github.com/user-attachments/assets/aa12cef1-b010-4db8-8c59-83cedbba3e2e)

<h1>Question 1</h1>
What regular expression pattern did you use? For each component of the pattern, what would happen if it were missing?

The regular expression pattern used was "r15\w+". Without the r15, the pattern will not match with device IDs that start with the characters "r15". Without the \w, the pattern will not match with alphanumeric characters following "r15". Without the +, the pattern will match with only the first alphanumeric character that occurs after "r15".

<h1>Task 4</h1>
Use the findall() function from the re module to find the device IDs that the target_pattern matches with. Be sure to replace the ### YOUR CODE HERE ### with your own code before you run the following cell.

Note: In order to use re.findall() in Tasks 4, 7, 8, 9 and 11, you must have previously run the code import re in Task 1.

![image](https://github.com/user-attachments/assets/4dd9bdcb-95aa-4fdf-8c8c-1a29ce3a919f)

<h1>Task 5</h1>
Now, the next task you're responsible for is analyzing a network security log file and determining which IP addresses have been flagged for unusual activity.

You're given the log file as a string stored in a variable named log_file. There are some invalid IP addresses in the log file due to issues in data collection. Your eventual goal is to use regular expressions to extract the valid IP addresses from the string.

Start by displaying the contents of the log_file to examine the details inside. Be sure to replace the ### YOUR CODE HERE ### with your own code before you run the following cell.

![image](https://github.com/user-attachments/assets/79b03581-64a1-4ce7-b1fa-bb7d30567718)

<h1>Task 6</h1>
In this task, you'll build a regular expression pattern that you can use later on to extract IP addresses that are in the form of xxx.xxx.xxx.xxx. In other words, you'll extract all IP addresses that contain four segments of three digits that are separated by periods.

Write a regular expression pattern that will match with these IP addresses and store it in a variable named pattern. Use the regular expression symbols \d and \. in your pattern. Note that the symbol \d matches with digits, in other words, any integer between 0 and 9. Be sure to replace the ### YOUR CODE HERE ### with your own code. Since you'll just build the pattern here, there won't be any output when you run this cell.

![image](https://github.com/user-attachments/assets/03e8bce0-e940-4dbe-a0bf-cedf5eff4784)

<h1>Task 7</h1>
In this task, you'll use the re.findall() function on the regular expression pattern stored in the pattern variable and the provided log_file to extract the corresponding IP addresses. Afterwards, run the cell and take note of what it outputs. Be sure to replace the ### YOUR CODE HERE ### with your own code before you run the following cell.

![image](https://github.com/user-attachments/assets/4f245b54-b868-4de2-b5eb-871ef5983ac7)

<h1>Question 2</h1>
What are some examples of IP addresses that were extracted? What are some examples of IP addresses that were not extracted? Do any that were not extracted seem to be valid IP addresses?

Examples of IP addresses that were extracted include "192.168.152.148" and "192.168.190.178". Examples of IP addresses that were not extracted include "192.168.22.115" and "1923.1689.3.24". IP addresses that have fewer then three digits per segment, such as "192.168.22.115" (which has two digits in the third segment and three digits in each of the other segments), are valid IP addresses but were not extracted.

<h1>Task 8</h1>
There are some valid IP addresses in the log_file that you haven't extracted yet. This is because each segment of digits in a valid IP address can have anywhere between one and three digits.

Adjust the regular expression in the pattern to allow for variation in the number of digits in each segment. You can do this by using the + symbol after the \d symbol. Afterwards, use the updated pattern to extract remaining IP addresses. Then, run the cell to analyze the results. Be sure to replace the ### YOUR CODE HERE ### with your own code before you run the following cell.

![image](https://github.com/user-attachments/assets/fb6aeea5-d138-4d0e-ab80-3f5b10372689)

<h1>Question 3</h1>
What gets extracted here? Do all extracted IP addresses have between one and three digits in every segment?

Now, extracted IP addresses include those with exactly three digits per segment (such as "192.168.152.148"), those with fewer than three digits per segment (such as "192.168.22.115"), and those with more than three digits per segment (such as "1923.1689.3.24"). Not all of the extracted IP addresses have between one and three digits in every segment.

<h1>Task 9</h1>
Note that all the IP addresses are now extracted but they also include invalid IP addresses with more than three digits per segment.

In this task, you'll update the pattern using curly brackets instead of the + symbol. In regular expressions, curly brackets can be used to represent an exact number of repetitions between two numbers. For example, {2,4} in a regular expression means between 2 and 4 occurrences of something. Applying this to an example, \w{2,4} would match with two, three, or four alphanumeric characters. Afterwards, you'll call the re.findall() function on the updated pattern and the log_file and store the output in a variable named valid_ip_addresses.

Then, display the contents of valid_ip_addresses and run the cell to analyze the results. Be sure to replace each ### YOUR CODE HERE ### with your own code before you run the following cell.

![image](https://github.com/user-attachments/assets/83b5df1c-0d03-4043-ac55-5de412f9963b)

<h1>Question 4</h1>
What do you notice about the extracted IP addresses here compared to those extracted in the previous two tasks?

Here, the extracted IP addresses all have between one and three digits per segment. Recall that in Task 7, only IP addresses with exactly three digits per segment were extracted. And in Task 8, IP addresses with more than three digits per segment were also extracted.

<h1>Task 10</h1>
Now, all of the valid IP addresses have been extracted. The next step is to identify flagged IP addresses.

You're given a list of IP addresses that have been previously flagged for unusual activity, stored in a variable named flagged_addresses. When these addresses are encountered, they should be investigated further. This list is just for educational purposes and contains examples of private IP addresses that are found only within internal networks.

Display this list and examine what it contains by running the cell. Be sure to replace the ### YOUR CODE HERE ### with your own code before you run the following cell.

![image](https://github.com/user-attachments/assets/07d77234-5f0c-4a82-a161-7d830f19ab09)

<h1>Task 11</h1>
Finally, you will write an iterative statement that loops through the valid_ip_addresses list and checks if each IP address is flagged. In the following code, the address will be the loop variable. Also, include a conditional that checks if the address belongs to the flagged_addresses list. If so, it should display "The IP address ______ has been flagged for further analysis." If not, it should display "The IP address ______ does not require further analysis." Be sure to replace each ### YOUR CODE HERE ### with your own code before you run the following cell.

![image](https://github.com/user-attachments/assets/156ad015-74ac-4cf6-bfdb-e1aec74ef081)

![image](https://github.com/user-attachments/assets/8dff7dfa-47ff-4d9f-97d0-edd5382b763f)

<h1>Conclusion</h1>
What are your key takeaways from this lab?

- Regular expressions in Python allow you to create patterns that you can then use to find important strings.
- Regular expression patterns can be built to match specific characters and character combinations.
- Examples of regular expression symbols practiced in this lab:
- \w represents any alphanumeric character.
-  +represents one or more occurrences of the previous character in the regular expression.
-  +\d represents any digit.
- \. represents a period.
- {x,y} represents anywhere between x and y number of occurrences of the previous character in the regular expression. The x and y can be replaced with any two positive integers to indicate an exact range for
  the number of occurrences.
- The re module in Python contains functions that are useful when working with regular expressions.
- One example is the re.findall() function, which takes in a regular expression pattern as well as a string, checks for all instances in the string that match with the pattern and outputs a list of the matches.
