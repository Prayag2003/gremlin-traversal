# 🧪 Gremlin Tutorial 1: Introduction to the Modern Toy Graph

This tutorial introduces you to the basics of Gremlin — the graph traversal language — using the **TinkerPop "Modern" toy graph**. You'll learn how to create the graph, interact with its vertices and edges, and perform simple traversals to query data.

---

## 📘 Background: What is Gremlin?

Gremlin is a **functional, path-based graph traversal language** that works across various graph database engines (e.g., TinkerGraph, JanusGraph, Amazon Neptune). You use it to describe **how to walk through a graph**, one step at a time, using vertices, edges, labels, and properties.

---

## 🧱 The Modern Toy Graph

TinkerPop provides a sample graph called `Modern`, which looks like this:

```

(1) marko ──knows──▶ (2) vadas
│
├─knows──▶ (4) josh
└─created▶ (3) lop
▲
(4) josh ───┘
(6) peter ──created──▶ (3) lop

```

Each vertex has properties like `name`, `age`, and `label` (e.g., "person", "software").

---

## ✅ Setup and Initialization

```groovy
// Load the toy graph
graph = TinkerFactory.createModern();

// Create a traversal source
g = graph.traversal();
```

---

## 🔍 Basic Traversals

### 1. Get all vertices

```groovy
g.V()
```

Returns all vertices in the graph.

---

### 2. Get vertex by ID

```groovy
g.V(1)
```

Returns the vertex with ID `1` (i.e., "marko").

---

### 3. Get a property value of a vertex

```groovy
g.V(1).values("name")
```

Returns `"marko"` — the `name` property of vertex 1.

---

## 🔁 Traversing Edges and Neighbors

### 4. Get outgoing edges from vertex 1 with label `knows`

```groovy
g.V(1).outE("knows")
```

Returns the edges from Marko to the people he "knows".

---

### 5. Get the names of people Marko knows (long version)

```groovy
g.V(1).outE("knows").inV().values("name")
```

- `outE("knows")`: traverse outgoing "knows" edges.
- `inV()`: move to the vertex at the other end of the edge.
- `values("name")`: extract their names.

---

### 6. Same as above, but concise

```groovy
g.V(1).out("knows").values("name")
```

- `out("knows")`: shortcut for `outE("knows").inV()`.

---

### 7. People Marko knows who are over 30

```groovy
g.V(1).out("knows").has("age", gt(30)).values("name")
```

- `has("age", gt(30))`: filters people with age > 30.
- Returns `"josh"` if using the default Modern graph.

---

## 📎 Summary of Steps

| Traversal                                               | Description                                 |
| ------------------------------------------------------- | ------------------------------------------- |
| `g.V()`                                                 | All vertices                                |
| `g.V(1)`                                                | Vertex with ID 1                            |
| `g.V(1).values("name")`                                 | Name of vertex 1                            |
| `g.V(1).outE("knows")`                                  | Outgoing "knows" edges                      |
| `g.V(1).out("knows").values("name")`                    | Names of people Marko knows                 |
| `g.V(1).out("knows").has("age", gt(30)).values("name")` | Names of people Marko knows who are over 30 |

---

## 🧠 Additional Notes

- Use `Ctrl+C` to escape multiline prompt errors in Gremlin Console.
- Use `:help` in console to see Gremlin shell commands.
- The Modern graph is **in-memory** — changes are **not persisted** unless explicitly saved.

---

## 📌 Next Up

In **Tutorial 2**, we'll cover:

- Edge and vertex filtering
- Grouping and counting
- Path traversals and subgraphs

Stay tuned!
