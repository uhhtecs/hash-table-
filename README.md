<<<<<<< HEAD
# Doctor Reporting Tree & Emergency Queue

This assignment simulates a medical management system built using non-linear data structures. Students will implement a custom binary tree to model a doctor reporting structure and a min-heap to manage patient urgency in an emergency room queue. These components provide practice in recursive methods, priority-based operations, and tree traversal techniques.

## Classes

### `DoctorNode` Class
Represents a doctor in the reporting hierarchy.

**Constructor**
```python
DoctorNode(name)
```

**Attributes**
- `name` (str): The doctor’s name.
- `left` (DoctorNode or None): Reference to the left report.
- `right` (DoctorNode or None): Reference to the right report.

### `DoctorTree` Class
Manages the binary tree structure of doctor reports.

**Constructor**
```python
DoctorTree()
```

**Attributes**
- `root` (DoctorNode or None): Reference to the root doctor.

**Methods**
- `insert(parent_name: str, employee_name: str, side: str) -> bool`
  - Adds a new doctor under a specified parent node on the given side.
- `preorder(node: DoctorNode) -> list`
  - Returns a list of doctor names using preorder traversal.
- `inorder(node: DoctorNode) -> list`
  - Returns a list of doctor names using inorder traversal.
- `postorder(node: DoctorNode) -> list`
  - Returns a list of doctor names using postorder traversal.

---

### `Patient` Class
Represents a patient waiting for emergency care.

**Constructor**
```python
Patient(name, urgency)
```

**Attributes**
- `name` (str): The patient’s name.
- `urgency` (int): A score from 1 to 10, where 1 is most urgent.

### `MinHeap` Class
Manages patients using a priority queue based on urgency.

**Constructor**
```python
MinHeap()
```

**Attributes**
- `data` (list): List of Patient instances. Index 0 is the most urgent patient.

**Methods**
- `insert(patient: Patient) -> None`
  - Adds a new patient and reorders the heap.
- `remove_min() -> Patient`
  - Removes and returns the most urgent patient.
- `peek() -> Patient`
  - Returns the most urgent patient without removing.
- `print_heap() -> None`
  - Prints each patient and their urgency level.
=======
# Contact Hash Table
This project implements a contact management system using a custom-built hash table in Python. Instead of using Python’s built-in dictionary, you’ll define a hash table from scratch that stores and retrieves `Contact` objects based on a user’s name.

The system uses separate chaining to handle hash collisions, meaning each array index contains a linked list of contacts that share the same hash value. This assignment deepens your understanding of how hash tables work behind the scenes and how to resolve collisions—a key concept for systems that rely on fast lookups like databases, caches, and contact directories.

## Features
- Insert new contacts by name and number
- Automatically update a contact’s number if the name already exists
- Handle collisions using linked lists
- Search for contacts by name
- Print the entire hash table, including all chained contacts

## Classes

### `Contact` Class
Represents a single contact with a name and phone number.

**Constructor**

```python
Contact(name: str, number: str)
```

**Attributes**
- `name` (str): The contact's name
- `number` (str): The contact's phone number (e.g. `"123-456-7890"`)

**Methods**
- `__str__() -> str`: Returns the contact in the format `"[CONTACT_NAME]: [CONTACT_NUMBER]"`

**Example Usage**
```python
contact_1 = Contact("Riley", "123-456-7890")
print(contact_1.name) # Riley
print(contact_1.number) # 123-456-7890 
print(contact_1) # Riley: 123-456-7890 
```

### `Node` Class
Represents a node in a linked list used to resolve hash collisions.

**Constructor**
```python
Node(key: str, value: Contact)
```

**Attributes**
- `key` (str): The key associated with the contact (typically the contact’s name)
- `value` (Contact): The `Contact` object stored at this node
- `next` (Node or None): Pointer to the next node in the list (default is `None`)

**Example Usage**
```python
contact_1 = Contact("Riley", "123-456-7890")
node_1 = Node(contact_1.name, contact_1)
print(node_1.key) # Riley 
print(node_1.value) # Riley: 123-456-7890 
print(node_1.next) # None 
```

### `HashTable` Class
Implements a hash table with separate chaining to store and retrieve contacts.

**Constructor**

```python
HashTable(size: int)
```

**Attributes**
- `size` (int): The number of slots in the underlying array
- `data` (list of Node or None): The array itself; each element is either `None` or a linked list of `Node` objects

**Methods**
- `hash_function(key: str) -> int`: Computes a hash value for the given key (e.g., using `ord()` values)
- `insert(key: str, number: str) -> None`: Creates a new `Contact` object and adds it to the table. If a contact with the same name already exists, updates the number.
- `search(key: str) -> Contact or None`: Searches for a contact by name and returns the `Contact` object if found. If no contact is found to match the `key`, then `None` is returned.
- `print_table() -> None`: Prints each index of the hash table and all contacts stored at that index.

**Example Usage**
```python
table = HashTable(10)
table.print_table()
'''
Index 0: Empty
Index 1: Empty
Index 2: Empty
Index 3: Empty
Index 4: Empty
Index 5: Empty
Index 6: Empty
Index 7: Empty
Index 8: Empty
Index 9: Empty 
'''
# Add some values
table.insert("John", "909-876-1234")
table.insert("Rebecca", "111-555-0002")
# Print the new table structure 
table.print_table()
'''
Index 0: Empty
Index 1: Empty
Index 2: Empty
Index 3: Empty
Index 4: Empty
Index 5: Empty
Index 6: Empty
Index 7: - Rebecca: 111-555-0002 
Index 8: Empty
Index 9: - John: 909-876-1234 
'''
# Search for a value
contact = table.search("John") 
print("\nSearch result:", contact)  # Search result: John: 909-876-1234 

# Edge Case #1 - Hash Collisons (assuming these hash to the same index) 
table.insert("Amy", "111-222-3333") 
table.insert("May", "222-333-1111")  # May collide with Amy depending on hash function 
table.print_table()
'''
Index 0: Empty
Index 1: Empty
Index 2: Empty
Index 3: Empty
Index 4: Empty
Index 5: - Amy: 111-222-3333 - May: 222-333-1111 
Index 6: Empty
Index 7: - Rebecca: 111-555-0002 
Index 8: Empty
Index 9: - John: 909-876-1234 
'''
# Edge Case #2 - Duplicate Keys 
table.insert("Rebecca", "999-444-9999")  # Should update Rebecca's number 
table.print_table()
'''
Index 0: Empty
Index 1: Empty
Index 2: Empty
Index 3: Empty
Index 4: Empty
Index 5: - Amy: 111-222-3333 - May: 222-333-1111 
Index 6: Empty
Index 7: - Rebecca: 999-444-9999 
Index 8: Empty
Index 9: - John: 909-876-1234 
'''
# Edge Case #3 - Searching for a value not in the table
print(table.search("Chris")) # None
```
>>>>>>> cf42a6d5912cd75b29e835b70f52f6a3353702f7
