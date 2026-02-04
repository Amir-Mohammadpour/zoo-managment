# 🐾 Zoo Animal Management System

![C++](https://img.shields.io/badge/language-C%2B%2B-blue)
![CLI App](https://img.shields.io/badge/type-CLI-green)
![Status](https://img.shields.io/badge/status-stable-brightgreen)

A command-line C++ application for managing animals in a zoo environment.  
The system provides structured record management including validation, search, editing, prioritised feeding logic, and persistent storage.

Designed as a lightweight data management engine demonstrating use of STL containers, sorting algorithms, file I/O, and stateful command processing.

---

## ✨ Features

- Structured animal record system
- Cage allocation with validation constraints
- Name and cage-based search
- Editable animal attributes
- Safe deletion and updates
- Deterministic sorting
- Priority-based feeding algorithm
- Persistent save/load functionality
- Command-driven interactive interface

---

## 📦 Data Model

Each animal is represented by:

| Field | Type | Description |
|------|------|-------------|
| name | string | Animal name |
| cage_number | int | Unique cage ID |
| year_of_entry | int | Year added to zoo |
| is_rare | bool | Rare animal flag |
| is_fed | bool | Feeding status |

Internally stored in a dynamic `std::vector<ANIMAL>`.

---

## 🧠 Feeding Algorithm (Priority Logic)

The feeding system selects animals that have **not yet been fed**, then sorts them using a two-level priority strategy:

1. Rare animals are prioritised over non-rare animals
2. Among equal rarity, older entries are fed first

This guarantees:

- Conservation priority
- Deterministic ordering
- Fairness over time

Sorting comparator:

rare animals > non-rare animals
earlier year_of_entry > later year_of_entry

Time complexity: **O(n log n)** due to sorting.

---

## ▶️ Build & Run

### Compile

```bash
g++ main.cpp -o zoo

Execute
./zoo


The program reads commands from standard input.

📘 Command Reference
SET

Define total number of cages:
SET <number>

ADD
ADD <name> <cage_number> <year_of_entry> <is_rare>
Adds a new animal with validation checks.

SEARCH
By name:
SEARCH name <animal_name>
By cage:
SEARCH cage_number <number>

LIST
LIST
Displays all animals.

DELETE
DELETE <cage_number>
Removes an animal from a cage.

EDIT
EDIT <cage_number> <field> <value>
Editable fields:
name
cage_number
year_of_entry
is_rare (toggle)
is_fed (toggle)

SORT
SORT
Sorts animals alphabetically by name, then by cage number.

FEED
FEED <count>
Feeds a selected number of animals using priority logic.

SAVE
SAVE filename.txt
Writes records to disk.

LOAD
LOAD filename.txt
Restores records from file.

EXIT
EXIT
Terminates the program.

▶️ Demo Session

Example interactive session:
SET 5
ADD lion 1 2020 1
ADD tiger 2 2018 0
ADD panda 3 2015 1
LIST
FEED 2
SAVE zoo.txt
EXIT


Output:
The animal named lion was added successfully
The animal named tiger was added successfully
The animal named panda was added successfully
lion 1 2020 1
tiger 2 2018 0
panda 3 2015 1
The animal named panda was fed
The animal named lion was fed
Animals were saved successfully

📂 Storage Format
Each line in the save file:
name cage_number year_of_entry is_rare is_fed

Example:
lion 1 2020 1 0
tiger 2 2018 0 1

⚠️ Validation Rules
Name must be ≥ 2 characters
Cage must exist within defined range
Each cage holds at most one animal
LOAD fails if file is missing
🏗 Technical Highlights
STL vectors and custom comparators
Deterministic sorting
File stream persistence
Input validation layer
Command dispatcher architecture
Mutable in-memory state model

📄 License
MIT — free to use and modify.
