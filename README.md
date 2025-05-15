# 🔁 Forward Chaining Inference

This project demonstrates **forward chaining in propositional logic** using **Horn clauses**. It is implemented in a Jupyter Notebook: `Process2.ipynb`.

The notebook reads a set of logical facts and rules from a file (`data.txt`), applies forward chaining to infer a given query, and generates two visualizations of the process using Graphviz.

---

## 📂 Project Structure

```
.
├── Process2.ipynb        # Jupyter Notebook containing the entire logic
├── data.txt              # Input file with facts and Horn clauses
├── kb_graph.png          # Visual graph of the knowledge base
├── inference_graph.png   # Graph showing inference path for the query
└── README.md             # Documentation
```

---

## 📘 Code Structure (in `Process2.ipynb`)

The notebook is structured into these main components:

### 1. **Clause**
A class representing a single Horn clause:  
```text
premises → conclusion
```
It tracks which premises have been satisfied during inference.

---

### 2. **KnowledgeBase**
Stores:
- A set of known **facts**
- A list of **rules** (clauses)

Provides helper methods to access relevant clauses.

---

### 3. **ForwardChaining**
Implements the core logic of forward chaining:
- Infers whether a **query** can be deduced
- Tracks which rules were used
- Visualizes the **inference path** to the query

---

### 4. **Problem**
Handles input parsing:
- Reads `data.txt`
- Converts lines into **facts** and **rules**
- Prints De Morgan transformations for educational traceability

Also includes a method to visualize the entire **knowledge base graph**.

---

### 5. **Main Execution**
At the bottom of the notebook:
- Loads the problem from `data.txt`
- Runs forward chaining for a specified query
- Prints the result and inference chain
- Saves two PNG visualizations:
  - `kb_graph.png`
  - `inference_graph.png`

---

## 🧾 Input File Format (`data.txt`)

Each line is either:
- A **fact** (positive literal):  
  ```
  a
  ```
- A **rule** (Horn clause):  
  ```
  -a -b c    # means: a ∧ b → c
  ```

Negated literals (premises) are prefixed with `-` or `¬`.

Example file:

```
a
b
-c d
-d e
-e f
-f g
```

---

## 📈 Output Graphs

### `kb_graph.png`
Visualizes the entire knowledge base:
- **Facts** are colored in blue
- **Rules** are shown with connecting arrows via dot (•) nodes

### `inference_graph.png`
Shows only the path of inference that leads to the queried conclusion.

Each node and edge illustrates which facts and rules contributed to the final result.

---

## 🚀 How to Run

1. Make sure you have Python and Jupyter Notebook installed.
2. Install Graphviz and the Python binding:
   ```bash
   pip install graphviz
   ```
3. Open and run `Process2.ipynb`.
4. Check the console output for:
   - De Morgan transformations
   - Whether the query was inferred
   - The rule chain used
5. Check `kb_graph.png` and `inference_graph.png` for visualizations.

---

## 📌 Example

`data.txt`

```text
-a -b c
-b -c -d e
a
b
d
```

Change the query in `Main Execution` section

```python
# --- Main Execution ---
if __name__ == '__main__':
    problem = Problem('data.txt')

    query = 'c' # here
```

Output



```
=== De Morgan Conversion for Forward Chaining Rules ===

[Line 1] -a -b c
  Step 1 - Disjunction:   ¬a ∨ ¬b ∨ c
  Step 2 - De Morgan:     c ∨ ¬(a ∧ b)
  Step 3 - Implication:   a ∧ b → c

[Line 2] -b -c -d e
  Step 1 - Disjunction:   ¬b ∨ ¬c ∨ ¬d ∨ e
  Step 2 - De Morgan:     e ∨ ¬(b ∧ c ∧ d)
  Step 3 - Implication:   b ∧ c ∧ d → e

[Line 3] a -> FACT: a

[Line 4] b -> FACT: b

[Line 5] d -> FACT: d


✅ Query 'c' was inferred using these rules:
  -> b ∧ a → c

🔍 Result: Can we deduce 'c'? True

📊 Knowledge graph saved to 'kb_graph.png' and opened for viewing.

📈 Inference graph saved to 'inference_graph.png' and opened for viewing.
```

**Generated graphs**:

- [kb_graph](kb_graph.png)
- [inference_graph](inference_graph.png)

---

## 📝 License

MIT License.  
Feel free to use or adapt this notebook for research, learning, or teaching purposes.


