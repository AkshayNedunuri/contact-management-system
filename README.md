# Smart Contact Management System Using Java & DSA

> **A robust, console-based Smart Contact Management System built using Java and core Data Structures & Algorithms (DSA). Designed as a premier college project for B.Tech Computer Science and Engineering (CSE).**

---

## 1. Project Overview

The **Smart Contact Management System** is an application designed to manage personal and professional contacts efficiently while showcasing real-world applications of:
- **Object-Oriented Programming (OOP):** Encapsulation, abstraction, constructor overloading, and method overriding.
- **Java Collections Framework:** `ArrayList`, `HashMap`, and `HashSet`.
- **Algorithms:** Linear Search, Binary Search, and Comparator-based TimSort.
- **Data Persistence:** File I/O stream processing for offline data storage (`contacts.txt`).
- **Defensive Programming:** Robust input validation and edge-case handling.

---

## 2. Project Architecture & File Structure

```
contact-management-system/
├── bin/                          # Compiled bytecode (.class files)
├── data/
│   └── contacts.txt              # Persistent storage file (CSV format)
├── src/
│   ├── Contact.java              # Entity model with encapsulation & hashing
│   ├── ContactManager.java       # Business logic & Collection synchronizer
│   ├── ContactSearch.java        # Searching (Linear/Binary) & Sorting algorithms
│   ├── FileStorage.java          # File I/O handler for saving & loading
│   └── Main.java                 # Interactive CLI menu & input validation
└── README.md                     # Project documentation & viva guide
```

