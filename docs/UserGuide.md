---
  layout: default.md
  title: "User Guide"
  pageNav: 4
---

# UniVerse User Guide


UniVerse is more than just a **desktop app for managing contacts**—it is a platform designed to foster meaningful connections and support the holistic growth of **university students**. Tailored specifically for students balancing academic, social, and career aspirations, UniVerse allows users to organize and manage their networks effectively. By leveraging a **Command Line Interface (CLI)** for quick, efficient input and command execution, along with an intuitive **Graphical User Interface (GUI)** for easy navigation, UniVerse empowers students to maintain detailed contact information and build relationships that go beyond academic and professional circles. Whether it’s connecting with peers, professors, or industry mentors, UniVerse encourages students to form lasting bonds rooted in shared interests and experiences, making it an essential tool for thriving both socially and academically on campus.

<!-- * Table of Contents -->

<page-nav-print />

---

<div style="page-break-after: always;"></div>

## Quick start

1. Ensure you have Java `17` or above installed in your Computer.

2. Download the latest `.jar` file from [here](https://github.com/AY2425S1-CS2103T-T17-1/tp/releases).

3. Copy the file to the folder you want to use as the _home folder_ for your UniVerse application.

4. Open a command terminal, `cd` into the folder you put the jar file in, and use the `java -jar UniVerse.jar` command
   to run the application.<br>
   A GUI similar to the below should appear in a few seconds. Note how the app contains some sample data.<br>
   <img src="images/Ui.png" alt="Ui" style="width: 90%;">

5. Type the command in the command box and press Enter to execute it. e.g. typing **`help`** and pressing Enter will
   open the help window.<br>
   Some example commands you can try:

    - `list`: Lists all contacts.
    - `add n/John Doe p/98765432 e/johnd@example.com a/311, Clementi Ave 2, #02-25 u/NUS m/Computer Science b/13-12-2003`:
      Adds a contact named **John Doe** to the address book.

      <box type="info" seamless>
      
      **Note**: The `add` command supports **optional fields** such as:
        - `w/WORK_EXPERIENCE`: Specifies past work or internships (e.g., `w/Intern,Google,2023`).
        - `i/INTEREST`: Adds interests to a contact (e.g., `i/Photography`).
        - `t/TAG`: Tags to label the contact (e.g., `t/friends`).
      
      </box>

      These fields can be added to make contact information more detailed. Here’s an example with optional fields included:
      ```markdown
       add n/Alice Tan p/91234567 e/alice@example.com a/Blk 123 Clementi Ave 3, #05-10 u/NTU m/Engineering b/15-04-2000 w/Intern,Google,2023 i/Photography t/friend
      ```

    - `addi in/1 i/Reading`:
      Adds an interest called **Reading** to the contact at index 1.
    - `findu u/NUS`: Finds all contacts studying at **NUS**.
    - `findi i/Swimming`: Finds all contacts whose interests include **Swimming**.
    - `exit`: Exits the app.

6. Refer to the [Features](#features) below for details of each command.

---

<div style="page-break-after: always;"></div>

## Features

<box type="info" seamless>

**Notes about the command format:**<br>

- Words in `UPPER_CASE` are the parameters to be supplied by the user.<br>
  e.g. in `add n/NAME`, `NAME` is a parameter which can be used as `add n/John Doe`.

- Note that name cannot include prefixes that are already part of our commands.

- Items in square brackets are optional.<br>
  e.g `n/NAME [t/TAG]` can be used as `n/John Doe t/friend` or as `n/John Doe`.

- Items with `…`​ after them can be used multiple times including zero times.<br>
  e.g. `[t/TAG]…​` can be used as ` ` (i.e. 0 times), `t/friend`, `t/friend t/family` etc.

- Work experience parameter `[w/WORK_EXPERIENCE]` can only be used one time. <br>

- Parameters can be in any order.<br>
  e.g. if the command specifies `n/NAME p/PHONE_NUMBER`, `p/PHONE_NUMBER n/NAME` is also acceptable.

- Extraneous parameters for commands that do not take in parameters (such as `help`, `list`, `exit` and `clear`) will be ignored.<br>
  e.g. if the command specifies `help 123`, it will be interpreted as `help`.

- If you are using a PDF version of this document, be careful when copying and pasting commands that span multiple lines as space characters surrounding line-breaks may be omitted when copied over to the application.
  </box>

### Viewing help : `help`

Shows a message explaning how to access the help page.

![help message](images/helpMessage.png)

Format: `help`

<br>

### Adding a person: `add`

Adds a person to the address book.

Format:

```plaintext
add n/NAME p/PHONE_NUMBER e/EMAIL a/ADDRESS u/UNIVERSITY m/MAJOR b/BIRTHDATE [w/WORK_EXPERIENCE] [i/INTEREST]... [t/TAG]...
```

<box type="tip" seamless>

**Tip:** A person can have any number of interests and tags (including 0)
</box>

Parameters:

- `n/NAME`: Full name of the contact.
- `p/PHONE_NUMBER`: Numeric input of any length.
- `e/EMAIL`: Email address in `local-part@domain` format.
- `a/ADDRESS`: Contact's address.
- `u/UNIVERSITY`: University name. It is case-sensitive.
- `m/MAJOR`: Major or field of study.
- `b/BIRTHDATE`: Date of birth in `dd-mm-yyyy` format.
- `[w/WORK_EXPERIENCE]`: Work experience in the format `ROLE,COMPANY,YEAR`, where role, company and year are capitalised.
- `[i/INTEREST]...`: Interests of the contact.
- `[t/TAG]...`: Tags for categorization.

<box type="note" seamless>

**Note:** Contacts can have same names but different phone numbers
</box>

Examples:

```plaintext
add n/John Doe p/98765432 e/johnd@example.com a/311, Clementi Ave 2, #02-25 w/Intern,Google,2024 u/NUS m/Computer Science t/friends t/owesMoney i/swimming i/reading b/13-12-2003
```

```plaintext
add n/Betsy Crowe p/98765431 e/betsycrowe@example.com a/Bishan Street 22, #02-12 w/Intern,Meta,2024 u/NTU m/Computer Science t/classmate b/01-01-2001
```

<br>

### Adding fields to an existing contact

#### Adding Interests: `addi`

Adds interest(s) to an existing contact.

Format:

```plaintext
addi in/INDEX i/INTEREST...
```

- `in/INDEX`: Index of contact user wishes to add interests to. It needs to be a number from 1 to the total number of existing contacts in the contact list.
- `i/INTEREST...`: Interests to add. Can add multiple interests. Note that length of interest can be 20 characters at most.
- **Note:** 
  - Only interests newly added (i.e.were originally not part of the contact's interest list) will be shown on the display message.
  - The first letter of each new interest added will automatically be capitalized in both the display message and in the `interests` field under the specified contact.

Example:

```plaintext
addi in/1 i/Swimming i/Cycling
```

<br>

#### Adding Work Experience: `addw`

Adds work experience to an existing contact.

Format:

```plaintext
addw in/INDEX w/ROLE,COMPANY,YEAR
```

- `in/INDEX`: Contact's position in the list.
- `w/ROLE,COMPANY,YEAR`: Work experience details.

Example:

```plaintext
addw in/1 w/Engineer,Google,2023
```

- `in/INDEX`: Index of contact user wishes to add work experience to. It needs to be a number from 1 to the total number of existing contacts in the contact list.
- `w/ROLE,COMPANY,YEAR`: Work experience details user wishes to add.
  - `ROLE`: Must be a single word without spaces, start with a capital letter, consist only of alphabetic characters. 
  - `COMPANY`: Must be a single word without spaces, start with a capital letter, consist of alphabetic characters. `&` and `-` are the only special characters allowed.
  - `YEAR`: A four-digit year.
- **Note:** If the specified contact already has existing work experience, it will just be replaced by the user input.

Example:

```plaintext
addw in/1 w/Intern,Johnson&Johnson,2024
```

- Adds the work experience `Intern,Johnson&Johnson,2024` to the 1st person in the contact list.

```plaintext
addw in/2 w/Analyst,Procter-Gamble,2024
```

- Adds the work experience `Analyst,Procter-Gamble,2024` to the 2nd person in the contact list.
  
<br>
<div style="page-break-after: always;"></div>

### Listing all persons : `list`

Shows a list of all persons in UniVerse.

Format:

```plaintext
list
```

<br>

### Editing a person : `edit`

Edits an existing person in UniVerse.

Format:

```plaintext
edit INDEX [n/NAME] [p/PHONE] [e/EMAIL] [a/ADDRESS] [t/TAG] [b/BIRTHDATE] [i/INTEREST] [w/WORK_EXPERIENCE] 
[m/MAJOR] [u/UNIVERSITY]…​
```

- **Index:**
  - Edits the person at the specified `INDEX`. The index refers to the index number shown in the displayed person list. The index **must be a positive integer** 1, 2, 3, …​
  - The index should not be longer than 1000. 
- **Updating Values:**
  - At least one of the optional fields must be provided.
  - Existing values will be updated to the input values.
- **Removing Optional Fields:**
  - `Interests`: If the edit command is executed with an empty `i/` field, it will remove the `interests` from the specified contact.
  - `Work Experience`: If the edit command is executed with an empty `w/` field, it will remove the `work experience` from the specified contact.
  - `Tag`: If the edit command is executed with an empty `t/` field, it will remove the `tag` from the specified contact.
**Note:** When editing tags, the existing tags of the person will be removed i.e adding of tags is not cumulative.

Examples:

```plaintext
edit 1 p/91234567 e/johndoe@example.com
```
- Edits the phone number and email address of the 1st person to be `91234567` and `johndoe@example.com` respectively.

```plaintext
edit 2 n/Betsy Crower t/
```
- Edits the name of the 2nd person to be `Betsy Crower` and clears all existing tags.

```plaintext
edit 3 i/
```
- Removes all interests from the third contact.

```plaintext
edit 4 w/
```
- Removes the work experience for the fourth contact.

<br>

### Finding contacts 
#### Locating persons by name: `find`

Finds persons whose names contain any of the given keywords.

Format:

```plaintext
find KEYWORD [MORE_KEYWORDS]
```

<box type="tip" seamless>

**Tip:** Type `list` to view the full list of contacts again.
</box>

- The search is case-insensitive. e.g `hans` will match `Hans`
- The order of the keywords does not matter. e.g. `Hans Bo` will match `Bo Hans`
- Only the name is searched.
- Only full words will be matched e.g. `Han` will not match `Hans`
- Persons matching at least one keyword will be returned (i.e. `OR` search).
  e.g. `Hans Bo` will return `Hans Gruber`, `Bo Yang`

Examples:

```plaintext
find John
```
- returns `john` and `John Doe`

```plaintext
find bob lee
```
- returns `Bob Chen`, `Catherine Lee`<br>

  <img src="images/findBobLeeResult.png" alt="result for 'find bob lee'" style="width: 80%;">

<br>

#### Finding Contacts by Interest: `findi`

Finds contacts with specific interests.

Format:

```plaintext
findi i/INTEREST
```

- `i/INTEREST`: Interest to search for. **Partial matches** are allowed, meaning any contact with an interest that partially matches the provided keyword will be listed.

Example: Finds contacts with the interest "swimming."
- **Exact Match**: 
```plaintext
findi i/swimming
```
- **Partial Match**: 
```plaintext
findi i/swim
```
<br>

<img src="images/findPplSwimming.png" alt="result for 'find i/swimming'" style="width: 80%;">

<br><br>

<box type="warning" seamless>

**Caution**:

Invalid Input: **Searching by multiple interests** is not supported and will trigger an error message:
```plaintext
Invalid command format! 
findi: Finds all persons whose interests contain the specified keyword (case-insensitive) and displays them as a list with index numbers.
Parameters: i/KEYWORD
```
Invalid formats:
```plaintext
findi i/reading i/swimming
```
```plaintext
findi i/reading,i/swimming
```
```plaintext
findi i/reading, i/swimming
```
```plaintext
findi i/reading swimming
```
```plaintext
findi i/reading,swimming
```
```plaintext
findi i/reading, swimming
```
</box>

<br>

#### Finding Contacts by Work Experience: `findw`

Finds contacts with specific work experiences based on **company** and optionally **role** and **year**.

Format:

```plaintext
findw w/ROLE,COMPANY,YEAR
```

- **`COMPANY`**: Required. The name of the company to search for.
- **`ROLE`**: Optional. The role or position held at the company (e.g., `Engineer`).
- **`YEAR`**: Optional. The year of employment at the company.

<box type="info" seamless>

**Note**: The fields `ROLE` and `YEAR` can be omitted, but `COMPANY` must always be specified.
</box>

Examples:

- Find all contacts who worked at Google:
  ```plaintext
  findw w/Google
  ```
- Find contacts who interned at Google:
  ```plaintext
  findw w/Intern,Google
  ```
- Find contacts who interned at Google in 2024:
  ```plaintext
  findw w/Intern,Google,2024
  ```

<br>

#### Finding Contacts by University: `findu`

Finds contacts with a specific university from the currently displayed list.

<box type="tip" seamless>

**Tip:** University name is case-sensitive.

</box>

Format:
```plaintext
findu u/UNIVERSITY
```

<box type="tip" seamless>

**Tip:** University name is case-sensitive.
</box>

- `u/UNIVERSITY`: The university to search for (case-sensitive). **Partial matches** are supported, allowing any contact with a university name that partially matches the keyword to be listed.

Example: Find contacts associated with SUTD.
- **Exact Match**:
```plaintext
findu u/SUTD
```
- **Partial Match**:
```plaintext
findu u/SUT
```

<box type="info" seamless>

**Note**:
The `findu` command operates based on the **current list of contacts displayed**. To ensure you search from the full contact list, type `list` before using `findu`. This refreshes the view to show all contacts, allowing `findu` to accurately filter contacts from the complete data set.

</box>

**Example Workflow**:
1. Type `list` to display all contacts.
2. Use `findu u/NUS` to filter and show only contacts from NUS.

<br>

#### Finding Contacts by Major: `findm`

Finds contacts with a specific major from the currently displayed list.

Format:

```plaintext
findm m/MAJOR
```

- `m/MAJOR`: Major or field of study. **Partial matches** are supported, so any contact with a major that partially matches the provided keyword will be included.

Example: Finds contacts with the major "Computer Science"
- **Exact Match**:
```plaintext
findm m/Computer Science
```
- **Partial Match**:
```plaintext
findm m/Comp
```
<img src="images/findPplCS.png" alt="result for 'findm m/Computer Science'" style="width: 80%;">


<br><br>

### Deleting a person : `delete`

Deletes the specified person from the address book.

```plaintext
delete INDEX
```

- Deletes the person at the specified `INDEX`.
- The index refers to the index number shown in the displayed person list.
- The index **must be a positive integer** 1, 2, 3, …​

Examples:

- `list` followed by `delete 2` deletes the 2nd person in the address book.
- `find Betsy` followed by `delete 1` deletes the 1st person in the results of the `find` command.

<br>

### Clearing all entries : `clear`

Clears all entries from the address book.

```plaintext
clear
```
<br>

### Exiting the program : `exit`

Exits the program.

```plaintext
exit
```

<br>

## Data Management

### Saving the data

UniVerse data are saved in the hard disk automatically after any command that changes the data. There is no need to save manually.

### Editing the data file

UniVerse data are saved automatically as a JSON file `[JAR file location]/data/UniVerse.json`. Advanced users are welcome to update data directly by editing that data file.

<box type="warning" seamless>

**Caution:**
If your changes to the data file makes its format invalid, UniVerse will discard all data and start with an empty data file at the next run. Hence, it is recommended to take a backup of the file before editing it.<br>
Furthermore, certain edits can cause the UniVerse to behave in unexpected ways (e.g., if a value entered is outside the acceptable range). Therefore, edit the data file only if you are confident that you can update it correctly.
</box>

### Archiving data files `[coming in v2.0]`

_Details coming soon ..._

---

<div style="page-break-after: always;"></div>

## FAQ

**Q**: How do I transfer my data to another Computer?<br>
**A**: Install the app in the other computer and overwrite the empty data file it creates with the file that contains the data of your previous UniVerse home folder.

---

## Known issues


1. **When using multiple screens**, if you move the application to a secondary screen, and later switch to using only the primary screen, the GUI will open off-screen. The remedy is to delete the `preferences.json` file created by the application before running the application again.
2. **If you minimize the Help Window** and then run the `help` command (or use the `Help` menu, or the keyboard shortcut `F1`) again, the original Help Window will remain minimized, and no new Help Window will appear. The remedy is to manually restore the minimized Help Window.
3. **Major and University Field Validation**:
    - The application currently allows numbers-only input for the **major** and **university** fields (e.g., `m/12345` or `u/9876`), which is unintended.
    - **Limitation**: The app does not restrict users from entering numerical values or potential module codes as majors and universities.
    - **Planned Solution**: We plan to introduce stricter input validation to prevent numbers-only entries for these fields in future versions.
4. **After deleting fields in json data file**, upon running the Universe app, the address book returned is empty but without an error message.
5. **When adding a new contact**, the `birthday` field is compulsory and it is allowed to be a date in the future.
6. **When adding `interests` to contacts**, running the `addi` command with multiple `in/` prefixes (e.g., `addi in/1 in/2 i/interest`), only the contact specified by the last index will receive the newly added interest. Therefore, users should specify only one `in/` prefix to avoid ambiguity.
7. **When adding `work experience` to contacts** : 
    - `role` field cannot contain numbers or special characters. `company` field cannot contain numbers. Additionally, `year` is allowed to be in the future.
    - The application currently allows numbers-only input for the **major** and **university** fields (e.g., `m/12345` or `u/9876`), which is unintended.
    - **Limitation**: The `role` and `company` fields for the `addw` command cannot contain spaces and can only consist of one word
    - **Planned Solution**: We plan to relax the input validation to allow :
      - Spaces after commas
      - Optional capitalization in the first word
      - Multi-word inputs for both role and company (e.g., `software engineer, Jane Street, 2024`)



---

## Glossary

- **CLI (Command Line Interface)**: A user interface that allows interaction with the application through text-based commands, enabling quick and efficient data entry and command execution.

- **GUI (Graphical User Interface)**: The visual component of the application that users interact with. It includes buttons, panels, and other visual elements to make navigation easier.

- **Keyword**: A word or phrase used to search for or filter contacts within the app (e.g., an interest or university name in search commands).

- **Index**: The numerical identifier assigned to each contact in the list, used in commands such as `delete 1` or `edit 2` to specify which contact is being referenced.

- **Tag**: A label attached to a contact for categorization and easy filtering. Tags help organize contacts based on shared attributes or groups.

- **University**: The name of the institution where a contact is studying or has studied. This field helps users find and connect with peers from specific universities.

- **Major**: The field of study that a contact is pursuing or has completed. It helps users find contacts within the same academic field.

- **Work Experience**: Information detailing a contact’s professional experience, formatted as `role,company,year` (e.g., `Intern,Google,2023`).

- **Interest**: A hobby or activity that a contact is interested in, used to connect with others who share similar interests.

- **Find Command**: A command used to filter and display contacts based on specific criteria (e.g., `findu`, `findm`, `findi`, `findw`).

- **Alphanumeric**: Refers to characters that are either letters (A-Z, a-z) or numbers (0-9). It may include symbols such as underscores (_) and hyphens (-) in certain contexts, but generally excludes special characters unless specified.

- **Case-Insensitive**: A search term or keyword that matches regardless of whether it is in uppercase or lowercase (e.g., `findu u/nus` matches both "NUS" and "nus").

- **Partial Match**: A feature in some commands where the search does not require an exact match of the keyword, but can find results that contain the keyword as part of a longer string (e.g., `findm m/Comp` could match "Computer Science" and "Computer Engineering").

---

## Command Summary
| Action                                      | Format, Examples                                                                                                                                                                                                                                                                                       |
|---------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Add new contact**                         | `add n/NAME p/PHONE_NUMBER e/EMAIL a/ADDRESS u/UNIVERSITY m/MAJOR b/BIRTHDATE [w/WORK_EXPERIENCE] [i/INTEREST]... [t/TAG]...`<br> e.g., `add n/Alice Tan p/91234567 e/alice@example.com a/Blk 123 Clementi Ave 3, #05-10 u/NTU m/Engineering b/15-04-2000 w/Intern,Google,2023 i/Photography t/friend` |
| **Add Interests to existing contact**       | `addi in/INDEX i/INTEREST...` <br> e.g., `addi in/1 i/Swimming`                                                                                                                                                                                                                                        |
| **Add Work Experience to existing contact** | `addw in/INDEX w/ROLE,COMPANY,YEAR` <br> e.g., `addw in/1 w/Intern,Google,2023`                                                                                                                                                                                                                        |
| **Delete a contact**                        | `delete INDEX` <br> e.g., `delete 3`                                                                                                                                                                                                                                                                   |
| **Edit an existing contact**                | `edit INDEX [n/NAME] [p/PHONE_NUMBER] [e/EMAIL] [a/ADDRESS] [u/UNIVERSITY] [m/MAJOR] [b/BIRTHDATE] [w/WORK_EXPERIENCE] [i/INTEREST]... [t/TAG]...` <br> e.g., `edit 2 n/James Lee e/jameslee@example.com`                                                                                              |
| **Delete all contacts**                     | `clear`                                                                                                                                                                                                                                                                                                |
| **Find by Name**                            | `find KEYWORD [MORE_KEYWORDS]`<br> e.g., `find James Jake`                                                                                                                                                                                                                                             |
| **Find by Interest**                        | `findi i/INTEREST` <br> e.g., `findi i/Swimming`                                                                                                                                                                                                                                                       |
| **Find by Work Experience**                 | `findw w/[ROLE],COMPANY,[YEAR]` <br> e.g., `findw w/Engineer,Google`, `findw w/Google`, `findw w/Google,2024`                                                                                                                                                                                          |
| **Find by University**                      | `findu u/UNIVERSITY` <br> e.g., `findu u/NUS`                                                                                                                                                                                                                                                          |
| **Find by Major**                           | `findm m/MAJOR` <br> e.g., `findm m/Computer Science`                                                                                                                                                                                                                                                  |
| **List all contacts**                       | `list`                                                                                                                                                                                                                                                                                                 |
| **Help**                                    | `help`                                                                                                                                                                                                                                                                                                 |
| **Exit the application**                    | `exit`                                                                                                                                                                                                                                                                                                 |