### Module Responsibilities:
| File | Responsibility |
|---|---|
| [Contact.java](file:///c:/Users/aksha/OneDrive/Desktop/contact-management%20-system/src/Contact.java) | Represents an individual contact (Name, Phone, Email, Category, Favorite). Implements `equals()`, `hashCode()`, and CSV formatting. |
| [ContactManager.java](file:///c:/Users/aksha/OneDrive/Desktop/contact-management%20-system/src/ContactManager.java) | Maintains synchronized state across `ArrayList`, `HashMap`, and `HashSet`. Handles CRUD operations, category filtering, and favorite toggling. |
| [ContactSearch.java](file:///c:/Users/aksha/OneDrive/Desktop/contact-management%20-system/src/ContactSearch.java) | Implements Linear Search (substring matching), Binary Search (on sorted list), and multiple `Comparator` sorting implementations. |
| [FileStorage.java](file:///c:/Users/aksha/OneDrive/Desktop/contact-management%20-system/src/FileStorage.java) | Reads and writes records to `data/contacts.txt`. Gracefully recovers from missing or corrupted records. |
| [Main.java](file:///c:/Users/aksha/OneDrive/Desktop/contact-management%20-system/src/Main.java) | Interactive console-driven menu using `Scanner`, regex input validation, and user notification messages. |

---

## 3. Data Structures & Algorithms (DSA) Rationale

### Why Each Data Structure is Used:
1. **`ArrayList<Contact>` (Primary Sequence):**
   - **Why:** Contacts need to be displayed in a numbered, ordered list, sorted alphabetically, or filtered dynamically. An `ArrayList` provides $O(1)$ indexed access and dynamic resizing.
2. **`HashMap<String, Contact>` (Direct Lookup):**
   - **Why:** Searching by a primary key (phone number) in a list takes $O(N)$ time. By indexing phone numbers in a `HashMap`, we retrieve any contact in **$O(1)$ constant time**.
3. **`HashSet<String>` (Duplicate Detection):**
   - **Why:** When adding a new contact or updating a number, checking for duplicate phone numbers in a list takes $O(N)$ time. `HashSet` performs membership checks in **$O(1)$ average time**.
4. **`Comparator<Contact>` (Sorting):**
   - **Why:** Provides flexible, decoupled sorting logic (by Name A-Z, Name Z-A, and by Category) without altering the `Contact` class.
5. **Linear Search vs. Binary Search:**
   - **Linear Search:** Used for flexible partial/substring searches (e.g. searching "ali" finds "Alice"). Time: $O(N)$.
   - **Binary Search:** Used for exact name queries on a sorted list. Employs divide-and-conquer to cut the search space in half each iteration. Time: $O(\log N)$.

---

## 4. Big-O Time & Space Complexity Analysis

| Operation | Data Structure / Algorithm | Best Case | Average Case | Worst Case | Space Complexity |
|---|---|---|---|---|---|
| **Add Contact** | `HashSet.contains()` + `ArrayList.add()` | $O(1)$ | $O(1)$ | $O(1)^*$ | $O(1)$ |
| **Lookup by Phone** | `HashMap.get(phone)` | $O(1)$ | $O(1)$ | $O(N)^{**}$ | $O(1)$ |
| **Search by Name (Substring)** | Linear Search (`for` loop) | $O(1)$ | $O(N)$ | $O(N)$ | $O(k)$ matches |
| **Search by Name (Exact)** | Binary Search (Divide & Conquer) | $O(1)$ | $O(\log N)$ | $O(\log N)$ | $O(1)$ |
| **Sort Contacts (A-Z)** | TimSort (`Collections.sort`) | $O(N)$ | $O(N \log N)$ | $O(N \log N)$ | $O(N)$ |
| **Delete Contact** | `Map/Set.remove()` + `ArrayList.remove()` | $O(1)$ | $O(N)$ | $O(N)$ | $O(1)$ |
| **Filter by Category** | Linear Scan | $O(N)$ | $O(N)$ | $O(N)$ | $O(k)$ matches |
| **Toggle Favorite** | `HashMap.get()` + setter | $O(1)$ | $O(1)$ | $O(1)$ | $O(1)$ |
| **Save / Load from File** | BufferedReader / BufferedWriter | $O(N)$ | $O(N)$ | $O(N)$ | $O(N)$ |

*\* Amortized time when ArrayList resizes.*  
*\*\* Worst case for hash table occurs only with extreme hash collisions.*

---

## 5. How to Compile and Run

### Prerequisites
- Java Development Kit (JDK 17 or higher recommended, JDK 25 tested).
- Visual Studio Code or any terminal (PowerShell, CMD, Bash).

### Quick Run Commands (PowerShell / Command Prompt)

1. Open a terminal in the project root directory:
   ```powershell
   cd "c:\Users\aksha\OneDrive\Desktop\contact-management -system"
   ```

2. Compile all source files into the `bin` folder:
   ```powershell
   javac -d bin src/*.java
   ```

3. Run the application:
   ```powershell
   java -cp bin Main
   ```

---

## 6. Sample Application Walkthrough

### Main Menu Interface
```text
========================================================
                     MAIN MENU                          
========================================================
  1. Add New Contact (Duplicate Check: HashSet)
  2. View All Contacts
  3. Search Contacts (Linear & Binary Search)
  4. Update Contact Details
  5. Delete Contact (O(1) Map/Set, O(N) List)
  6. Sort Contacts (Alphabetical / Category)
  7. Filter Contacts (By Category / Favorites)
  8. Toggle Favorite (* [FAV])
  9. File Storage (Manual Save / Reload)
  0. Save & Exit Application
========================================================
Enter your choice (0-9): 2
```

### Formatted Contacts Table Display
```text
====================================================================================================
#    | STATUS     | NAME                   | PHONE          | EMAIL                     | CATEGORY    
----------------------------------------------------------------------------------------------------
1    | * [FAV]    | Alice Smith            | 9876543210     | alice@example.com         | Friends     
2    | * [FAV]    | Bob Johnson            | 9123456780     | bob@example.com           | Work        
3    | * [FAV]    | Charlie Brown          | 9988776655     | charlie@college.edu       | College     
4    |            | David Miller           | 9011223344     | david.m@work.org          | Work        
5    | * [FAV]    | Emily Davis            | 9445566778     | emily@family.net          | Family      
====================================================================================================
Total Count: 5
```

---

## 7. Edge Cases Handled

1. **Duplicate Phone Numbers:** Prevents storing duplicate entries using $O(1)$ `HashSet` lookups before prompting for remaining details.
2. **Invalid Phone Number:** Rejects numbers that are not exactly 10 numeric digits.
3. **Invalid Email Format:** Validates standard email patterns (e.g. `user@example.com`) while allowing users to skip if not available.
4. **Empty Inputs:** Rejects empty contact names or blank mandatory fields.
5. **Missing File on Startup:** If `data/contacts.txt` does not exist, the app gracefully creates default starter contacts and saves them without crashing.
6. **Corrupted File Lines:** Malformed rows in `contacts.txt` are caught, logged, and skipped without halting application loading.

---

## 8. College Viva Voce Questions & Answers

### Q1: Why did you use three collections (`ArrayList`, `HashMap`, `HashSet`) instead of just one?
**Answer:** Each data structure optimizes a different operation:
- `ArrayList` preserves sequence, allows indexed display, and supports sorting via `Collections.sort`.
- Searching a contact by phone number in an `ArrayList` takes $O(N)$ linear time. A `HashMap` provides instant $O(1)$ retrieval.
- A `HashSet` gives immediate $O(1)$ verification for duplicate detection when creating or updating contacts.

### Q2: Why is it necessary to override both `equals()` and `hashCode()` in the `Contact` class?
**Answer:** The Java **equals and hashCode contract** requires that if two objects are equal according to `equals(Object)`, their `hashCode()` must produce the same integer. If we only override `equals()` and not `hashCode()`, two contact objects with the identical phone number might map to different buckets in a `HashSet` or `HashMap`, breaking duplicate detection.

### Q3: When should you use Binary Search over Linear Search?
**Answer:** Binary Search is far superior ($O(\log N)$ vs $O(N)$) for large datasets, but it **requires the list to be sorted**. Linear Search works on unsorted lists and supports partial substring queries (e.g., finding "David" when searching "da").

### Q4: How does TimSort work in Java's `Collections.sort()`?
**Answer:** TimSort is a hybrid stable sorting algorithm derived from Merge Sort and Insertion Sort. It has a best-case time complexity of $O(N)$ on nearly sorted data and a guaranteed worst-case complexity of $O(N \log N)$.

### Q5: How is data persistence handled?
**Answer:** Contacts are serialized into Comma-Separated Values (CSV) format and stored in `data/contacts.txt`. We use Java's `BufferedReader` and `BufferedWriter` wrapped inside `try-with-resources` blocks to guarantee that file streams are automatically flushed and closed even if an exception occurs.

---

## 9. Future Improvements
- **Graphical User Interface (GUI):** Implement a modern JavaFX or Swing desktop UI.
- **Relational Database:** Migrate storage from text files to SQLite or MySQL using JDBC.
- **Trie Data Structure:** Implement a Prefix Tree (Trie) for real-time contact search autocomplete.
- **Export & Import:** Add support for `.vcf` (vCard) and `.csv` export/import formats.
